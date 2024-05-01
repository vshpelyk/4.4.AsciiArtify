### ArgoCD
-------
**ArgoCD** - це зручний інструмент GitOps для організації continuous delivery застосунку в кластер K8s

**Архітектура**
![ArgoDC](https://github.com/vshpelyk/4.4.AsciiArtify/blob/main/doc/argocd_arch.png)

1. Створюємо кластер argo для встановлення ArgoCD
```sh
k3d cluster create argo
```
2. Встановлюємо ArgoDC
```sh
# для зручності створимо окремий namespace argocd
kubectl create namespace argocd
# встановлюємо ArgoCd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
# перевіряємо статус  запущених pods argocd
 k get pods -n argocd
 ```
3. Налаштування web доступу до ArgoCd
```sh
# Щоб отримати доступ до ArgoCd можна скористатися одним з трьох варіантів 
- Service Type Load Balancer
- Ingress
- Port Forwarding
# 
kubectl port-forward svc/argocd-server -n argocd 8080:443&

```
4. Заходимо в ArgoCD за посиланням https://127.0.0.1:8080/
```sh
# Щоб отримати пароль користувача admin
 kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}"
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}"|base64 -d;echo  
```
6. 