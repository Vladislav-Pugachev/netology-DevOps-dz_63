### Задание 1: подготовить helm чарт для приложения
- подготовленные манифесты:
    - - [backend](./app/templates/deploy/backend.yml)
    - - [frontend](./app/templates/deploy/frontend.yml)
    - - [statfulsets](./app/templates/statefullset/postgres.yml)
    - - [service backend](./app/templates/service/backend-srv.yml)
    - - [service frontend](./app/templates/service/front-srv.yml)
    - - [service statefulset](./app/templates/service/statfullset-srv.yml)
    - - [persistent volume](./app/templates/volume/pv.yml)
    - - [persistent volume claim](./app/templates/volume/pvc.yml)
    - - [storage class](./app/templates/volume/st.yml)
- переменные которые можно переопределить находятся в файле [values.yml](./app/values.yaml)

### Задание 2: запустить 2 версии в разных неймспейсах
- запуск первой версии приложения в namespase app1
```
vlad@home:~/Documents/Netology/DevOps/netology-DevOps-dz_63$ helm install -n app1 first -f ./app/my_values.yml ./app
NAME: first
LAST DEPLOYED: Thu Nov  3 15:55:08 2022
NAMESPACE: app1
STATUS: deployed
REVISION: 1
TEST SUITE: None
```
- запуск второй версии приложения в том же  namespase
```
vlad@home:~/Documents/Netology/DevOps/netology-DevOps-dz_63$ helm install -n app1 first2 -f ./app/my_values.yml ./app
NAME: first2
LAST DEPLOYED: Thu Nov  3 15:55:20 2022
NAMESPACE: app1
STATUS: deployed
REVISION: 1
TEST SUITE: None
```
- запуск приложения в namespase app2
```
vlad@home:~/Documents/Netology/DevOps/netology-DevOps-dz_63$ helm install -n app2 first3 -f ./app/my_values.yml ./app
NAME: first3
LAST DEPLOYED: Thu Nov  3 16:08:39 2022
NAMESPACE: app2
STATUS: deployed
REVISION: 1
TEST SUITE: None
```

- Все запущенные версии
```
vlad@home:~/Documents/Netology/DevOps/netology-DevOps-dz_63$ kubectl get pods -A
NAMESPACE     NAME                                       READY   STATUS    RESTARTS       AGE
app1          first-backend-69c9f596cf-wx99p             1/1     Running   0              112m
app1          first-front-9fb74645d-9hg6p                1/1     Running   0              112m
app1          first-postgres-0                           1/1     Running   0              112m
app1          first2-backend-7fdb894ff-xtdjm             1/1     Running   0              111m
app1          first2-front-997796b66-ghlrh               1/1     Running   0              111m
app1          first2-postgres-0                          1/1     Running   0              111m
app2          first3-backend-7d7947b5fb-lnrns            1/1     Running   0              98m
app2          first3-front-75f4ccd9df-hkmdk              1/1     Running   0              98m
app2          first3-postgres-0                          1/1     Running   0              98m
```
