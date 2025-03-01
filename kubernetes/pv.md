# 8.4.6 Pod 容器持久化存储

容器服务通常被设计成无状态的，每个容器都可以随意启停，并被可被编排到不同节点，但传统的应用都是携带数据状态，并且还有一些容器需要共享数据，此时就需要容器挂载外部存储。对于这种这种情况 ，Kubernetes 引入了 PV（Persistent Volume，PV）和 PVC（Persistent Volume Claim， PVC）实现数据持久化的存储。

PV 是外部存储系统的一块存储空间，可以是一个本地存储路径，也可以是一个 ceph、gluster 类型的分布式文件系统，它具有持久性，其生命周期独立于 Pod。

PVC 是对 PV 的申请。需要为用户增加存储资源时，用户可以根据储需求创建一个 PVC，Kubernetes 会根据 PVC 的筛选条件匹配合适的 PV 绑定。

PVC 是 Kubernetes 提供的一种抽象层，PVC 解除了 Pod 同具体存储之间的耦合，向用户屏蔽了具体存储的实现形式。用户只需要告诉 Kubernetes 需要什么样的存储资源。而不用关心存储系统的底层细节。