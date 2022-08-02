# shopper application

Документация

* 🇬🇧 [English version](https://www.github.com/arturyumaev/shopper/blob/main/README.md)
* 🇷🇺 [Russian version](https://www.github.com/arturyumaev/shopper/blob/main/README_rus.md)

Приложение состоит из нескольких микросервисов в отдельных репозиториях

- [shopper-db](https://www.github.com/arturyumaev/shopper-db)
- [shopper-api](https://www.github.com/arturyumaev/shopper-api)

___

Для запуска на MacOS с драйвером `virtualbox` я использовал [minikube](https://minikube.sigs.k8s.io/docs/start/) и [virtualbox](https://www.virtualbox.org/wiki/Downloads).

Установить [helm](https://helm.sh/), если он не был установлен. Запустить minikube с драйвером `virtualbox` командой

```shell
minikube start --memory=4096 --driver=virtualbox
```

Получить `ip` кластера в `minikube`:

```shell
minikube ip
```

После получения `ip` добавить следующую строчку в конец файла `/etc/hosts/` (`<ip>` заменить на полученный `ip`):

```shell
<ip> arch.homework
```

## Последовательность запуска

### shopper-db

В репозитории проекта `shopper-db` в директории `k8s` выполнить скрипт

```shell
$ ./k8s.sh up
```

После успешного создания экземпляра базы данных `postgres` накатить миграцию командой

```shell
$ kubectl apply -f ./shopper-db/job.yaml
```

### shopper-api

В репозитории проекта `shopper-api` в директории `k8s` выполнить скрипт

```shell
$ ./k8s.sh up
```

Проверить доступность сервиса

```shell
$ curl arch.homework/health
```

Запустить тесты

```shell
$ newman run shopper-api.postman_collection.json
```
