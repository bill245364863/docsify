# 部署信息

## 容器服务信息
> 速响部署以docker部署为主，一共有26个容器服务

| 基础路径 | 容器名 | 描述 | 版本 | 路径 | 端口号 | 内存占用 |
|---------------------|-----------------------------------|----------------------|-----------------|-----------------------|---------|-------------|
| /data/anscen | galaxy-standalone-nacos | 提供注册中心与配置中心 | 1.3.0 | /nacos | 8600 | 2G |
| | galaxy-mysql | Mysql 数据存储 | 5.6.8 | /mysql | 3306 | 1G |
| | galaxy-redis | Redis 缓存服务 | 6.2.6 | /redis | 6379 | 1G |
| | galaxy-rabbitmq | 消息队列服务 | 3.12.2| /rabbitmq | 5673/15672 | 1G |
| | galaxy-minio | minio对象文件存储 | DEVELOP.NT.GOET| /minio | 19000 | 2G |
| | galaxy-mongo | Mongo 文档存储 | 4.4.16-r6.0.7| /mongo | 28001 | 2G |
| | galaxy-elasticsearch | Elasticsearch 集群 | 7.0.0 | /es | 9200 | 2G |
| | galaxy-nginx | nginx代理服务（前端） | 1.19.0 | /nginx | 8600 | 2G |
| | galaxy-gateway-web | 网关服务 | 1.0 | /app/galaxy/gateway-web | 8604 | 2G |
| | galaxy-authentication-server | 鉴权服务 | 1.0 | /app/galaxy/authentication-server| 8605 | 3G |
| | galaxy-authorization-server | 授权服务 | 1.0 | /app/galaxy/authorization-server | 8606 | 3G |
| | as-galaxy-portal | 门户服务 | 1.0 | /app/portal | 8630 | 2G |
| | as-moon | 客户端服务 | V1.10.9_073 | /app/moon-release | 8097/8098| 3G |
| | as-mpbd-api-18307 | 提供基础api服务接口 | 1.08.01.0145 | /app/mpbd | 18307 | 1G |
| | as-mpbd-biz-18305 | 提供 biz 服务 | - | - | 18305 | 0.5G |
| | as-mpbd-biz-18306 | 提供 biz 服务 | - | - | 18306 | 0.5G |
| | as-mpbd-task-18111 | 提供 task 服务 | - | - | 18111 | 0.5G |
| | as-mpbd-h2-18251 | h2缓存数据库 | - | - | 18251 | 0.5G |
| | as-jizz-api-8808 | 提供 API 接口服务 | 1.08.12216 | /app/jizz-app | 8808 | 0.5G |
| | as-jizz-api-8807 | 提供 API 接口服务 | - | - | 8807 | 0.5G |
| | as-jizz-api-8806 | 提供 API 接口服务 | - | - | 8806 | 0.5G |
| | as-jizz-file-8820 | 提供文件服务 | - | - | 8820 | 0.5G |
| | as-jizz-nebula-8809 | 极智业务服务 | - | - | 8809 | 2G |
| | as-jizz-task-8810 | 提供任务调度服务 | - | - | 8810 | 2G |
| | as-jizz-task-8811 | 提供任务调度服务 | - | - | 8811 | 2G |
| | as-jizz-third-8816 | 提供第三方集成服务 | - | - | 8816 | 2G |

!> 后端服务路径：`/data/anscen/app `  
 前端部署路径 `/data/anscen/nginx/html`  
 其他版本部署信息，若有疑意可以钉钉联系我


## 应用访问路径

> 平台访问路径


| 应用 | 访问地址 |
|-----|---------|
|nacos|http://ip:8600/nacos|
|星云门户|http://ip:8660/galaxy|
|容器运维|http://ip:18050|
|证书生产|http://ip:8340|
|消息队列|http://ip:15673|
|MINIO对象存储|http://ip:19000|
|kibana|http://ip:5601|

