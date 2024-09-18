# Xdebug setup in VS code for Linux
Open terminal from processmaker folder

### Step 1: Install xdebug

```
sudo apt-get install php-xdebug
```

### Step 2: Configure PHP with Xdebug
After installing Xdebug, you need to configure PHP to use it. Edit your `php.ini` file (location varies by system; you can find it by running `php --ini`)

Or you can use CLI to open the `php.ini` file:
```
sudo nano /etc/php/8.3/cli/php.ini
```
Add the following lines to php.ini:
```
[xdebug]
xdebug.mode=debug
xdebug.start_with_request=yes
xdebug.client_host=127.0.0.1
xdebug.client_port=9003
```
Save and close the file (in nano, press `Ctrl+X`, then `Y`, and `Enter`).

### Step 3: Restart Your Web Server
If you are using `apache`
```
sudo systemctl restart apache2
```
Or if you are using `Nginx` with `PHP-FPM`:
```
sudo systemctl restart php-fpm
sudo systemctl restart nginx
```

### Step 4: Verify Xdebug is Enabled
To ensure Xdebug is correctly enabled, create a PHP script called `xdebug_info.php` in your root folder and add:
```
<?php
phpinfo();
?>
```
Run this script from the CLI:
```
php xdebug_info.php
```
Look for Xdebug in the output. If it’s correctly configured, you should see information about Xdebug.

### Step 5: Install PHP Debug Extension in VS Code
Open VS code extension and search for `PHP Debug` and install the extension by `Xdebug`.

1. Open your PHP project in VS Code.

2. Open the Run view by clicking the play icon in the sidebar or pressing Ctrl+Shift+D.

3. Click on `create a launch.json file` link.
Select PHP from the list of configurations.(If asked you to do so)

This will create a launch.json file with the following content:
```
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Listen for Xdebug",
            "type": "php",
            "request": "launch",
            "port": 9003
        }
    ]
}
```

### Step 6: Start Debugging

1. Set breakpoints in your PHP code.

2. In the Run and Debug view, select "Listen for Xdebug" and click the green play button.

3. Run your PHP script or load it in your web browser.

### Tips
Include below line in php.ini to avoid xdebug warning
```
xdebug.log_level=0
```
