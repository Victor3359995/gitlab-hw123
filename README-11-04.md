
# Домашнее задание к занятию "Очереди RabbitMQ" - `Важинский`
-- 

### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1. Установка RabbitMQ

Используя Vagrant или VirtualBox, создайте виртуальную машину и установите RabbitMQ.
Добавьте management plug-in и зайдите в веб-интерфейс.

*Итогом выполнения домашнего задания будет приложенный скриншот веб-интерфейса RabbitMQ.*

![Interface](./img/interface.jpg)

---

### Задание 2. Отправка и получение сообщений

Используя приложенные скрипты, проведите тестовую отправку и получение сообщения.
Для отправки сообщений необходимо запустить скрипт producer.py.

Для работы скриптов вам необходимо установить Python версии 3 и библиотеку Pika.
Также в скриптах нужно указать IP-адрес машины, на которой запущен RabbitMQ, заменив localhost на нужный IP.

```shell script
$ pip install pika
```

Зайдите в веб-интерфейс, найдите очередь под названием hello и сделайте скриншот.
После чего запустите второй скрипт consumer.py и сделайте скриншот результата выполнения скрипта

*В качестве решения домашнего задания приложите оба скриншота, сделанных на этапе выполнения.*

Для закрепления материала можете попробовать модифицировать скрипты, чтобы поменять название очереди и отправляемое сообщение.

Очередь в веб-интерфейсе после выполнения скрипта producer.py:

![producer](./img/queue1.jpg)

Очередь в веб-интерфейсе после выполнения скрипта consumer.py:

![consumer](./img/consumer.jpg)
![consumer](./img/consumer1.jpg)

Консоль:

![consol](./img/cmdreceive.jpg)

---

### Задание 3. Подготовка HA кластера

Используя Vagrant или VirtualBox, создайте вторую виртуальную машину и установите RabbitMQ.
Добавьте в файл hosts название и IP-адрес каждой машины, чтобы машины могли видеть друг друга по имени.

Пример содержимого hosts файла:
```shell script
$ cat /etc/hosts
192.168.0.10 rmq01
192.168.0.11 rmq02
```
После этого ваши машины могут пинговаться по имени.

Затем объедините две машины в кластер и создайте политику ha-all на все очереди.

*В качестве решения домашнего задания приложите скриншоты из веб-интерфейса с информацией о доступных нодах в кластере и включённой политикой.*

Также приложите вывод команды с двух нод:

```shell script
$ rabbitmqctl cluster_status
```

Для закрепления материала снова запустите скрипт producer.py и приложите скриншот выполнения команды на каждой из нод:

```shell script
$ rabbitmqadmin get queue='hello'
```

После чего попробуйте отключить одну из нод, желательно ту, к которой подключались из скрипта, затем поправьте параметры подключения в скрипте consumer.py на вторую ноду и запустите его.

*Приложите скриншот результата работы второго скрипта.*

---

Прописываем соответствия ip-адреса доменному имени:

```shell script
$ cat /etc/hosts
echo "192.168.1.105 rabbit1" >> /etc/hosts
echo "192.168.1.88 rabbit2" >> /etc/hosts
```

Для работы кластера RabbitMQ все узлы, участвующие в кластере, должны иметь одинаковые файлы cookie.
Скопируем содержимое файла Cookie с первой (main) машины (ноды) на вторую, которую будем добавлять в кластер. Файл Cookie находится здесь: /var/lib/rabbitmq/.erlang.cookie.

На второй ноде (rabbit2) перезапустим службу:

```shell script
systemctl restart rabbitmq-server
```

Остановим и сбросим приложение:

```shell script
rabbitmqctl stop_app
rabbitmqctl reset
```

Подключим к кластеру и запустим:

```shell script
rabbitmqctl join_cluster rabbit@rabbit1
rabbitmqctl start_app
```

На ноде1 (rabbit1) cоздаем политику, которая позволяет зеркалить очереди для всех узлов в кластере:

```shell script
rabbitmqctl set_policy ha-all ".*" '{"ha-mode":"all"}'  
```

![rabbit1](./img/cluster.jpg)
![rabbit1](./img/policies.jpg)

![status1](./img/cl_status1.jpg)
![status2](./img/cl_status2.jpg)

Устанавливаем и запускаем утилиту rabbitmqadmin:

![rabbitadmin](./img/rma2.jpg)
![rabbitadmin](./img/rma1.jpg)

![notrun](./img/not_run.jpg)

Выполнение скрипта consumer.py на погашенной ноде1 - rabbit1:

![notrun](./img/last_cinsumer.jpg)

--- 
