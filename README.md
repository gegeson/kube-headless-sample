# kueb-headless-sample

Kubernetesのheadless serviceを使って各PodのIPを知る.

## 手順

1. Deploymentをapplyする

        $ kubectl apply -f deployment.yaml

2. Podができているか確認

        $ kubectl get pods -o wide

3. Serviceをapplyする

        $ kubectl apply -f service.yaml

4. Serviceができているか確認

        $ kubectl get services headless-svc -o wide

5. 同じnamespaceにnslookupのあるbusyboxコンテナを立ち上げてみます。

        $ kubectl run busybox --image=busybox --restart=Never --tty -i

6. コンソール内で先程立ち上げたserviceから引いてみると

        / # nslookup headless-svc

こんな感じにIP取得

```
/ # nslookup headless-svc
Server:         10.152.183.10
Address:        10.152.183.10:53

Name:   headless-svc.ingress-tutorial.svc.cluster.local
Address: 10.1.254.77
Name:   headless-svc.ingress-tutorial.svc.cluster.local
Address: 10.1.254.80
```
