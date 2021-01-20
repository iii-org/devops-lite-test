# devops-lite-test
測試小型專案部屬 ( 關閉安全性驗證、production與效能提升相關組件)

# gitlab
* `helm repo add gitlab https://charts.gitlab.io/`
* `helm repo update`
* `helm install -n gitlab gitlab gitlab/gitlab -f ./gitlab-lite-install.yaml`
#* `helm get values gitlab > gitlab.yaml`
