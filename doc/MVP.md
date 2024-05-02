## MVP (Minimum Viable Product) ##
-----------
### Запуск застосунку ###

- переадресуємо порти командою
```sh
kubectl port-forward -n demo svc/ambassador 8081:80
```
- зробимо запит на вказаний порт 
```sh
curl localhost:8081
```
- завантажимо картинку і завантажемо її в застосунок 
```sh
wget -O /tmp/g.png https://img2.gratispng.com/20180406/xhq/kisspng-computer-icons-house-window-blinds-shades-brookl-adress-5ac7dd63724750.6622363615230477794681.jpg

curl -F 'image=@/tmp/g.png' localhost:8081/img/
```
- отримуємо результат
 ![Результат](https://github.com/vshpelyk/4.4.AsciiArtify/blob/main/doc/mvp1.png)

 - Презентація 
  ![Приклад](https://github.com/vshpelyk/4.4.AsciiArtify/blob/main/doc/mvp.gif)
