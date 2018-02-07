# Pod

Kubernetesの最小リソース単位。1Pod = 1Containerが基本

---

作成
```
kubectl apply -f pod.yml
```

確認
```
kubectl get pods(po)
```

---

コンテナへログイン
```
kubectl exec -it [pod名] /bin/bash
```

---

## 特権コンテナ

kube-apiserverとkubeletで「--allow-privileged=true」に設定し<br />
yaml定義のspec.containers[0-9].securityContext.privileged = true に設定する

---

## init Container

Pod内のコンテナを起動する前に動作するコンテナ

---

## ライフサイクル

再起動動作はspec.restartPolicyで設定可能
```
Always: 常に再起動
OnFailure: exit-code0以外の場合再起動
Never: 再起動しない
```

postStart: コンテナ起動後に実行される<br />
preStop: コンテナ停止直前に実行される<br />
