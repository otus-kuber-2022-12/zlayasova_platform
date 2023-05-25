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

Homework №11

Основное задание:
Создан кластер consul и vault. Созданы роли и политики. Так же были получены секреты веб сервером и настроена работа vault с сертификатами
Все выводы прикреплены ниже

Error initializing: Error making API request.

URL: PUT http://127.0.0.1:8200/v1/sys/init
Code: 400. Errors:

* Vault is already initialized
  command terminated with exit code 2

Unseal Key 1: Xk6dvtgG5t804g+qVVNl+REjCrtxBFZJnhroMrKczfU=

Initial Root Token: hvs.zQr09tLHQJNTiX3bSCwtYejo

Vault initialized with 1 key shares and a key threshold of 1. Please securely
distribute the key shares printed above. When the Vault is re-sealed,
restarted, or stopped, you must supply at least 1 of these keys to unseal it
before it can start servicing requests.

Vault does not store the generated root key. Without at least 1 keys to
reconstruct the root key, Vault will remain permanently sealed!

It is possible to generate new unseal keys, provided you have a quorum of
existing unseal keys shares. See "vault operator rekey" for more information.

➜  kubernetes-vault git:(kubernetes-vault) ✗ kubectl exec -it vault-0 --  vault login
Token (will be hidden):
Success! You are now authenticated. The token information displayed below
is already stored in the token helper. You do NOT need to run "vault login"
again. Future Vault requests will automatically use this token.

Key                  Value
---                  -----
token                hvs.zQr09tLHQJNTiX3bSCwtYejo
token_accessor       z0cNLWWBwz7zaODke4EkMCdI
token_duration       ∞
token_renewable      false
token_policies       ["root"]
identity_policies    []
policies             ["root"]
➜  kubernetes-vault git:(kubernetes-vault) ✗ kubectl exec -it vault-0 -- vault auth list
Path      Type     Accessor               Description                Version
----      ----     --------               -----------                -------
token/    token    auth_token_8aa9f90d    token based credentials    n/a

➜  kubernetes-vault git:(kubernetes-vault) ✗ kubectl exec -it vault-0 -- vault read otus/otus-ro/config
Key                 Value
---                 -----
refresh_interval    768h
password            Mk7Mdt22ZY
username            otus

➜  kubernetes-vault git:(kubernetes-vault) ✗ kubectl exec -it vault-0 --  vault auth list
Path           Type          Accessor                    Description                Version
----           ----          --------                    -----------                -------
kubernetes/    kubernetes    auth_kubernetes_67d645ab    n/a                        n/a
token/         token         auth_token_8aa9f90d         token based credentials    n/a

hvs.CAESIKrVCURs7SfQEJlMh_O85nHY47lA0SKEz6VvaGF5d5fZGh4KHGh2cy5ldE1MbDlSN0piOFp6aWRUSDcwTk00Nzc

/ # curl --header "X-Vault-Token:$TOKEN" $VAULT_ADDR/v1/otus/otus-ro/config
{"request_id":"c5d62be1-236d-c50e-2068-40b22364fa79","lease_id":"","renewable":false,"lease_duration":2764800,"data":{"password":"Mk7Mdt22ZY","username":"otus"},"wrap_info":null,"warnings":null,"auth":null}

/ # curl --header "X-Vault-Token:$TOKEN" $VAULT_ADDR/v1/otus/otus-rw/config
{"request_id":"cc875599-9b3d-fc51-0793-96898356c2e8","lease_id":"","renewable":false,"lease_duration":2764800,"data":{"password":"Mk7Mdt22ZY","username":"otus"},"wrap_info":null,"warnings":null,"auth":null}


