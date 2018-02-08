# ReplicaSet

公式ドキュメント<br />
https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/

---

指定した数のPodを維持し続ける機能<br/ >
templateに生成するpodを記載する<br/ >

---

作成
```
kubectl apply -f replicaset.yml
```

確認
```
kubectl get replicasets(rs)
kubectl get pods
```

---

## podのスケール
```
kubectl scale rs [replicaset名] --replicas 5
```
もしくはyamlを書き換えてapplyする<br />
yamlの状態を正にしたいのでできればyamlを書き換える運用にしたい<br />
