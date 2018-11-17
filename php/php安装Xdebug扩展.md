# php安装Xdebug扩展

1. 下载源码: `curl https://xdebug.org/files/xdebug-2.6.1.tgz`

2. 解压:`tar -zxf xdebug-2.6.1.tgz`

3. `cd xdebug-2.6.1`

4. `phpize`

5. `./configure --with-php-config=/usr/local/php/bin/php-config`

6. 编译：`make`

7. 安装：`make install`

8. 加载Xdebug模块:`zend_extension=xdebug.so`

9. 检测是否加载成功:`php -m | grep xdebug`  *如果出现xdebug则表示安装成功*
