# Домашнее задание к занятию "Система мониторинга Zabbix" - `Важинский Виктор`
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

### Задание 1
Задание 1
Установите Zabbix Server с веб-интерфейсом.


Прикрепите в файл README.md скриншот авторизации в админке.

![zabbix](https://github.com/Victor3359995/gitlab-hw1/blob/main/img/Zabbix%20%D0%B0%D0%B2%D1%82%D0%BE%D1%80%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F.jpg) 
![zabbix](https://github.com/Victor3359995/gitlab-hw1/blob/main/img/Zabbix%20UI.jpg)

### Задание 2
Установите Zabbix Agent на два хоста.

Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу

![zabbix](https://github.com/Victor3359995/gitlab-hw1/blob/main/img/Zabbix%20hosts.jpg)
Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером

![zabbix](https://github.com/Victor3359995/gitlab-hw1/blob/main/img/systemctl%20status.jpg)

![zabbix](https://github.com/Victor3359995/gitlab-hw1/blob/main/img/zabbix_agent_log.jpg)

![zabbix](https://github.com/Victor3359995/gitlab-hw1/blob/main/img/systemctl%20status%20is%20woking%20again.jpg)

Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.

![zabbix](https://github.com/Victor3359995/gitlab-hw1/blob/main/img/Latest%20data.jpg)







