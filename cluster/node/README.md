# node作成

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

### ユーザ作成
```
```

### ディレクトリ作成
```
mkdir /var/lib/kubelet
mkdir /etc/kubernetes
```

---

## Kubernetesインストール
```
wget https://storage.googleapis.com/kubernetes-release/release/v1.9.1/kubernetes.tar.gz
tar xzvf kubernetes.tar.gz

sh -c kubernetes/cluster/get-kube-binaries.sh
tar xzvf kubernetes/server/kubernetes-server-linux-amd64.tar.gz

ln -s /root/kubernetes/server/bin/kubelet /usr/local/bin/
ln -s /root/kubernetes/server/bin/kube-proxy /usr/local/bin/
```

---

## dockerのインストール
```
apt-get update
apt-get install -y docker.io

apt-get update
apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
add-apt-repository \
   "deb https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
   $(lsb_release -cs) \
   stable"
apt-get update && apt-get install -y docker-ce=$(apt-cache madison docker-ce | grep 17.03 | head -1 | awk '{print $3}')
```

---

## flannelのインストール
```
wget https://github.com/coreos/flannel/releases/download/v0.9.1/flanneld-amd64
chmod 755 flanneld-amd64
ln -s /root/flanneld-amd64 /usr/local/bin/flanneld
```
