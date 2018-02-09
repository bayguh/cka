# ストレージまわり

公式ドキュメント<br />
https://kubernetes.io/docs/concepts/storage/volumes/

---

## Volume

### EmptyDir
pod用の一時的なディスク

### HostPath
Node上のディレクトリをコンテナにマウントする<br />
typeにはDirectory, DirectoryOrCreate, File, FileOrCreateなどがある<br />

---

## PersistentVolume
永続化領域として確保されるVolume<br /><br />

https://kubernetes.io/docs/concepts/storage/persistent-volumes/<br / >

```
kubectl apply -f persistentvolume.yml
kubectl get persistentvolumes(pv)
```

アクセスモード
```
ReadWriteOnce: 単一ノードからRead/Writeされます
ReadOnlyMany: 単一ノードからWrite、複数ノードからReadされます
ReadWriteMany: 複数ノードからRead/Writeされます
```

Reclaim Policy(PV利用終了後どうするか)
```
Retain: PVのデータも消さずに保持するので再マウントされない
Recycle: PVのデータを削除し再マウントされる可能性がある
Delete: PV自体が削除されます
```

Storage Class(どのようなディスクを利用するか)

---

## PersistentVolumeClaim
Persistent Volume Claimは永続化領域の要求を行うリソース

作成
```
kubectl apply -f persistentvolumeclaim.yml
```

確認
```
kubectl get pvc
kubectl get pv
```

※ pvとpvcのアクセスモードが異なるとPendingとなる



