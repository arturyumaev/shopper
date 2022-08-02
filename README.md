# shopper application

Documentation

* 🇬🇧 [English version](https://www.github.com/arturyumaev/shopper/blob/main/README.md)
* 🇷🇺 [Russian version](https://www.github.com/arturyumaev/shopper/blob/main/README_rus.md)

The application consists of 2 parts:

- [shopper-db](https://www.github.com/arturyumaev/shopper-db)
- [shopper-api](https://www.github.com/arturyumaev/shopper-api)

___

To run on MacOS with `virtualbox` driver I used [minikube](https://minikube.sigs.k8s.io/docs/start/) and [virtualbox](https://www.virtualbox.org/wiki/Downloads).

Install [helm](https://helm.sh/), if it hasn't been installed yet. Run `minikube` with `virtualbox` driver

```shell
$ minikube start --memory=4096 --driver=virtualbox
```

Get cluster `ip` from `minikube`:

```shell
$ minikube ip
```

After getting `ip` add the next line at the end of the `/etc/hosts/` file (`<ip>` replace with minikube `ip`):

```shell
<ip> arch.homework
```

## Run in kubernetes

### shopper-db

In `shopper-db` repository in `k8s` directory run script

```shell
$ ./k8s.sh up
```

After successfully creating `postgres` instance apply migrations by running

```shell
$ kubectl apply -f ./shopper-db/job.yaml
```

### shopper-api

In `shopper-api` repository in `k8s` directory run script

```shell
$ ./k8s.sh up
```

Check service availability

```shell
$ curl arch.homework/health
```

Run tests

```shell
$ newman run shopper-api.postman_collection.json
```