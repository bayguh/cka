# namespace作成

Namespaceを使うことによりPodなどのリソースを分離することが可能

---

作成
```
kubectl apply -f namespace.yml
```

確認
```
kubectl get namespace(ns)
```

---

namespaceを指定してリソースを作成したい場合、下記のようにmetadata指定
```
apiVersion: v1
kind: Pod
metadata:
  name: sample-pod
  namespace: project1
  labels:
    app: sample-app
spec:
  containers:
    - name: nginx-container
      image: zembutsu/docker-sample-nginx:1.0
      ports:
        - containerPort: 80
```
