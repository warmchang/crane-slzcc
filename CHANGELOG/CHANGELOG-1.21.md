- [v1.21](#v121)
  - [Updated Instructions](#updated-instructions)
    - [v1.21.0.0 更新内容](#v12100)
    - [v1.21.0.1 更新内容](#v12101)
    - [v1.21.1.0 更新内容](#v12110)
    - [v1.21.1.1 更新内容](#v12111)
    - [v1.21.1.2 更新内容](#v12112)

# v1.21.0.0

Crane 以更新至 1.21.0.0 版本。

更新组件版本:
 * coredns:    1.8.3
 * cni:        v0.9.1
 * etcd:       3.4.9
 * calico:     v3.18.1
 * containerd: 1.4.4
 * cri_tools:  v1.21.0
 * crio:       v1.20.2
 * docker:     20.10.5
 * haproxy:    2.3.9

[Kubernetes](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.21.md) 1.21.0 版本官方更新说明.


# v1.21.0.1

dockerd 删除 aliyun 的加速器配置, 因 aliyun 加速器存在超时的问题。


# v1.21.1.0

Crane 以更新至 1.21.0.0 版本。

# v1.21.1.1

## 修复

修复 etcd Backup 时, 备份文件丢失的问题。

修复 calico 网络在通过 `upgrade_version.yml` 时执行删除顺序的报错。

关闭 `upgrade_version.yml` 中自动关闭集群 `node` 节点的调度, 移除独立操作文件 `k8s_setup_close_schedule.yml` 和 `k8s_setup_open_schedule.yml`, 提倡人为执行。

修复 Makefile 不下载 crictl 工具问题。

修复如不想默认安装 cri 时, 还会安装 runC 和 crictl 的问题。

修复添加或删除节点时, labels 不会变更的问题。

修复添加 node 节点时, 无法找到 cri-tools 版本的问题。

## 新增

`k8s_setup_close_schedule.yml` 关机集群 `node` 节点调度。

`k8s_setup_open_schedule.yml` 开启集群 `node` 节点调度。

> 上述功能主要是人为维护集群时手动批量操作功能。

`etcd_backup_cluster.yml` 备份当前 `etcd` 集群, 备份文件默认在第一个 `etcd` 节点的 `/tmp/crane/etcdb` 中。

`etcd_new_cluster.yml` 新建一组 `etcd` 集群通过 `nodes` 文件中的 `[etcd-del-cluster]` 适配。

`etcd_restore_cluster.yml` 新建一组 `etcd` 集群通过 `nodes` 文件中的 `[etcd-new-cluster]` 适配, 

并且支持指定文件恢复, 可通过 `roles/etcd-cluster-management/defaults/etcd-new-cluster.yaml` 配置支持 `http` 和本地文件方式进行恢复。

`migration_k8s_to_new_etcd_cluster.yml` 让 apiServer 服务指向指定的新 `etcd` 集群, 通过 `[etcd-new-cluster]` 适配。

`remove_etcd_cluster.yml` 删除指定的 `etcd` 集群数据及配置, 不要与 `remove_etcd_nodes.yml` 混淆, `remove_etcd_nodes.yml` 主要是移除集群中的一个或多个节点, `remove_etcd_cluster.yml` 是删除一整组集群。

> 上述功能主要操作 etcd。

`remove_k8s_master.yml` 对 `master` 节点降级为 `node` 节点, 并同步 `haproxy` 配置信息。

# v1.21.1.2

## 修复

修复 `upgrade version` 过程中先 `kube-proxy` 先删除在启动的逻辑, 改成升级策略。

修复 `calico` 3.18.x 版本初始安装时, `CRD` 不全的问题。

修复 `remove cluster` 中 `calico` 配置残留的问题。

修复 `calico` 默认为 `IPIP` 模式, 因绝大多数纯 `BGP` 模式无法正常启动。

## 新增

升级 `kube-proxy` 之前会先备份集群中的 `kube-proxy`。