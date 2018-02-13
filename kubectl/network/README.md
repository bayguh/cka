# ネットワークまわり

公式ドキュメント<br />
https://kubernetes.io/docs/concepts/services-networking/service/

---

## clusterIP
clusterIP -> コンテナ待受port

確認
```
kubectl apply -f clusterip.yml
kubectl get service(svc)
```

## nodePort
clusterIP -> nodeサーバ待受port -> コンテナ待受port

確認
```
kubectl apply -f nodeport.yml
kubectl get service(svc)
```

## loadbalancer(内部ロードバランサ)
EXTERNAL-IP(LB) -> clusterIP -> nodeサーバ待受port -> コンテナ待受port

確認
```
kubectl apply -f loadbalancer.yml
kubectl get service(svc)
```

---

## externalName

CNAME設定<br />

確認
```
kubectl apply -f loadbalancer.yml
kubectl get service(svc)
```

---

## ingress(ロードバランサ)

https://kubernetes.io/docs/concepts/services-networking/ingress/ <br />

確認
```
kubectl apply -f ingress.yml
kubectl get service(svc)
```
