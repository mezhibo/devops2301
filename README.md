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


[locals.tf[]()](https://github.com/mezhibo/devops2301/blob/3677544c46fe367a18d1470abd0703920ec9446a/IMG/locals.tf)

[network.tf](https://github.com/mezhibo/devops2301/blob/3677544c46fe367a18d1470abd0703920ec9446a/IMG/network.tf)

[output.tf](https://github.com/mezhibo/devops2301/blob/3677544c46fe367a18d1470abd0703920ec9446a/IMG/output.tf)

[provider.tf](https://github.com/mezhibo/devops2301/blob/3677544c46fe367a18d1470abd0703920ec9446a/IMG/provider.tf)

[vars.network.tf](https://github.com/mezhibo/devops2301/blob/3677544c46fe367a18d1470abd0703920ec9446a/IMG/vars.network.tf)

[vars.provider](https://github.com/mezhibo/devops2301/blob/3677544c46fe367a18d1470abd0703920ec9446a/IMG/vars.provider.tf)

[vars.vm](https://github.com/mezhibo/devops2301/blob/3677544c46fe367a18d1470abd0703920ec9446a/IMG/vars.vm.tf)

[vm](https://github.com/mezhibo/devops2301/blob/3677544c46fe367a18d1470abd0703920ec9446a/IMG/vm.tf)


Проинициализируем проект

![Image alt](скрин2)


И создадим наши облачные ресурсы

![Image alt](скрин3)

Перейдем в клауд и видим что все ресурсы удачно созданы


![Image alt](скрин4)


![Image alt](скрин5)



Видим что создалась таблица маршрутизации


![Image alt](скрин6)


Подключимся к публичной машине vm-public с внешним ip-адресом и проверим на ней наличии интернета


![Image alt](скрин7)


Подключимся на nat-instance-vm-01 и проверим с нее доступ в интернет


![Image alt](скрин8)




