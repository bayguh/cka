# 設定まわり

公式ドキュメント<br />
https://kubernetes.io/docs/concepts/configuration/overview/

---

## 環境変数

https://kubernetes.io/docs/tasks/inject-data-application/environment-variable-expose-pod-information/<br /><br />

spec.containers[x].envでコンテナ内に環境変数を渡すことが可能<br />
podに関する情報はfieldRefで取得可能<br />
containerに関する情報はresourceFieldRefで取得可能<br />
<br />

確認
```
kubectl exec -it env env
kubectl logs env
```

---

## 機密情報

https://kubernetes.io/docs/concepts/configuration/secret/<br /><br />

Secret は認証情報などの機密情報を保持するためのリソース<br />

作成方法
```
# ファイルから作成(改行コード注意)
kubectl create secret generic db-auth --from-file=./secret_file/username --from-file=./secret_file/password

# yamlから作成
kubectl apply -f secret.yml

# kubectl直指定(機密的にはこちら)
kubectl create secret generic db-auth --from-literal=username=root --from-literal=password=password

# envfile指定(複数指定可能なので、こちらがいいかな)
kubectl create secret generic db-auth --from-env-file ./secret_file/env_secret
```

確認
```
kubectl get secret db-auth -o json | jq .data
kubectl get secret db-auth -o json | jq .data.username | base64 -d
kubectl get secret db-auth -o json | jq .data.password | base64 -d
```

---

## 証明書の登録
```
# openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /tmp/tls.key -out /tmp/tls.crt -subj "/CN=sample1.example.com"
kubectl create secret tls tls-sample --key /tmp/tls.key --cert /tmp/tls.crt
```

---

## ConfigMap

https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/<br /><br />

設定情報などの Key-Value で保持できるデータを保存しておくリソース<br />
nginx.confやmy.cnfの設定で使用する<br />
環境変数とかも全てこちらで管理してコンテナに渡すことで設定類がまとまるので、管理がしやすくなる<br /><br />

作成方法
```
kubectl create configmap nginx --from-file=./configmap_file/nginx.conf
kubectl create configmap env --from-env-file ./configmap_file/env_configmap
```

確認方法
```
kubectl describe configmap nginx
kubectl describe configmap env
```

### ConfigMapの定義を環境変数で渡す
```
kubectl apply -f env_configmap.yml
```

確認方法
```
kubectl exec -it env-configmap env
kubectl exec -it env-configmap env | grep CONNECTION_MAX
```

### ConfigMapの定義をValumeとしてマウントする
```
kubectl apply -f volume_configmap.yml
```

確認方法
```
kubectl exec -it volume_configmap cat /config/nginx.conf
```

※ ConfigMapを変更することでマウントしているファイルを動的に変更することが可能<br />
  kubeletのSync Loopのタイミングでチェックされる(デフォルト60秒)
