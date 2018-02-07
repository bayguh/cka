# kubectlチートシート

## 補完設定
```
# bash
echo "source <(kubectl completion bash)" >> ~/.bashrc
# zsh
echo "source <(kubectl completion zsh)" >> ~/.zshrc
```

---

```
# クラスター情報取得
kubectl cluster-info
# クラスターノード確認
kubectl get nodes
# 不要なノード削除
kubectl delete node [ノード名]
```
