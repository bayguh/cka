# kubectlチートシート

## 公式ページ
https://kubernetes.io/docs/reference/kubectl/cheatsheet/

---

## 補完設定
```
# bash
echo "source <(kubectl completion bash)" >> ~/.bashrc
# zsh
echo "source <(kubectl completion zsh)" >> ~/.zshrc
```

---

### クラスター関連

```
# クラスター情報
kubectl cluster-info
# クラスター情報詳細
kubectl cluster-info dump

# クラスターノード一覧
kubectl get nodes
# クラスタノードー詳細
kubectl describe node [node名]
# 不要なクラスターノード削除
kubectl delete node [ノード名]
```

### pod関連
```
# pod一覧
kubectl get pods
# pod一覧(ラベル表示)
kubectl get pod --show-labels
# pod一覧(node表示)
kubectl get pod -o wide

# podー詳細
kubectl describe pod [pod名]
# pod削除
kubectl delete pod [pod名]

# ログ取得
kubectl logs [pod名]
# ログtail
kubectl logs -f [pod名]

# podに対してコマンド実行
kubectl exec [pod名] [コマンド]
```

### replicaset関連
```
# replicaset一覧
kubectl get replicasets(rs)
# replicaset削除
kubectl delete replicaset [replicaset名]
```

### service関連
```
# サービス一覧
kubectl get services(svc)
# サービス削除
kubectl delete service [service名]
```

### メンテナンス
```
# スケジューラの候補から外す
kubectl cordon [node名]

# podの退避
kubectl drain [node名] --force --delete-local-data
```

### その他
```
# リソースの作成/更新
kubectl apply -f ./resource.yml
# リソースの削除
kubectl delete -f ./resource.yml

# kubectlのconfig情報
kubectl config view

## kubernetes version確認
kubectl version
```

---

### オプション
```
# --all-namespaces(全てのnamespaceが対象)
# -o wide(情報量が増える)
# -o json(詳細情報をjsonで出力)
# -o yaml(詳細情報をyamlで出力)
# -w(変更差分を定期的に表示)
```
