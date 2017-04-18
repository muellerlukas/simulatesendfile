## What is it?
A simple class to fetch mod_xsendfile-headers and provide a alternative with symlinks without big modifying you software.

## What does it do?
Put simply: There is a rewrite method that looks for the Sendfile-headers, creates a symlink and forwards to the symlink instead of sending the Sendfile-headers. It will be registered as shutdown-function. So it is called right before giving control back to the webserver.

## Requirements
Tested with PHP 7.0 and Apache 2.4 on Linux. It _should_ work on PHP 5.3+ but is not tested.
Development started on PHP 7.0, Apache 2.4 and Windows 10. So _maybe_ that could also work. But there were a lot of changes betweet start and now.
And of course: You need the permission to use the symlink() function.

## Usage
Sample code here. Just add it to the beginning of your script (or before exiting the script) and change it to your requirements.
```php
require('xsendfile.class.php');
use mulu\xsendfile;
// set directory for symlinks
if (xsendfile::setLinkDir(__DIR__ . '/symlink/'))
{
	xsendfile::setLinkDirUri('http://localhost/stest/symlink/'); // web path to symlink-dir
	xsendfile::setExpireTime(3600); // symlinks expire in 1h
	xsendfile::register(); // register as shutdown function
	xsendfile::runGBC(); // run the gbc
}`
[...]
// Send file via X-Sendfile here
```

## Other
There is also a wordpress-plugin available tested with Wordpress 4.7.3 and WooCommerce 3.
https://github.com/muellerlukas/simulatesendfile_wordpress