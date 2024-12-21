**Задание 1. Yandex Cloud**

Что нужно сделать

1. Создать пустую VPC. Выбрать зону.

2. Публичная подсеть.

 - Создать в VPC subnet с названием public, сетью 192.168.10.0/24.

 - Создать в этой подсети NAT-инстанс, присвоив ему адрес 192.168.10.254. В качестве image_id использовать fd80mrhj8fl2oe87o4e1.

 - Создать в этой публичной подсети виртуалку с публичным IP, подключиться к ней и убедиться, что есть доступ к интернету.

3. Приватная подсеть.

- Создать в VPC subnet с названием private, сетью 192.168.20.0/24.

- Создать route table. Добавить статический маршрут, направляющий весь исходящий трафик private сети в NAT-инстанс.

- Создать в этой приватной подсети виртуалку с внутренним IP, подключиться к ней через виртуалку, созданную ранее, и убедиться, что есть доступ к интернету.

  

**Решение 1**

Устанавиливаем terraform, првоеряем работоспособность

![Image alt](https://github.com/mezhibo/devops2301/blob/3677544c46fe367a18d1470abd0703920ec9446a/IMG/1.jpg)

Создадим манифесты для всех ресурсов нашего окружения в Yandex Cloud


[locals.tf](https://github.com/mezhibo/devops2301/blob/f9674074e802b20e1a52436ce2930ac669af053c/IMG/locals.tf)

[network.tf](https://github.com/mezhibo/devops2301/blob/f9674074e802b20e1a52436ce2930ac669af053c/IMG/network.tf)

[output.tf](https://github.com/mezhibo/devops2301/blob/f9674074e802b20e1a52436ce2930ac669af053c/IMG/output.tf)

[provider.tf](https://github.com/mezhibo/devops2301/blob/f9674074e802b20e1a52436ce2930ac669af053c/IMG/provider.tf)

[vars.network.tf](https://github.com/mezhibo/devops2301/blob/f9674074e802b20e1a52436ce2930ac669af053c/IMG/vars.network.tf)

[vars.provider](https://github.com/mezhibo/devops2301/blob/f9674074e802b20e1a52436ce2930ac669af053c/IMG/vars.provider.tf)

[vars.vm](https://github.com/mezhibo/devops2301/blob/f9674074e802b20e1a52436ce2930ac669af053c/IMG/vars.vm.tf)

[vm](https://github.com/mezhibo/devops2301/blob/f9674074e802b20e1a52436ce2930ac669af053c/IMG/vm.tf)


Проинициализируем проект

![Image alt](https://github.com/mezhibo/devops2301/blob/f9674074e802b20e1a52436ce2930ac669af053c/IMG/2.jpg)


И создадим наши облачные ресурсы

![Image alt](https://github.com/mezhibo/devops2301/blob/f9674074e802b20e1a52436ce2930ac669af053c/IMG/3.jpg)

Перейдем в клауд и видим что все ресурсы удачно созданы


![Image alt](https://github.com/mezhibo/devops2301/blob/f9674074e802b20e1a52436ce2930ac669af053c/IMG/4.jpg)


![Image alt](https://github.com/mezhibo/devops2301/blob/f9674074e802b20e1a52436ce2930ac669af053c/IMG/5.jpg)



Видим что создалась таблица маршрутизации


![Image alt](https://github.com/mezhibo/devops2301/blob/f9674074e802b20e1a52436ce2930ac669af053c/IMG/6.jpg)


Подключимся к публичной машине vm-public с внешним ip-адресом и проверим на ней наличии интернета


![Image alt](https://github.com/mezhibo/devops2301/blob/f9674074e802b20e1a52436ce2930ac669af053c/IMG/7.jpg)


Подключимся к нашей NAT-машине nat-instance-vm-01 и проверим с нее доступ в интернет


![Image alt](https://github.com/mezhibo/devops2301/blob/f9674074e802b20e1a52436ce2930ac669af053c/IMG/8.jpg)


Добавим закрытый ключ id_rsa под которым мы подключаемся к удаленным машинам на нашу nat-вм для возможности подключения к вм в приватной сети


![Image alt](https://github.com/mezhibo/devops2301/blob/f9674074e802b20e1a52436ce2930ac669af053c/IMG/9.jpg)


Теперь подключимся к нашей ВМ не имеющей внешнего ip-адреса и проверим с нее доступ в интернет через нашу NAT-вм



![Image alt](https://github.com/mezhibo/devops2301/blob/f9674074e802b20e1a52436ce2930ac669af053c/IMG/10.jpg)


И видим что пинги проходят.





