# k8s学习

## 1.环境

windows下的kubernetes

开启Hyper - V

安装Docker Desktop  [Docker 官方下载页面](https://www.docker.com/products/docker - desktop)

**开启 Kubernetes**：打开 Docker Desktop，在系统托盘中右键单击 Docker 图标，选择 “Settings” -> “Kubernetes”，勾选 “Enable Kubernetes”，点击 “Apply & Restart”，等待 Kubernetes 启动。

## 2.安装 kubectl

- **下载**：访问 [kubectl 官方下载页面](https://kubernetes.io/docs/tasks/tools/install - kubectl - windows/)，下载适用于 Windows 的 kubectl 可执行文件。
- **配置环境变量**：将下载的 kubectl 可执行文件所在目录添加到系统的环境变量`PATH`中。
- **验证安装**：打开 PowerShell 或命令提示符，输入以下命令验证 kubectl 是否安装成功：

```powershell
kubectl version --client
```

## 3.k8s概念

- **Pod**：Kubernetes 中最小的可部署单元，一个 Pod 可以包含一个或多个紧密相关的容器。
- **Node**：是 Kubernetes 集群中的工作节点，负责运行 Pod。
- **Deployment**：用于管理 Pod 的副本，确保指定数量的 Pod 副本始终运行。
- **Service**：为一组 Pod 提供统一的访问入口，实现负载均衡。

## 4.基本操作

创建 Deployment 和 Service

- 创建一个名为`nginx-deployment.yaml`的文件，内容如下：

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

此文件定义了一个包含 3 个 Nginx 容器副本的 Deployment。

- 使用 kubectl 创建 Deployment：

```powershell
kubectl apply -f nginx-deployment.yaml
```

- 创建一个名为`nginx-service.yaml`的文件，内容如下：

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: LoadBalancer
```

此文件定义了一个用于访问 Nginx Deployment 的 Service。

- 使用 kubectl 创建 Service：

```powershell
kubectl apply -f nginx-service.yaml
```

## 5.资源命令

查看资源命令

```powershell
# 查看所有Deployment
kubectl get deployments
# 查看所有Service
kubectl get services
# 查看所有Pod
kubectl get pods
```

删除资源

```powershell
kubectl delete deployment nginx-deployment
kubectl delete service nginx-service
```

