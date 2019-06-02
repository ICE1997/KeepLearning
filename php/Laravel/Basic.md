# Laravel配置

## 介绍

所有配置文件都被存放在`config`文件夹下。

## 环境配置

Laravel框架的根目录包含一个`.env.example`的文件，如果你通过Composer装的Laravel,那么这个文件将会被自动重命名为`.env`,否则，你需要手动来重命名`.env.example`为`.env`

> Note:当你的项目被类似于GitHub一样代码托管时，请不要commit `.env`文件。
>
> 当你用PHPUnit测试或执行Artisan命令（在命令后添加`--env=testing`）时，创建`.env.testing`文件将会覆盖`.env`文件。
>
> .env中的任何变量都会被外部环境变量覆盖，例如系统级别的环境变量。

### 环境变量类型

`.env`文件中所有的变量都会被解析成字符串类型，所以被保存的值可以通过`env()`这个函数来使得返回更多的类型。对应关系如下：

| `.env` Value | `env()` Value |
| ------------ | ------------- |
| true         | (bool) true   |
| (true)       | (bool) true   |
| false        | (bool) false  |
| (false)      | (bool) false  |
| empty        | (string) ''   |
| (empty)      | (string) ''   |
| null         | (null) null   |
| (null)       | (null) null   |

> 如果你想定义一个名字中包含空格的变量，你需要用双引号将这个变量包起来。

### 获取环境配置

当你接受到一个请求，所有被列在`.env`文件中的变量都将被储存在一个叫`$_ENV`的超级全局变量中。然而，你可能会用`env` helper来从配置文件中获取变量的值。事实上，如果你仔细查看Laravel的配置文件，你就会注意到一些选项已经在使用这个helper,例如：

```php
'debug' => env('APP_DEBUG', false),
```

env函数的第二个值是默认值，如果环境变量没有APP_DEBUG的值，false就会被使用。

### 检测当前环境

当前应用的环境可以通过`.env`中的`APP_ENV`变量来检测，你可能会通过APP facade中的`environment`方法来访问这个值。

```php
$environment = APP::environment();
```

你也可以向`environment`方法中传参量来检测这个环境是否匹配一个值，如果匹配，就会返回`true`.例如：

```php
if (App::environment('local')) {
    // The environment is local
}

if (App::environment(['local', 'staging'])) {
    // The environment is either local OR staging...
}
```

> 当前应用的环境检测可以被Servel级别的`APP_ENV`环境变量覆盖。

### 在Debug页面隐藏环境变量

当开启Debug模式，但一个异常未被捕获时，此时Debug将会显示所有的环境变量以及他们的值。有时你可能想隐藏某个特定的变量，那么，你可以通过更新`config/app.php`文件中的`debug_list`设置来实现。

一些变量在环境变量和server/request数据中都是存在的，因此，你可以为`$_ENV`和`$_SERVER`来为他们建立一个黑名单：例如：

```php
return [

    // ...

    'debug_blacklist' => [
        '_ENV' => [
            'APP_KEY',
            'DB_PASSWORD',
        ],

        '_SERVER' => [
            'APP_KEY',
            'DB_PASSWORD',
        ],

        '_POST' => [
            'password',
        ],
    ],
];
```