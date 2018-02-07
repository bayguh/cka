# クラスター作成

## 環境
・ GCP環境 <br />
・ Ubuntu Ubuntu 16.04 LTS <br />
・ kubernetes 19.1 <br />

## master
▼ インストールするもの <br />
・ kubernetes 19.1 <br />
&nbsp;&nbsp;&nbsp;&nbsp;- kube-apiserver, kube-controller-manager, kube-scheduler <br />
・ etcd 3.1.10 <br />
・ flannel 0.9.1 <br />


## node
▼ インストールするもの <br />
・ kubernetes 19.1 <br />
&nbsp;&nbsp;&nbsp;&nbsp;- kubelet, kube-proxy <br />
・ Docker 17.03-ce <br />
・ flannel 0.9.1 <br />
・ cni v0.6.0 <br />
