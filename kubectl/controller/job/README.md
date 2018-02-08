# Job

公式ドキュメント<br />
https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/

---

一度限りの処理を実行させるリソース<br />
バッチ処理などで利用する<br />

---

作成
```
kubectl apply -f job.yml --record
```

確認
```
kubectl get job
kubectl get pods
```

---

## ライフサイクル

再起動動作はspec.restartPolicyで設定可能
```
OnFailure: 再度同一のPodを利用してJobを再開
Never: pod障害時には新規のPodを作成
```
