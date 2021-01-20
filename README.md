# devops-lite-test
測試小型專案部屬 ( 關閉安全性驗證、production與效能提升相關組件)

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
