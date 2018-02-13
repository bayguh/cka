# [WIP うごかない]DNS設定

GitHub<br />
https://github.com/kubernetes/kubernetes/tree/master/cluster/addons/dns


## kubeletのオプション設定(node側)
```
--cluster-dns=10.0.0.254 --cluster-domain=cluster.local
```

---

## kube-dns作成
```
sed -i 's|__PILLAR__DNS__SERVER__|10.0.0.254|g' kube-dns.yaml
sed -i 's|__PILLAR__DNS__DOMAIN__|cluster.local|g' kube-dns.yaml
kubectl apply -f kube-dns.yaml
```
