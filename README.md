# kube-autoscale-example
Kubernetes auto-scale, exemplo rápido utilizando o stress-ng;

## Documentação de referência:

* [Kubernetes: Horizontal Pod Autoscaler](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/)

* [GCP: Como configurar um escalonador automático de pod horizontal](https://cloud.google.com/kubernetes-engine/docs/how-to/horizontal-pod-autoscaling?hl=pt-br#kubectl-get)

* [Testes de stress de CPU com base no pacote Stress-ng](https://kernel.ubuntu.com/~cking/stress-ng/)

O modelo baseia-se na documentação ofical do GCP com algumas adequações para simular rapidamente o stress nos recursos forçando scale;

```sh
kubectl apply -f https://git.io/JflSi
# URL Original: https://raw.githubusercontent.com/sre-team/kube-autoscale-example/master/deploy/kube-autoscale-hpa-example.yaml
#
kubectl get deploy,hpa
```

Implementando o stress para o teste de hpa:
```sh
kubectl exec deploy/nginx -- sh -c 'apk add stress-ng'
```

Neste exemplo a unica replica em execução receberá uma alocação de 1 core de CPU, 75% acima do limits configurado:
```sh
kubectl exec deploy/nginx -- sh -c 'stress-ng --cpu 1'
```

Durante a execução verifique as metricas atuais de cpu e o hpa:
```sh
kubectl get hpa
kubectl top po
```

---
@sre-team 2020
