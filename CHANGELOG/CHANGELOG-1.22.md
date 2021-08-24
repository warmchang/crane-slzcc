- [v1.22](#v122)
  - [Updated Instructions](#updated-instructions)
    - [v1.22.0.0 更新内容](#v12200)
    - [v1.22.1.0 更新内容](#v12210)
    - [v1.22.1.1 更新内容](#v12211)

# v1.22.0.0

Crane 以更新至 1.22.0.0 版本。

更新组件版本:
 * pause:      3.5
 * coredns:    1.8.4
 * cni:        v0.9.1
 * etcd:       3.4.9
 * calico:     v3.20.0
 * cilium:     v1.10.3
 * containerd: 1.5.5
 * cri_tools:  v1.22.0
 * crio:       v1.21.2
 * docker:     20.10.8
 * haproxy:    2.4.2

[Kubernetes](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.22.md) 1.22.0 版本官方更新说明.

# v1.22.1.0

Crane 以更新至 1.22.1.0 版本。

# v1.22.1.1

拆分 k8s_addons 到 k8s_addons.yml 中, 不在放入默认 main.yml 文件中。

修改 `rbac.authorization.k8s.io/v1beta1` 为 `rbac.authorization.k8s.io/v1` 。