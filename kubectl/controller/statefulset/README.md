# StatefulSet

公式ドキュメント<br />
https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/

---

データベースなどstateful(永続データなど)で利用する<br />

---

作成
```
kubectl apply -f storageclass.yml
kubectl apply -f statefulset.yml --record
```

確認
```
kubectl get statefulset(sts)
kubectl get pods -o wide
```

---
