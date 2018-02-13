## [WIP うごかない]auth設定

公式ページ<br />
https://kubernetes.io/docs/admin/authentication/<br />

---

## ssl設定

```
mkdir /etc/kubernetes/ssl

openssl req -newkey rsa:2048 -nodes -sha256 \
              -keyout /etc/kubernetes/ssl/apiserver.key \
              -x509 -days 356 \
              -out /etc/kubernetes/ssl/apiserver.crt \
              -subj "/CN=[master IP]"
```

```
# apiserverオプションの追加
--bind-address=0.0.0.0 --secure-port=6443 --tls-cert-file=/etc/kubernetes/ssl/apiserver.crt --tls-private-key-file=/etc/kubernetes/ssl/apiserver.key

# controller-managerオプションの追加
--root-ca-file=/etc/kubernetes/ssl/apiserver.crt

# kubeletオプションの追加
--tls-cert-file=/etc/kubernetes/ssl/apiserver.crt --tls-private-key-file=/etc/kubernetes/ssl/apiserver.key
```
※ --insecureな設定は認証を行わない
