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
5. Створюємо додаток в ArgoCD за допомогою графічного інтерфейсу
![ArgoDC](https://github.com/vshpelyk/4.4.AsciiArtify/blob/main/doc/create-argocd.png)
![ArgoDC](https://github.com/vshpelyk/4.4.AsciiArtify/blob/main/doc/create-argocd2.png)
   - 1 Створюємо новий проект
   - 2 Назва для проекту
   - 3 Проект до якого належить додаток (по замовчуванню)
   - 4 Шлях до репозиторію з яким буде синхронізація (https://github.com/den-vasyliev/go-demo-app )
   - 5 Шлях до каталога я якому лежать маніфест файли для K8s
   - 6 Вибираємо локальний кластер
   - 7 Створюємо нове namespace - demo, потрібно поставити галояку auto-create namespace
6. Синхронізація застосунку
   ![ArgoDC](https://github.com/vshpelyk/4.4.AsciiArtify/blob/main/doc/create-argocd3.png)
7. Перевірка стану застосунка в кластері
![ArgoDC](https://github.com/vshpelyk/4.4.AsciiArtify/blob/main/doc/create-argocd4.png)

8. Демо створення застосунку в ArgoCD
![Приклад](https://github.com/vshpelyk/4.4.AsciiArtify/blob/main/doc/poc.gif)
