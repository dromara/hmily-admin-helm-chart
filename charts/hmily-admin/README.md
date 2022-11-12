# hmily-admin-helm-chart

A helm chart for hmily-admin.

## 添加 Helm 仓库

```shell
helm repo add hmily-admin https://dromara.github.io/hmily-admin-helm-chart
helm repo update
```

### 说明

* **服务暴露**：使用 NodePort 暴露服务，admin 默认端口为 `31095`, bootstrap 为 `31195`。
* **数据库**：目前支持 MySQL 作为数据库。

### 安装

修改以下命令并复制，执行：

```shell
helm install hmily-admin hmily-admin/hmily-admin -n=hmily --create-namespace \
      --set dataSource.active=mysql \
      --set dataSource.mysql.ip=127.0.0.1 \
      --set dataSource.mysql.port=3306 \
      --set dataSource.mysql.username=root \
      --set dataSource.mysql.password=123456 \
      --set dataSource.mysql.database=hmily
```

运行成功后，输出的最后会有 `NOTES`，会给出访问服务的命令。

### 若需要大量修改配置信息，如何安装

1. 下载完整 values.yaml
* 最新 chart 版本：`helm show values hmily-admin/hmily-admin > values.yaml`
* 特定 chart 版本, 如 `0.1.0`: `helm show values hmily-admin/hmily-admin --version=0.1.0 > values.yaml`
2. 修改 values.yaml 文件
3. 更改相应配置，使用 `-f values.yaml` 的格式执行 `helm install` 命令。
   如：`helm install hmily-admin hmily-admin/hmily-admin -n=hmily --create-namespace -f values.yaml`

## Values

| 配置项                                        | 类型    | 默认值                 | 描述                                                       |
|----------------------------------------------|--------|-----------------------|----------------------------------------------------------|
| replicaCount                                 | int    | 1                     | 副本数量                                                     |
| image.repository                             | string | "dromara/hmily-admin" | 镜像地址                                                     |
| image.pullPolicy                             | string | "IfNotPresent"        | 镜像拉取策略                                                   |
| image.tag                                    | string | "1.0.2"               | 镜像版本                                                     |
| service.type                                 | string | "ClusterIP"           | Kubernetes Service 类型，支持 NodePort，ClusterIP，LoadBalancer |
| service.port                                 | int    | 31888                 | Kubernetes Service 端口                                    |
| applicationConfig.server.servlet.contextPath | string | ""                    | hmily-admin contextPath                                  |
| applicationConfig.hmily.admin.userName       | string | "admin"               | hmily-admin 默认用户名                                        |
| applicationConfig.hmily.admin.password       | string | "admin"               | hmily-admin 默认密码                                         |


