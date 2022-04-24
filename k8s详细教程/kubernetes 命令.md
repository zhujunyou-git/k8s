### 命令
关闭防火墙-selinux   selinux=disabled    sed -ri 's/SELINUX=enforcing/SELINUX=disabled/' /etc/selinux/config
时间同步 netdate ntp机器ip
关闭机器swap分区  free -h 查看  注释/etc/fstab文件

pod节点控制器
svc服务发现
pv

安装docker 
获取集群 kubectl get nodes
查看健康状态  kubectl get cs
查看集群运行在那个机器上的 kubectl cluster-info

kubectl客户端工具
get nodes
-n 命名空间

yaml文件学习
1对象 键值对
 映射 哈希  字典 
name:new
hash :{name:new,age:28}

2数组
new
- 男的
- 28
new:[男的,28]

3纯量 单个的值
数值
number:28.11
布尔
isSet:true
null 用~表索
parent:~
时间才有IOS8601格式
!!两个感叹号强转数据类型
a:!!str 123
字符串不需要引号
特殊字符需要放在引号中
转义引号的话用2个引号

常用字段
version  k8sapi的版本 可以使用kubectl api-cersion查看
kind 定义资源类型比如pod
metadata 元数据对象固定值写metadata
metadata.name 元数据对象的名字 比如pod的名字
metadata.namespace 命令空间
Spec 对象的详细描述
Spec.containers[]容器列表定义
spec.containers[]name 容器名称
spec.containers[]image 容器镜像

namespace学习
查看namespace 
kubectl get namespace 
kubectl get ns
创建namespace
kubectl create namespace  new
kubectl apply -f new.yaml
删除namespace
kubectl delete namespace new
kubectl delete -f new.yaml

最小调用单元pod
查看pod
kubectl get pod 查看default命名空间里面的pod
kind:Pod
metadata:
 name:pod1
spec:
 containers:
 - name:nginx-pod
   image:nginx:latest
   ports:
   - name:nginxport
      containerPort:80
pod跟namespace操作类似    pod是容器

Controller
kubectl get deployments.apps   查看deploy的控制器启动的pod
监控pod 会重新拉起
用控制器启动的话不能直接删除pod
需要删除的话需要删除控制器里面的pod
kubectl -n coding-ide get pod,ds,deployment
查看pod守护进程是控制器启动的还是守护进程启动的
删除deployment的话会自动删除pod
kubecl -n coding-ide delete deployment cs-apiserver

describe 看看具体信息
kubectl -n coding-ide describe pod cs-apiserver-74d6798768-bzqhv

service 
作为一种转发服务
pod可以直接访问  但是不建议  通过service
kubectl expose 暴露pod 可以转发端口
kubectl get service  查看service
kubectl get svc
kubectl get endpoints  查看端点  查看关联关系

kubectl exec -it pod sh  进入pod
kubectl get pod -o wide 查看物理网卡
kubectl get svc 查看虚拟地址

给机器打标签
kubectl label nodes 10.21.3.6 10.21.3.5 10.21.3.13 type_name=datatalk
kubectl get node --show-labels
修改pod部署文件加上
      nodeSelector:
        type_name: datatalk
