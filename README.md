Mike Magic Tools
====================
2016-02-01




This is a set of various tools.



MikeMagicTools can be installed as a [planet](https://github.com/lingtalfi/Observer/blob/master/article/article.planetReference.eng.md).


File section
-------------------

- prepender: prepend some string for every file in the given file set
- remove x first lines: remove the first x lines for every file in the given file set
- reduce consecutive end of lines: reduce consecutive end of lines to one single end of line for every file in the given file set
- free hand tool: use this tool to freely modify the content of every file in the given file set, using a callback




How to use
-------------


### prepender tool 

Here is how to use the prepend tool, 
I needed it once because I wanted to test the order in which my js files were called,
so so I needed to prepend every js file with a "console.log ( 'file $xx loaded' );" statement.


```php
<?php


use DirScanner\YorgDirScannerTool;
use MikeMagicTools\File\MikeFilePreprenderTool;

require_once "bigbang.php"; // start the local universe




$prependix = function ($file) {
    return "console.log('" . basename($file) . " lib');" . PHP_EOL;
};



$dir = "/path/to/my/app/www/libs";
$files = YorgDirScannerTool::getFilesWithExtension($dir, 'js', false, true);
MikeFilePreprenderTool::prependFiles($files, $prependix);


```


### remove first x lines tool 

You might need this if you've used the prepender tool for debug purposes.
Then use this tool to go back to the original files' state.


```php
<?php


use DirScanner\YorgDirScannerTool;
use MikeMagicTools\File\MikeFileRemoveFirstXLinesTool;

require_once "bigbang.php"; // start the local universe




$prependix = function ($file) {
    return "console.log('" . basename($file) . " lib');" . PHP_EOL;
};



$dir = "/path/to/my/app/www/libs";
$files = YorgDirScannerTool::getFilesWithExtension($dir, 'js', false, true);
MikeFileRemoveFirstXLinesTool::removeFirstXLines(1, $files);


```







What if something goes wrong with the File tools?
-------------------------------------

Every Mike Magic file tool uses the Mike magic's FreeHandTool under the hood.
The reason for this is that the free hand tool automatically creates a copy of the file set (unless
you tell it specifically to not do so).

So, if for some reason you accidentally blow a set of files away, you can try to go to the 
free hand tool's trash directory and see if you can backup your original files from there.
Beware that the trash only saves one state and overwrites itself if necessary, so don't go too fast.

For more info, please browse the source code's comments.





History Log
------------------
    
- 1.0.0 -- 2016-02-01

    - initial commit
    
    