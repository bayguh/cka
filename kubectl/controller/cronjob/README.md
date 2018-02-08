# CronJob

公式ドキュメント<br />
https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/

---

Cronのようにスケジュールされた時間にJobを生成するリソース<br />

---

作成
```
kubectl apply -f cronjob.yml --record
```

確認
```
kubectl get cronjob
kubectl get jobs
```

---

## 設定

同時実行ポリシー: spec.concurrencyPolicy
```
Allow(default): 同時実行に対して制限を行わない
Forbid: 同時実行を行わない
Replace: 前のjobをキャンセルし実行する
```

開始時刻が遅れた場合に許容できる秒数: spec.startingDeadlineSeconds<br />
保存する成功jobリソースの数: spec.successfulJobsHistoryLimit<br />
保存する失敗jobリソースの数: spec.failedJobsHistoryLimit<br />
