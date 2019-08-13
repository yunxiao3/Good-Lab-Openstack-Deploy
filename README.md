## NCU Good 实验室openstack部署

这学期对虚拟化技术很感兴趣，刚好实验室有一个小的集群，虽然最近docker技术非常火，但考虑到学院很多师生对命令行并不熟悉，所以选择了openstack虚拟化实验室的集群，使得可以为用户提供Windows环境和图形界面。最近实验买了很多GPU： 8块 tesla v100和一台DGX-STATION，但是对于GPU的虚拟化部分还不是很熟悉，有时间将会尝试虚拟化实验室GPU。

整理仓促，有时间我将会openstack的搭建过程整理上传，对openstack感兴趣的朋友可以参照（<https://www.openstack.org/>）进行部署使用

####　物理架构图

![1565714719822](/home/jakcdu/GitHub/Good-Lab-Openstack-Deploy/img/1565714719822.png)  

#### openstack架构图

![1565714865857](/home/jakcdu/GitHub/Good-Lab-Openstack-Deploy/img/1565714865857.png)

集群有一个控制节点和多个计算节点，同时控制节点也承担的计算节点的角色。控制节点的网卡一(eno1)接入外网，提供neutron网络的物理接口,网卡二(eno2)作为内网的管理网卡。整个结构充分的利用了物理资源，实现了一个简单的OpenStack集群。为了使内网的机器可以访问外网，我们将控制节点网卡二(eno2)的流量转发到网卡一(eno1)以网卡二的地址作为内部机器的网关。