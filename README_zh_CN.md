# phpdock

<p align="center">⛵<code>phpdock</code> 是一个使用docker构建PHP环境的工具, 通过它你很方便的可以打造相同PHP环境，不管是本地开发，还是测试环境，还是生产环境</p>


## 说明

让我们看看使用docker来安装PHP,nginx,MySQL,Redis和Composer是怎样的丝滑

1 - 下载 phpdock 到你的php项目同级:

```
git clone https://github.com/ibiteam/phpdock.git
```

2 - 进入phpdock 并设置配置文件:

```
cd phpdock
cp .env.example .env
cp docker-compose-example.yml docker-compose.yml
```

3 - 启动容器:

```
docker-compose up -d nginx mysql php redis
```

等镜像下载下来并启动了容器，你将看到如下的服务在运行

![phpdock](./files/2022-08-26_15-23.png)


## 重启nginx
```
docker-compose restart nginx
```

## 运行`composer install` 
* 示例假设phpdock同级有一个`laravel`的文件夹
```
docker-compose exec -T php bash -c "cd laravel && composer install --no-dev"
```
* tips:本地文件都映射进容器的`/var/www`

# 文档

### .env.example
* 设置redis密码
```
REDIS_PASSWORD=123456
```

* 设置mysql数据库名称
```
MYSQL_DATABASE=phpdock
```

* 设置mysql数据库root密码
```
MYSQL_ROOT_PASSWORD=phpdock
```

* 设置mysql数据库数据保存路径
```
MYSQL_DATA_PATH=./data/mysql
```

* 设置rabbitmq默认的vhost
```
RABBITMQ_DEFAULT_VHOST=phpdock
```

* 设置rabbitmq登录的用户名
```
RABBITMQ_DEFAULT_USER=phpdock
```

* 设置rabbitmq登录的密码
```
RABBITMQ_DEFAULT_PASS=phpdock
```

* 设置php的版本，可选的有[72 , 74 , 81]
```
PHP_VERSION=74
```

* 设置php扩展的路径
```
PHP_EXTENSION_DIR=/usr/local/lib/php/extensions/no-debug-non-zts-20190902
```

* 设置nginx配置文件的目录，如`local`,`test`,`production`等，或者你可以根据你自己的需要进行定义
```
NGINX_CONF_DIR=local
```

* 设置时区
```
TIME_ZONE=Asia/Shanghai
```

### 文件目录

```
cron      # 运行定时任务，更多的文档可以查看 `ofelia`,`config.ini.example`是一个示例
data      # mysql和redis数据保存的路径
logs      # nginx和redis日志保存的路径
mysql     # mysql镜像的配置
nginx     # nginx站点配置信息，`production`文件下的配置文件是被忽略的，需要手动进行编辑
php-fmp   # 不同版本PHP镜像构建的文件
redis     # redis配置文件
```