Key                 Value
---                 -----
ca_chain            [-----BEGIN CERTIFICATE-----
MIIDnDCCAoSgAwIBAgIUcEFFg61PIRXOaozvK7cTM3pYkvgwDQYJKoZIhvcNAQEL
BQAwFTETMBEGA1UEAxMKZXhhbXBsZS5ydTAeFw0yMzA1MjAyMjExMTZaFw0yODA1
MTgyMjExNDZaMCwxKjAoBgNVBAMTIWV4YW1wbGUucnUgSW50ZXJtZWRpYXRlIEF1
dGhvcml0eTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAL+ArUlV6Bhm
2s7rCQr93hIQZISjwXxw/ZBr2/wz5b3OXqbqPyfP4ph0BtAeoIEZXuWpKqD1faYp
55WFw6VQlDoY1UmfT3lVCyA5Q2agmMonEZdFwU363v70aaRLd1IsHY96iW9NHDhm
8eAnY0JiC5Us651Zqncy7+fJaiG8G155a/HiOVQAeJORHUofyck6JUXJAy2LWht3
/2n44qGQtHklJlnw6i+GxBbVI+0JwPb3ewyn3B6wY+L4CzkQT7u+7rPXKwnEyNeK
mZsOeJdxgvXLG0Od8KYCxGrUN61a7vnMNnb3PqDv0umXuc9QfzNGkdxQKJ7djFyQ
s54r3RoixCUCAwEAAaOBzDCByTAOBgNVHQ8BAf8EBAMCAQYwDwYDVR0TAQH/BAUw
AwEB/zAdBgNVHQ4EFgQU6zqexDIfsGdl68WYUJxv9ybpt8IwHwYDVR0jBBgwFoAU
VXF9uo7Autb6t525uYYBPUdCWcEwNwYIKwYBBQUHAQEEKzApMCcGCCsGAQUFBzAC
hhtodHRwOi8vdmF1bHQ6ODIwMC92MS9wa2kvY2EwLQYDVR0fBCYwJDAioCCgHoYc
aHR0cDovL3ZhdWx0OjgyMDAvdjEvcGtpL2NybDANBgkqhkiG9w0BAQsFAAOCAQEA
ntGUDuJnwux8zbLAL0CS2zCicVdi5gFMQ5d0zUgKi+zcz7ZoU1wOf8vupwW/OiIa
xei8YtLGnAOfOzmZW3U0AVjkuk7ZBUX2Rv8bMfOJP5DeAhBOi9z7XcH2m2FfHI3Q
BmlLfDXh+ShH50636KSlqk/+BpVPeybFmjYn4HB+1+vTljc9YhvCEUInRCvzafW8
9Ejk1ma9aYV6fQJEt5vD9xE/bEb1Jdn7es+ce3eHJtAB8jgcNoJz7wVPBJVNhGd1
1bn9R2Gvhbt5bkYPIVtJKy+n77jO/6APrZIgCn+bA0pzWVx50MaQekKQvRVl2ywO
qEM1AohCJpZeDfVW9Jsfgw==
-----END CERTIFICATE----- -----BEGIN CERTIFICATE-----
MIIDMjCCAhqgAwIBAgIUZ7liXtUCYVUf2dRzBf1m1SSMwiswDQYJKoZIhvcNAQEL
BQAwFTETMBEGA1UEAxMKZXhhbXBsZS5ydTAeFw0yMzA1MjAyMjA1NTVaFw0zMzA1
MTcyMjA2MjVaMBUxEzARBgNVBAMTCmV4YW1wbGUucnUwggEiMA0GCSqGSIb3DQEB
AQUAA4IBDwAwggEKAoIBAQDQdaJ1wYyFcHtB+e+2nOVKKpr5zcIBnQ3OsSg7VMGh
zcgnCAKwwAaJ/6hbEqPv4R3xnbllq74y0e1wGvlyXBxKHwsqP/1y1C+WY8+er1MW
iM16aNi5SJ9p91n516wljF2o6DEoIQimyREaro6nU0scf9ujnx7ZSbETiGhbONvI
l5fz8MAlGC+B4EXJu2BLOtrE97YXbkEg44td9sBoEeckkIccMP0tUCVu8UwOQ26A
fY2i386/nkoJU2Dl9vC/E3n2w5gHcUV3Kwl3pmE/8uLV89d1SpgPPi7KtlfhSlsN
WB7TA5GY9u5dlza0wFimyfiNcgNnNemqy1TjobmIoA9lAgMBAAGjejB4MA4GA1Ud
DwEB/wQEAwIBBjAPBgNVHRMBAf8EBTADAQH/MB0GA1UdDgQWBBRVcX26jsC61vq3
nbm5hgE9R0JZwTAfBgNVHSMEGDAWgBRVcX26jsC61vq3nbm5hgE9R0JZwTAVBgNV
HREEDjAMggpleGFtcGxlLnJ1MA0GCSqGSIb3DQEBCwUAA4IBAQAbwqpnk6XePxBH
X+IX9yNsvAABJqyk1RKdTbcV4XPNhVXTdxYmo+5SGu5+RF12It0cIVJO3KGSpQ2G
f3t3FuA565l0cQJiftaffql5urfD2N/x8VciK3vLAppFR80qCHg58rd7SI6COY5d
NVUm+wDBPDqNDrr8Slrq3GjH3HDcbqpSfMj4ee265R4Un8+qnmKJYmxy+qQPW37f
hkHXTGA9QzSa86G80MAIJTZGnfkD4ffNJo7fuGXJ9I40E0hS6TsASJ48TUu73UX2
hpRfrw6zV+FzKFBS12nYfgv8VGBfZt8/yDOensM5DKQ+OPVMyClq0T33YYQiQ3Uy
wlopFRvD
-----END CERTIFICATE-----]
certificate         -----BEGIN CERTIFICATE-----
MIIDZzCCAk+gAwIBAgIUJz4taJ78gAIaNMeb+Q63FtE49YowDQYJKoZIhvcNAQEL
BQAwLDEqMCgGA1UEAxMhZXhhbXBsZS5ydSBJbnRlcm1lZGlhdGUgQXV0aG9yaXR5
MB4XDTIzMDUyMDIyMTI0OVoXDTIzMDUyMTIyMTMxOVowHDEaMBgGA1UEAxMRZ2l0
bGFiLmV4YW1wbGUucnUwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCy
lnp+Wv1V9Zf5trDtZAvZx3BTz9AhZtIbxtPBVLs/rnrKLkME+oLsNh7OeCczLiLC
mCz3CPAsb8oVgG/GpoFVHK6UoQqrOALvLHPNeScrsfNHCUfYAqR9D7AgWjhD08xl
80BunSwSf6HpS1XV57lYDNgZuwyocqF1mj9fck1GC1/tcpRz2J97zy+f/QnctjXI
hDTwUDEbBjCUW+RnZFrcphT64IIv/E79wGRKBpkr9J1jtNbkedwqYNgZRjLxk0XR
A2IQ3GGvfpKjhL5+JrMtvX7OGxGr+NsvKzASob2oU6jSVV1Cezix38VbtoZcW1VR
OOmgGgxY4h7h/aqmKPPtAgMBAAGjgZAwgY0wDgYDVR0PAQH/BAQDAgOoMB0GA1Ud
JQQWMBQGCCsGAQUFBwMBBggrBgEFBQcDAjAdBgNVHQ4EFgQUxezZq8HLLZ9D9c0g
JW7pCEziaLowHwYDVR0jBBgwFoAU6zqexDIfsGdl68WYUJxv9ybpt8IwHAYDVR0R
BBUwE4IRZ2l0bGFiLmV4YW1wbGUucnUwDQYJKoZIhvcNAQELBQADggEBABkY63g9
jXLZn4XOck2KItVHlcJWB66iM7CF2gPC+SGYyccTxt19p07KSshO7/yzvRE/h8xi
0962eNSIDLUjwmrT9vZZ5mqiqCkmrv05kP7eyBB7oaiDS979k1+R71PL4YqgER52
pj3oLeajN69MLtVANwmv92MiEvm4mZu7kbbJp9UYubkrYd5klv9HBxaWt4yw37fK
l3KD/Xew9/0bbgy9Pjqsk9Kyt2aGU5Al4C5+vvgMqpXxJEg0yQADsdzjv+aBJ3jp
lHw64rne3+w6SHJf9hy7I7TNNk2eX4S9sBvV0daukCISiWW4KnJsFHYezCICOrD6
EQVk7rvPmRk27vo=
-----END CERTIFICATE-----
expiration          1684707199
issuing_ca          -----BEGIN CERTIFICATE-----
MIIDnDCCAoSgAwIBAgIUcEFFg61PIRXOaozvK7cTM3pYkvgwDQYJKoZIhvcNAQEL
BQAwFTETMBEGA1UEAxMKZXhhbXBsZS5ydTAeFw0yMzA1MjAyMjExMTZaFw0yODA1
MTgyMjExNDZaMCwxKjAoBgNVBAMTIWV4YW1wbGUucnUgSW50ZXJtZWRpYXRlIEF1
dGhvcml0eTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAL+ArUlV6Bhm
2s7rCQr93hIQZISjwXxw/ZBr2/wz5b3OXqbqPyfP4ph0BtAeoIEZXuWpKqD1faYp
55WFw6VQlDoY1UmfT3lVCyA5Q2agmMonEZdFwU363v70aaRLd1IsHY96iW9NHDhm
8eAnY0JiC5Us651Zqncy7+fJaiG8G155a/HiOVQAeJORHUofyck6JUXJAy2LWht3
/2n44qGQtHklJlnw6i+GxBbVI+0JwPb3ewyn3B6wY+L4CzkQT7u+7rPXKwnEyNeK
mZsOeJdxgvXLG0Od8KYCxGrUN61a7vnMNnb3PqDv0umXuc9QfzNGkdxQKJ7djFyQ
s54r3RoixCUCAwEAAaOBzDCByTAOBgNVHQ8BAf8EBAMCAQYwDwYDVR0TAQH/BAUw
AwEB/zAdBgNVHQ4EFgQU6zqexDIfsGdl68WYUJxv9ybpt8IwHwYDVR0jBBgwFoAU
VXF9uo7Autb6t525uYYBPUdCWcEwNwYIKwYBBQUHAQEEKzApMCcGCCsGAQUFBzAC
hhtodHRwOi8vdmF1bHQ6ODIwMC92MS9wa2kvY2EwLQYDVR0fBCYwJDAioCCgHoYc
aHR0cDovL3ZhdWx0OjgyMDAvdjEvcGtpL2NybDANBgkqhkiG9w0BAQsFAAOCAQEA
ntGUDuJnwux8zbLAL0CS2zCicVdi5gFMQ5d0zUgKi+zcz7ZoU1wOf8vupwW/OiIa
xei8YtLGnAOfOzmZW3U0AVjkuk7ZBUX2Rv8bMfOJP5DeAhBOi9z7XcH2m2FfHI3Q
BmlLfDXh+ShH50636KSlqk/+BpVPeybFmjYn4HB+1+vTljc9YhvCEUInRCvzafW8
9Ejk1ma9aYV6fQJEt5vD9xE/bEb1Jdn7es+ce3eHJtAB8jgcNoJz7wVPBJVNhGd1
1bn9R2Gvhbt5bkYPIVtJKy+n77jO/6APrZIgCn+bA0pzWVx50MaQekKQvRVl2ywO
qEM1AohCJpZeDfVW9Jsfgw==
-----END CERTIFICATE-----
private_key         -----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAspZ6flr9VfWX+baw7WQL2cdwU8/QIWbSG8bTwVS7P656yi5D
BPqC7DYezngnMy4iwpgs9wjwLG/KFYBvxqaBVRyulKEKqzgC7yxzzXknK7HzRwlH
2AKkfQ+wIFo4Q9PMZfNAbp0sEn+h6UtV1ee5WAzYGbsMqHKhdZo/X3JNRgtf7XKU
c9ife88vn/0J3LY1yIQ08FAxGwYwlFvkZ2Ra3KYU+uCCL/xO/cBkSgaZK/SdY7TW
5HncKmDYGUYy8ZNF0QNiENxhr36So4S+fiazLb1+zhsRq/jbLyswEqG9qFOo0lVd
Qns4sd/FW7aGXFtVUTjpoBoMWOIe4f2qpijz7QIDAQABAoIBAFm7NCcCzuF++fJ1
ceaFa1LsW6sw8pGl2RItz74HNeJkZ7vojLIWsOvAsa/qPUABAWQnFAi3y/132eD9
3KvCg59hPvLdC8BF72t/OVxXcHALBIJ/zkJh6YYQ+Nz4l+a0p7HeDFTH0holWRQg
TyugN8dfBMHA8zY8CpZNf2QUyXDUdSR1itE3PbFMh8+HX4E0QbuWQ86bp3r1Bn2U
TD+qx7cHXQfyG1K47+8XYt/Y8svHzKMYtz5sxGBPLXxOAqoEyjfRre5+9KaRYk2u
5p1bfNMuXUF6CmLUQyA8gYdX3iYe1Z7WO50KcDxcPGXm8iAo2vQfsyJaVZFM4GS6
WBBA1MECgYEAy0INqYOk3BiIYnNmQf7jgOcSFcy6PazckFwZeRyB4mRzLUXqDhiG
L4yWJvnb3NgtEkRGyOpraZq+5P7Y4a9BUkVrTiFfNAmA/BCYaWTwgemLXcuPvoZq
O+cuBfPpFhFbk5OsxBkUNMq57yz+1mX2ZBHCxVVlzFWFx+3PW44QHN0CgYEA4O2k
OMLMwSMHKv52bn0W20lzTtvRTJrGgAGRogAkbL9TSNwk5SOcUhVpAm3D3G/u8LvU
oEfAssC9E2TYuDq+knKB1miHKM0KZrb8kBZ/ZtGABCsjq8xPlKpYMBmAbVRGAb/W
aKPi2ZbF/TlVpTmwVjCJm0rrC0B0mwtTuHRg+lECgYBoBMa/IJrG9FsfnxUO4yWE
ezx7IYmSNJuv2SJEI72ooWV8HtJ4Ij7RqK3TBn1pGMyAE6bx/V247rOQt4dAgBL6
yoHuuw9grxhuZwPItBqNMXrcJmfKxjkprNaVv0xiucFW1fVNadQ4bCMZbrp/+DBO
5/P4TwrItl+/gElk/l/qlQKBgHfVpDypbDUp2FPLpoVPF7JU+53z9xp9C2x/aXuJ
394gQNr8jpuV0V7aEUw99q+m4wJWz/1kvQF/Njzy6ZOdmJKldw8oOXo/Y1899mk9
0zqQO0f9Q8/v1iY6aymVLJsS3wlnj2/IgL+0WF+FAGA6z/vbeDTIQVmJSZag/kWz
m0dBAoGANpQsqXBLXWzRI1kL3zHW4EW4Smm87no9Yy4LQSdqQSncKiDV3w4ZhdoQ
ItSnAadcWVAWA3WEUPecn5gGRWrNa1Iov6xugCO21I3CGjsFo/YU8lYmSuDRSwvI
f7p4d4IWdYD4+g2gmB/7asqsl1O9YzTaLoy+jJidpHfNhGuCe0U=
-----END RSA PRIVATE KEY-----
private_key_type    rsa
serial_number       27:3e:2d:68:9e:fc:80:02:1a:34:c7:9b:f9:0e:b7:16:d1:38:f5:8a

Homework №12
Основное задание:
Установлен CSI драйвер. Протестирован функционал снапшотов

kubectl get pod
NAME                   READY   STATUS    RESTARTS   AGE
csi-hostpath-socat-0   1/1     Running   0          77m
csi-hostpathplugin-0   8/8     Running   0          77m
csi-storage-pod        1/1     Running   0          9s

kubectl exec csi-storage-pod -- touch /data/test.txt
kubectl exec csi-storage-pod -- ls /data/
test.txt

kubectl delete -f hw/csi-pvc.yaml -f hw/storage-pod.yaml
persistentvolumeclaim "csi-storage" deleted
pod "csi-storage-pod" deleted

kubectl apply -f hw/csi-restore.yaml
persistentvolumeclaim/hpvc-restore created


kubectl apply -f hw/storage-pod.yaml
pod/csi-storage-pod created


kubectl get pod
NAME                   READY   STATUS    RESTARTS   AGE
csi-hostpath-socat-0   1/1     Running   0          109m
csi-hostpathplugin-0   8/8     Running   0          109m
csi-storage-pod        1/1     Running   0          6s

kubectl exec csi-storage-pod -- ls /data/
test.txt