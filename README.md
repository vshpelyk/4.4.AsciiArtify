# 4.4.AsciiArtify
### K3d ###

1. Встановлення K3d
   ```sh
   wget -q -O - https://raw.githubusercontent.com/rancher/k3d/main/install.sh | bash
   or
   ```
   ```sh
   curl -s https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash
   ```
2. Створити/видалити кластер
    ```sh
    k3d cluster create demo
    k3d cluster create demo --servers 3 
    k3d cluster delete demo
    ```
    видалити всі кластера
    ```sh
    k3d cluster delete -a
    ```
3. Преглянути створені ноди 
    ```sh
    kubectl get nodes
    ```
4. Створити тестовий deployment - hello-world
    ```sh
    kubectl create deployment hello-world --image=vshpelyk/k8sphp:latest
    перевірити створений deployment
    kubectl get pods


    ```
5. Створюємо тестовий service - hello-world та надаємо доступ до deploy hello-world
   ```sh
    kubectl expose deployment hello-world --type=LoadBalancer --port=8080
    отримати список сервісів
    kubectl get services
    видалити service
    kubectl delete service hello-world

   ```
