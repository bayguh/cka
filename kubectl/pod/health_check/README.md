# ヘルスチェック

公式ページ<br />
https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/

---

## ▼ 分類
Liveness Prove: podの生存確認、失敗した場合pod再生成<br />
Readiness Prove: podの疎通性確認、失敗した場合pod再生成しない<br />

## ▼ チェック方法
exec: コマンドを実行し、終了コードで判定(0か0以外か)<br />
httpGet: httpリクエストを実行しstatusで判定(200-399かそれ以外か)<br />
tcpSocket: tcpコネクション<br />

## チェック間隔
initialDelaySeconds: ヘルスチェック開始までの期間<br />
periodSeconds: ヘルスチェックの間隔<br />
timeoutSeconds: タイムアウトまでの秒数<br />
successThreshold: 成功と判断するまでのチェック回数<br />
failureThreshold: 失敗と判断するまでのチェック回数<br />

