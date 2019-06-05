<h1>蛋壳本地开发环境搭建</h1>
<h3>*** 目前为初版可能会遇到各种问题，希望大家加入进来一起完善 ***</h3>
<h3>首先确保你的电脑已经安装了docker环境</h3>

可以查看一下 MAC 安装 docker 环境的方法 <a href="https://www.jianshu.com/p/9142187552db">https://www.jianshu.com/p/9142187552db</a>


<h3>第一步拉取镜像文件</h3>

```bash
docker pull registry.cn-beijing.aliyuncs.com/aliyun-php/danke_php72
```

<h3>第二步运行docker 容器</h3>

```bash 
docker run --restart always --name php7.2  -p 80:80 -v /danke/:/var/www/ -itd  php7.2:latest
```

	--restart always 容器自动重启
	
	--name 是容器名称随意定
	
	-p 80:80 指定本地80端口指向容器的80端口 （如果本地有80端口被占用先停掉本地80端口）
	
	-v /danke/:/var/www/  将本地 /danke/ 目录挂载到 容器的/var/www/目录下 （本地目录根据自己项目位置自定义）

<h3>第三步定义本地 hosts文件</h3>

127.0.0.1 dev.test.laputa.com

127.0.0.1 dev.test.crm_feedback.com	

	默认容器里有2个nginx conf文件  分别是laputa 和 crm_feedback项目的
	
	config文件自己可以根据自己需求随意更改


<h3>进入容器 执行 composer update -vvv </h3>

```bash docker exec -it php7.2 bash```


	如果已经执行过，无需在执行
	cd /var/www/项目目录
	composer update -vvv


<h3>最后一步</h3>
打开浏览器 访问 dev.test.crm_feedback.com 或者	dev.test.laputa.com

如果能正常访问则恭喜你环境搭建成功！	

<h3>【注意】 在本地增加Class或者引入新的Composer包后都推荐执行一次</h3>

```bash 

composer dumpautoload; php artisan clear-compiled; php artisan ide-helper:generate -M; php artisan ide-helper:models -n; php artisan optimize;

```


