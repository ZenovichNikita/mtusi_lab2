# Технологии разработки программного обеспечения
## Лабораторная работа №2: создание кластера Kubernetes и деплой приложения
## Зенович Никита Евгеньевич ЗМБД2031
Целью лабораторной работы является знакомство с кластерной архитектурой на примере Kubernetes, а также деплоем приложения в кластер.
## Манифест deployment.yaml
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
spec:
  replicas: 10
  selector:
    matchLabels:
      app: my-app
  strategy:
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
    type: RollingUpdate
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - image: myapi:latest
          imagePullPolicy: Never 
          name: myapi
          ports:
            - containerPort: 8080
      hostAliases:
      - ip: "192.168.49.1" # The IP of localhost from MiniKube
        hostnames:
          - postgres.local
```

## Манифест service.yaml
```

apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: NodePort
  ports:
    - nodePort: 31317
      port: 8080
      protocol: TCP
      targetPort: 8080
  selector:
    app: my-app
```
## Ссылки на скриншоты
https://drive.google.com/file/d/1JgAn0Gy-FH63G8_xwC19UJVsmhZ3dM89/view?usp=sharing

https://drive.google.com/file/d/11BLU0JH3SvLRMCSJJQEm21CAOAX2nnYb/view?usp=sharing

## Ссылка на видео
https://drive.google.com/file/d/1lrWwW24gfK5MN9RBnp4Lvo5pRA0IVbdA/view?usp=sharing
