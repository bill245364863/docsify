# 工具使用

## MinIO Client
>MinIO Client (mc) 提供minio图片迁移能力

### mc使用
#### 查看连接

`Mc alias list`

#### 删除连接

`mc alias remove myminio`

#### 文件导出

1、添加 minio 连接服务的 别名

`mc alias set minio68 http://10.30.49.68:19000 minio minio123`

2、导出 minio

`mc mirror minio68/moonupload/230511182309191451360007 /data/230511182309191451360007`

#### 文件导入

1、添加 minio 连接服务的 别名

`mc alias set minio67 http://10.30.49.67:19000 minio minio123`

2、导入 minio

`mc cp --recursive /data/230511182309191451360007 minio67/moonUpload/`

#### 将桶导出导其他存储

`mc mirror myminio/<bucket_name> otherminio/<bucket_name>`

---

## elasticdump

>elasticdump提供elasticsearch数据索引迁移能力

`–input: 源地址，可为ES集群URL、文件或stdin,可指定索引，格式为：{protocol}://{host}:{port}/{index} –input-index: 源 ES 集群中的索引`

`–output: 目标地址，可为 ES 集群地址 URL、文件或 stdout，可指定索引，格式为：{protocol}://{host}:{port}/{index} –output-index: 目标 ES 集群的索引`

`–type: 迁移类型，默认为 data，表明只迁移数据，可选 settings, analyzer, data, mapping, alias –limit：每次向目标ES集群写入数据的条数，不可设置的过大，以免bulk队列写满`

更多操作内容查看 `elasticdump --help`

### 导出setting
`elasticdump --input=http://192.168.33.xxx:9200/myindex --output=/data/myindex_settings.json --type=settings`
### 导出mapping
`elasticdump --input=http://192.168.33.xxx:9200/myindex --output=/data/myindex_mapping.json --type=mapping`
### 导出data
`elasticdump --input=http://192.168.33.xxx:9200/myindex --output=/data/myindex_data.json --type=data`

!>先将索引的settings先迁移，如果直接迁移mapping或者data将失去原有集群中索引的配置信息如分片数量和副本数量等
### 迁到另一个集群,其它操作类同
`elasticdump --input=http://192.168.33.xxx:9200/myindex --output=http://192.168.33.yyy:9200/myindex --type=settings`

### 迁到所有集群
!>此操作并不能迁移索引的配置如分片数和副本数(必须对每个索引单独进行配置的迁移)，或者直接在目标集群中将索引创建完毕后再迁移数据

`elasticdump --input=http://A:9200 --output=http://B:9200`

### 导入数据 limit参数不宜过大
`elasticdump --input=/data/myindex_data.json --output=http://192.168.33.29:9200/myindex --limit 2000`

---

## Docker基础命令
>docker操作的简单基础命令

### 容器生命周期管理

run - 创建并启动一个新的容器。  
start/stop/restart - 这些命令主要用于启动、停止和重启容器。  
kill - 立即终止一个或多个正在运行的容器  
rm - 于删除一个或多个已经停止的容器。  
pause/unpause - 暂停和恢复容器中的所有进程。  
create - 创建一个新的容器，但不会启动它。  
exec - 在运行中的容器内执行一个新的命令。  
rename - 重命名容器。  

### 容器操作

ps - 列出 Docker 容器  
inspect - 获取 Docker 对象（容器、镜像、卷、网络等）的详细信息。  
top - 显示指定容器中的正在运行的进程。  
attach - 允许用户附加到正在运行的容器并与其交互。  
events - 获取 Docker 守护进程生成的事件。  
logs - 获取和查看容器的日志输出。  
wait - 允许用户等待容器停止并获取其退出代码。  
export - 将容器的文件系统导出为 tar 归档文件。  
port - 显示容器的端口映射信息。  
stats - 实时显示 Docker 容器的资源使用情况。  
update - 更新 Docker 容器的资源限制，包括内存、CPU 等。  
容器的root文件系统（rootfs）命令  
commit - 允许用户将容器的当前状态保存为新的 Docker 镜像。  
cp - 用于在容器和宿主机之间复制文件或目录。  
diff - 显示 Docker 容器文件系统的变更。  
### 镜像仓库
login/logout - 管理 Docker 客户端与 Docker 注册表的身份验证。  
pull - 从 Docker 注册表（例如 Docker Hub）中拉取（下载）镜像到本地。  
push - 将本地构建的 Docker 镜像推送（上传）到 Docker 注册表（如 Docker Hub 或私有注册表）。  
search - 用于在 Docker Hub 或其他注册表中搜索镜像。  
### 本地镜像管理
images - 列出本地的 Docker 镜像。  
rmi - 删除不再需要的镜像。  
tag - 创建本地镜像的别名（tag）。  
build - 从 Dockerfile 构建 Docker 镜像。  
history - 查看指定镜像的历史层信息。  
save - 将一个或多个 Docker 镜像保存到一个 tar 归档文件中。  
load - 从由 docker save 命令生成的 tar 文件中加载 Docker 镜像。  
import - 从一个 tar 文件或 URL 导入容器快照，从而创建一个新的 Docker 镜像。  
### info|version
info - 显示 Docker 的系统级信息，包括当前的镜像和容器数量。  
version - 显示 Docker 客户端和服务端的版本信息。  
### Docker Compose
docker compose run - 启动一个新容器并运行一个特定的应用程序。  
docker compose rm - 启动一个新容器并删除一个特定的应用程序。  
docker compose ps - 从 docker compose 检查 docker 容器状态。  
docker compose build - 构建 docker compose 文件。  
docker compose up - 运行 docker compose 文件。  
docker compose ls - 列出 docker compose 服务。  
docker compose start - 启动 docker compose 文件创建的容器。  
docker compose restart - 重启 docker compose 文件创建的容器。  
### 网络命令
docker network ls: 列出所有网络。  
docker network create <network>: 创建一个新的网络。  
docker network rm <network>: 删除指定的网络。  
docker network connect <network> <container>: 连接容器到网络。  
docker network disconnect <network> <container>: 断开容器与网络的连接。  
详细内容查看：docker network --help 命令  

### 卷命令
docker volume ls: 列出所有卷。  
docker volume create <volume>: 创建一个新的卷。  
docker volume rm <volume>: 删除指定的卷。  
docker volume inspect <volume>: 显示卷的详细信息。  

