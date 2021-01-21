# devops-lite-test
測試小型專案部屬

## 須注意事項
1. 目前方案無法承受任何一個節點故障
2. 目前方案無法承受任何一點節點滿載
3. 在部屬上仍然為production的k8s方法，僅是關閉HA以及一些額外支援性功能
4. redis保留與資料庫獨立為確保系統運作上的順暢穩定(不會因為一段時間的使用後效能逐漸下降)
5. 下面範例storage採用NFS機制，因此建議有一個獨立的NFS伺服器來源做使用

## 前安裝
* `snap install helm --classic`

# gitlab
* `helm repo add gitlab https://charts.gitlab.io/`
* `helm repo update`
* `helm install -n gitlab gitlab gitlab/gitlab -f ./gitlab-lite-install.yaml`
* `helm get values gitlab > gitlab.yaml`

## check install condition
* `kubectl get pod -n gitlab`

# harbor
* `helm repo add harbor https://helm.goharbor.io`
* `kubectl create ns harbor`
* `helm install -n harbor harbor harbor/harbor -f ./harbor-lite-install.yaml`
