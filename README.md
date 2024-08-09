# smarty_init
## `Codeigniter 3.1.13 `
## `smarty 4.5.0`

### Khởi tạo smarty với codeigniter 3 (8/8/2024)
+ Bước 1: Tải CI3 từ [trang chủ](https://codeigniter.com/download).
+ Bước 2: Tải smarty từ [trang chủ](https://www.smarty.net/download), giải nén (lưu tên file   
  là smarty) và lưu vào thư mục application/third_party.
+ Bước 3: Trong application/libraries tạo SmartyLibrary.php   
  với nội dung:

```
    <?php defined('BASEPATH') OR exit('No direct script access allowed');  
    require_once(APPPATH . 'third_party/smarty/libs/Smarty.class.php');  
    class SmartyLibrary extends Smarty {  
       function __construct() {  
          parent::__construct();  
          // Define directories, used by Smarty:  
          $this->setTemplateDir(APPPATH . 'views');  
          $this->setCompileDir(APPPATH . 'cache/smarty_templates_cache');  
          $this->setCacheDir(APPPATH . 'cache/smarty_cache');  
       }  
    }
```
+ Bước 4: Truy cập application\config\autoload.php và cấu hình libraries:
``` $autoload['libraries'] = array('SmartyLibrary' => 'smarty'); ```
---
### Ghi chú

**Đã bao gồm chức năng ghi LOG khi tác động vào database**

*system/database/DB_driver.php (Hàm query)*

```
	if($this->is_write_type($sql)) {
		$ci = &get_instance();
		$now = date('m-d-Y H:i:s');
		$date_now = date('m-Y', time());
		$day = date('d', time());
		$user = $ci->session->userdata('username');
		$txt_log = "[". $user . "]" . " - " . $now . " --> " . $sql;
		$directoty = "./LOGS/" . $date_now;
		if(!is_dir($directoty)) {
			mkdir($directoty, 0777, true);
		}
		file_put_contents($directoty . "/log_" . $day . ".txt" ,$txt_log ."\n", FILE_APPEND);
	}
```
