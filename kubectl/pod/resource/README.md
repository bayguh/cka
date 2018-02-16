# リソース

公式ページ<br />
https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/

---

CPUとMemoryのみ定義可能

作成
```
kubectl apply -f resource.yml
```

確認
```
kubectl describe node
```

---

## LimitRange
デフォルトリソース定義(Namespace毎に設定)<br /><br />

https://kubernetes.io/docs/tasks/administer-cluster/memory-default-namespace/<br />
https://kubernetes.io/docs/tasks/administer-cluster/cpu-default-namespace/<br />
https://kubernetes.io/docs/tasks/administer-cluster/memory-constraint-namespace/<br />
https://kubernetes.io/docs/tasks/administer-cluster/cpu-constraint-namespace/<br />

作成
```
kubectl apply -f limitrange.yml
```

確認
```
kubectl describe limitrange
```
---

## Resource Quota
クラスタ毎に利用可能なResourceを制限する<br /><br />

https://kubernetes.io/docs/tasks/administer-cluster/quota-memory-cpu-namespace/<br />
https://kubernetes.io/docs/tasks/administer-cluster/quota-pod-namespace/<br />
https://kubernetes.io/docs/tasks/administer-cluster/quota-api-object/<br />

作成
```
kubectl apply -f resourcequota.yml
```

確認
```
kubectl describe resourcequota --namespace=project1
```
