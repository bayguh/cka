# DaemonSet

公式ドキュメント<br />
https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/

---

全nodeに1podずつ配置するリソース<br />
fluentd,Datadogなど、各nodeに配置することが必要なコンポーネントで利用する<br />

---

作成
```
kubectl apply -f daemonset.yml --record
```

確認
```
kubectl get daemonset(ds)
kubectl get pods -o wide
```

---
