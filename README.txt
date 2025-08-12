yc managed-kubernetes cluster get-credentials --id cat86okbh6a2fvag1hak --external


kubectl version --client
kubectl cluster-info 
kubectl get nodes
kubectl get nodes -o wide
kubectl top nodes - получить информацию о потребление ресурсов на нодах

kubectl apply -f my-deployment.yaml - Команда для применения изменений в deployment
kubectl set image deployment/my-deployment my-container=nginx:1.19.2 - Обновление можно выполнить императивным способом

kubectl scale deployment my-deployment --replicas=10 - Для масштабирования до 10 реплик
kubectl rollout undo deployment/my-deployment - Откат изменений

kubectl get deployment <deployment_name> -o yaml- Для анализа причин возникшей проблемы (смотреть поле status)
kubectl get deployment <deployment-name> - Для мониторинга состояния Deployment
kubectl describe deployment <deployment-name> - для получения более подробной информации о ходе развёртывания и возможных проблемах.
kubectl delete -f deploy.yaml

kubectl create namespace my-namespace
kubectl apply -f pod.yaml -n my-namespace
kubectl get pods -n my-namespace
kubectl config set-context --current --namespace=my-namespace - Вы можете настроить контекст по умолчанию для работы в определённом Namespace
kubectl delete ns application

kubectl logs <POD_NAME>
kubectl logs <POD_NAME> -c another-container - Если Pod содержит несколько контейнеров, необходимо указать имя контейнера
kubectl logs --since=1h
kubectl logs nginx-deploy-6b7f675859-xg7bv --since=30m

kubectl create configmap wordpress-config --from-literal=WORDPRESS_DB_HOST=localhost --from-literal=WORDPRESS_DB_NAME=exampledb

kubectl exec nginx-pod -- cat /etc/nginx/nginx.conf - проверка что файл в Поде

Команда kubectl exec используется для выполнения curl-запроса внутри Pod nginx-pod в Kubernetes.
Опция -s -S используется для подавления вывода прогресса и информации об операционной системе,
что позволяет получить чистый текст ответа от веб-сервера, настроенного на http://localhost
kubectl exec nginx-pod -- curl -s -S -u user:password http://localhost

Создать сервис можно и императивным путём с помощью команды.
Здесь nginx-app — название Deployment, для которого будет создан сервис. Такой способ создания сервиса подходит для экспериментов и разработки.
kubectl expose deployment nginx-app --port 80 --target-port=8080

Helm-charts
1. helm repo add — добавляет репозиторий с Helm-чартами. (helm repo add stable https://charts.helm.sh/stable)
2. helm repo update — обновляет локальный кеш репозиториев с чартами.
3. helm search repo/hub — ищет чарты в добавленном или официальном репозитории. (helm search repo mysql; helm search hub mysql)
4. helm template — генерирует манифесты, позволяя предварительно просмотреть конфигурацию.
5. helm list — показывает список установленных релизов.
6. helm upgrade — обновляет установленный релиз с новыми версиями чарта или значениями.
7. helm rollback — откатывает релиз до предыдущей версии. (helm rollback my-release 1)
8. helm uninstall — удаляет установленный релиз из кластера.
9. helm show values — показывает значения по умолчанию для чарта.
10. helm package — создаёт пакет чарта из локальной директории. (helm package mychart/)
11. helm --help - Для просмотра всех команд Helm.