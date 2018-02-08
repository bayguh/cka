# Deployment

公式ドキュメント<br />
https://kubernetes.io/docs/concepts/workloads/controllers/deployment/

---

複数のReplicaSetを管理することで、Blue Green Deployment、ローリングアップデート、ロールバックなどを実現可能にするリソース<br />
Kubernetesでは最も推奨されているコンテナの起動方法となっています。1コンテナだけでもDeploymentを利用する<br />

---

作成
```
kubectl apply -f deployment.yml --record
```

確認
```
kubectl get deployment(deploy)
kubectl get rs
kubectl get pods
```

---

## ローリングアップデート

イメージの更新(本来はyaml更新してapply)
```
kubectl set image deployment/deployment nginx=zembutsu/docker-sample-nginx:latest
```

確認
```
kubectl get rc

# 実行中のステータス確認
kubectl rollout status deployment/deployment
# リビジョン等確認
kubectl rollout history deployment/deployment
# リビジョン指定で詳細確認
kubectl rollout history deployment/deployment --revision 1
```

---

## ロールバック
```
# 直前にロールバック
kubectl rollout undo deployment/deployment
# リビジョン指定でロールバック
kubectl rollout undo deployment/deployment --to-revision 1
```

## 更新禁止
```
# 更新ができなくなる
kubectl rollout pause deployment/deployment

# 更新可能にする
kubectl rollout resume deployment/deployment
```
