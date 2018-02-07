# master作成

## 各ファイルの配置場所
・ 作業ディレクトリ -> /root <br />
・ configファイル -> /etc/kubernetes <br />
・ binファイル -> /uer/local/bin <br />
・ systemdファイル -> /etc/systemd/system <br />

## 初期設定

### 関連パッケージのインストール
```
apt-get update
apt-get install -y build-essential linux-libc-dev bridge-utils git curl ssh unzip golang tmux
```

### ホスト名登録
```
sh -c "echo '[master IP] kube-master' >> /etc/hosts"
sh -c "echo '[node1 IP] kube-node1' >> /etc/hosts"
sh -c "echo '[node2 IP] kube-node2' >> /etc/hosts"
```

### ディレクトリ作成
```
mkdir -p /root/.kube
touch /root/.kube/config
mkdir -p /etc/kubernetes
mkdir -p /var/lib/etcd
```

### ファイルの配置
・ config以下の各コンポーネントの設定ファイルを/etc/kubernetes配下に配置 <br />
・ service以下のファイルを/etc/systemd/system配下に配置

---

## Kubernetesインストール
```
wget https://storage.googleapis.com/kubernetes-release/release/v1.9.1/kubernetes.tar.gz
tar xzvf kubernetes.tar.gz

sh -c kubernetes/cluster/get-kube-binaries.sh
tar xzvf kubernetes/server/kubernetes-server-linux-amd64.tar.gz

ln -s /root/kubernetes/server/bin/kube-apiserver /usr/local/bin/
ln -s /root/kubernetes/server/bin/kube-controller-manager /usr/local/bin/
ln -s /root/kubernetes/server/bin/kube-scheduler /usr/local/bin/
ln -s /root/kubernetes/server/bin/kubectl /usr/local/bin/
```

---

## etcdインストール
```
wget https://github.com/coreos/etcd/releases/download/v3.1.10/etcd-v3.1.10-linux-amd64.tar.gz
tar xzvf etcd-v3.1.10-linux-amd64.tar.gz

ln -s /root/etcd-v3.1.10-linux-amd64/etcd /usr/local/bin/
ln -s /root/etcd-v3.1.10-linux-amd64/etcdctl /usr/local/bin/
```

---

## flannelインストール
```
wget https://github.com/coreos/flannel/releases/download/v0.9.1/flanneld-amd64
chmod 755 flanneld-amd64
ln -s /root/flanneld-amd64 /usr/local/bin/flanneld
```

---

### サービスの起動

▼ 自動起動設定
```
systemctl enable etcd
systemctl enable flanneld
systemctl enable kube-apiserver
systemctl enable kube-controller-manager
systemctl enable kube-scheduler

# 確認
systemctl list-unit-files -t service
```

▼ 起動
```
systemctl start etcd
etcdctl mk /test.io/network/config '{"Network":"10.0.0.0/16"}'

systemctl start flanneld
systemctl start kube-apiserver
systemctl start kube-controller-manager
systemctl start kube-scheduler
```

---

### etcd接続確認
```
curl -s -L http://127.0.0.1:2379/version
```

### プロセスのLISTEN確認
```
netstat -tulnp | grep -E "(kube)|(etcd)"
```

### logの確認方法
```
systemctl status etcd.service | less
systemctl status flanneld.service | less
systemctl status kube-apiserver.service | less
systemctl status kube-scheduler.service | less
systemctl status kube-controller-manager.service | less

journalctl -xe | less

journalctl -xe --unit etcd
journalctl -xe --unit flanneld
journalctl -xe --unit kube-apiserver
journalctl -xe --unit kube-scheduler
journalctl -xe --unit kube-controller-manager
```

---

### clusterへ接続

```
kubectl config set-cluster test-cluster --server=http://[master hostname]:8080
kubectl config set-credentials admin --username=admin --password=admin
kubectl config set-context test --cluster=test-cluster --user=admin
kubectl config use-context test
```
