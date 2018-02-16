# [WIP うごかない]podpreset

公式ページ<br />
https://kubernetes.io/docs/concepts/workloads/pods/podpreset/

---

Pod を作成する際にデフォルト設定を埋め込むリソース<br />

設定
```
# kube-apiserverのadmission-controlにパラメータ設定
--admission-control=PodPreset
```


確認
```
kubectl apply -f podpreset.yml
```
