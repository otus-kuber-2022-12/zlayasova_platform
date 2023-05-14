# zlayasova_platform
zlayasova Platform repository

HomeWork №1

Основное задание:
Собран docker-образ веб-сервера. Создан манифест для приложения. Проверена работоспособность приложения.
Дополнительно задание:
Pod не запускался из-за не указанной переменной "PRODUCT_CATALOG_SERVICE_ADDR"

HomeWork №2

Основное задание:
Созданые манифесты для реплик и деплоймента приложения. Собран docker-образ приложения paymentservice. Применены различные созданные манифесты
Дополнительное задание:
Обновление ReplicaSet не повлекло обновлению pod, потому что контроллер ReplicaSet управляет только количеством реплик. Для обновления необходимо пересоздать ReplicaSet
Какая разница между ReplicaSet и Deployments в k8s?
ReplicaSet-сущность, которая следит за количеством подов
Deployment-это обертка над ReplicaSet, которая позволяет желаемое состояние pod и автоматическое обновление. Так же он предоставляет возможность откатываться к предыдущему состоянию или отключить обновление

Созданы манифесты для разного способа обновления приложения и создан манифест для развертывания приложения node exporter на все ноды

HomeWork №3

Основное задание:
Созданы и применены манифесты для сетевых сервисов и деплоя приложения

Homework №4

Основное задание:
Создан манифест для работы приложения minio.
Дополнительное задание:
Переменные были вынесены в Secrets

Homework №5
Основное задание:
Созданы манифесты для создания сервисных аккаунтов, ролей и их привязке

Homework №6
Основное задание:
Созданы манифесты helm-charts для развертывания микросервисов в кластере

Homework №7
Основное задание:
Создан манифест для CDR mysqls.otus.homework. Так же созданы манифесты для контроллера
Вывод "kubectl exec -it $MYSQLPOD -- mysql -potuspassword -e "select * from test;" otus-database"
mysql: [Warning] Using a password on the command line interface can be insecure.
+----+------------+
| id | name       |
+----+------------+
|  1 | some data  |
|  2 | some data2 |
+----+------------+

Homework №8
Основное задание:
Созданы манифесты для приложения и подключения его к системе мониторинга

Homework №9
Основное задание:
Создан кластер с двумя разными группами узлов. Создан кластер ELK для сбора логов. Так же был установлен Loki для сбора логов

Homework №10
Основное задание:
Создан кластер k8s. Создан репозиторий в gitlab. Был подключен flux для отслеживания версий сервисов в registry.
Так же был подключен istio и flagger и настроен canary deployment

kubectl describe canary frontend -n microservices-demo

Type     Reason  Age                 From     Message
  ----     ------  ----                ----     -------
Warning  Synced  20m                 flagger  frontend-primary.microservices-demo not ready: waiting for rollout to finish: observed deployment generation less than desired generation
Normal   Synced  20m (x2 over 20m)   flagger  all the metrics providers are available!
Normal   Synced  20m                 flagger  Initialization done! frontend.microservices-demo
Normal   Synced  17m                 flagger  Starting canary analysis for frontend.microservices-demo
Warning  Synced  17m                 flagger  canary deployment frontend.microservices-demo not ready: waiting for rollout to finish: 1 old replicas are pending termination
Normal   Synced  13m (x2 over 18m)   flagger  New revision detected! Scaling up frontend.microservices-demo
Normal   Synced  12m (x2 over 17m)   flagger  Advance frontend.microservices-demo canary weight 10
Normal   Synced  12m (x2 over 16m)   flagger  Advance frontend.microservices-demo canary weight 20
Normal   Synced  11m (x2 over 16m)   flagger  Advance frontend.microservices-demo canary weight 30
Normal   Synced  11m (x2 over 15m)   flagger  Advance frontend.microservices-demo canary weight 40
Normal   Synced  10m (x2 over 15m)   flagger  Advance frontend.microservices-demo canary weight 50
Normal   Synced  10m                 flagger  Copying frontend.microservices-demo template spec to frontend-primary.microservices-demo
Normal   Synced  9m3s (x6 over 14m)  flagger  (combined from similar events): Promotion completed! Scaling down frontend.microservices-demo


