# 設定まわり

公式ドキュメント<br />
https://kubernetes.io/docs/concepts/configuration/overview/

---

## 環境変数

https://kubernetes.io/docs/tasks/inject-data-application/environment-variable-expose-pod-information//<br />

spec.containers[x].envでコンテナ内に環境変数を渡すことが可能<br />
podに関する情報はfieldRefで取得可能<br />
containerに関する情報はresourceFieldRefで取得可能<br />
<br />

確認
```
kubectl exec -it env env
kubectl logs env
```


