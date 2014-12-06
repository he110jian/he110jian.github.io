---
layout: post
---

<h2>{{ page.title }}</h2>
<p class='meta'>{{ page.date | date_to_string }} - NanJing</p>

---

![](http://www.directitcorp.com/wp-content/uploads/2011/10/windows_server_system_logo.jpg)

### PHP ###
1. php配置 
 - 打开php.ini，查找“extension_dir =”，去掉分号，配置扩展路径。
 - 搜索“windows extension”，把你需要的扩展放开即可。extension=php_gd2.dll extension=php_mbstring.dll extension=php_mcrypt.dll extension=php_mysql.dll extension=php_pdo_mysql.dll。
 - 配置完成后，需要将php.ini拷贝到c：\windows目录下。
 
1. 配置 IIS 使其支持 PHP ：首先必须确定系统中已经正确安装 IIS ，如果没有安装，需要先安装 IIS PHP 支持 CGI 和 ISAPI 两种安装模式，推荐使用 ISAPI 模式。这里只解介绍 ISAPI 模式安装方法。ISAPI 模式安装步骤：
 - 打开“internet信息服务（IIS）管理器”，右击“网站”选择“属性”
 - 选择“ISAPI筛选器”选项卡---“添加”，筛选器名称：php，可执行文件：X:\php\php5isapi.dll 确定。
 - 选择“处理程序映射”，“添加”：X:\php\php5isapi.dll，扩展名：*.php。

### FTP ###
windows server服务器端安装IIS自带的FTP功能，如果防火墙关闭才可以通过FTP正常访问，打开FTP则不能访问，解决办法如下:

 - IIS6：
控制面板 》系统和安全 》Windows 防火墙 》允许的程序”，在“允许另一个程序”中添加 “C:\WINDOWS\system32\inetsrv\inetinfo.exe”这个程序，添加完成即可
 - IIS7：
控制面板 》系统和安全 》Windows 防火墙 》允许的程序”，在“允许另一个程序”中添加 “C:\Windows\System32\svchost.exe”这个程序，添加完成即可

---

