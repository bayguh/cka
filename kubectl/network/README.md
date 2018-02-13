# ネットワークまわり

公式ドキュメント<br />
https://kubernetes.io/docs/concepts/services-networking/service/

---

## Service

確認
```
kubectl apply -f service.yml
kubectl get service(svc)

for i in `seq 1 100`; do curl -s http://svc:8080; done | grep Host | sort | uniq
```
