# devops-lite-test
測試小型專案部屬

## 須注意事項
1. 目前方案無法承受任何一個節點故障
2. 目前方案無法承受任何一點節點滿載
3. 在部屬上仍然為production的k8s方法，僅是關閉HA以及一些額外支援性功能
4. redis保留與資料庫獨立為確保系統運作上的順暢穩定(不會因為一段時間的使用後效能逐漸下降)
5. 下面範例storage採用NFS機制，因此建議有一個獨立的NFS伺服器來源做使用

## chart套件清單
[helm-charts](helm repo add cetic https://cetic.github.io/helm-charts)
[helm/bitnami/postgresql](https://artifacthub.io/packages/helm/bitnami/postgresql)
[helm/bitnami/redis](https://artifacthub.io/packages/helm/bitnami/redis)
[stevehipwell.github.io/helm-charts/](helm repo add stevehipwell https://stevehipwell.github.io/helm-charts/)  
[/bitnami/redmine](https://artifacthub.io/packages/helm/bitnami/redmine)

## 匯入chart套件清單
* `helm repo add bitnami https://charts.bitnami.com/bitnami`
* `helm repo add bitnami https://charts.bitnami.com/bitnami`
* `helm repo add cetic https://cetic.github.io/helm-charts`
* `helm repo add stevehipwell https://stevehipwell.github.io/helm-charts/`
* `helm repo add bitnami https://charts.bitnami.com/bitnami`

## 前安裝
* `snap install helm --classic`
* `kubectl create ns devops`

## 共享安裝版本

### 共享資料庫與Redis
* `helm install -n devops share-postgresql bitnami/postgresql -f ./share-postgresql-install.yaml`
* `helm install -n devops share-redis bitnami/redis -f ./share-redis-install.yaml`
* `helm install -n devops db-gui cetic/adminer`
備註: 需新增`clair`與`registry資料庫`
* `helm install -n devops devops-harbor harbor/harbor -f ./share-harbor-lite-install.yaml`
備註: 需新增`sonarqube`
* `helm install -n devops -f ./share-sonarqube-install.yaml devops-sonarqube stevehipwell/sonarqube`
* `helm install -n devops devops-redmine bitnami/redmine -f ./share-redmine-install.yaml`

## 獨立安裝版本

### gitlab (獨立安裝)
* `helm repo add gitlab https://charts.gitlab.io/`
* `helm repo update`
* `helm install -n gitlab gitlab gitlab/gitlab -f ./gitlab-lite-install.yaml`

## check install condition
* `kubectl get pod -n gitlab`

### harbor (獨立安裝版本)
* `helm repo add harbor https://helm.goharbor.io`
* `kubectl create ns harbor`
* `helm install -n harbor harbor harbor/harbor -f ./harbor-lite-install.yaml`
