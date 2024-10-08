### Домашнее задание к занятию 3 «Использование Ansible»
## Подготовка к выполнению
Для выполнения ДЗ я создаю 3 виртуальные машины в Yandex.Cloud с использованием Terraform.
Код Terraform доступен по ссылке: [https://github.com/slava1005/08_ansible_03/tree/main/terraform]

## Основная часть
```
1. Допишите playbook: нужно сделать ещё один play, который устанавливает и настраивает LightHouse.
2. При создании tasks рекомендую использовать модули: get_url, template, yum, apt.
3 .Tasks должны: скачать статику LightHouse, установить Nginx или любой другой веб-сервер, настроить его конфиг для открытия LightHouse, запустить веб-сервер.
4. Подготовьте свой inventory-файл prod.yml.
5. Запустите ansible-lint site.yml и исправьте ошибки, если они есть.
6. Попробуйте запустить playbook на этом окружении с флагом --check.
7. Запустите playbook на prod.yml окружении с флагом --diff. Убедитесь, что изменения на системе произведены.
8. Повторно запустите playbook с флагом --diff и убедитесь, что playbook идемпотентен.
9. Подготовьте README.md-файл по своему playbook. В нём должно быть описано: что делает playbook, какие у него есть параметры и теги.
Готовый playbook выложите в свой репозиторий, поставьте тег 08-ansible-03-yandex на фиксирующий коммит, в ответ предоставьте ссылку на него.
```
## Решение:
1-3. Дописываю еще один play, который устанавливает LightHouse. Используем модули get_url, template, yum, service, file. 
Происходит установка и конфигурирование веб-сервера Nginx, установка и конфигурирование LightHouse, запуск служб Nginx и LightHouse.

4. Подготовил свой inventory-файл prod.yml:

![1](https://github.com/user-attachments/assets/fdfc750e-78dd-4f71-9fa1-5ceb8e272ad2)

>>> При поготовке к запуску не забываем поправить ip созданных с помощью terraform машин на актуальные в файлах playbook/group_vars/vector/vars.yml и playbook/inventory/prod.yml!!!!!! 

5. Запускаю ansible-lint site.yml ... и сразу получаем квест по исправлению ошибок в использовании старых наименований модулей, отсутствии прав на скачиваемые или создаваемые файлы.

6. Запускаю playbook с флагом --check. Снова ыполнение playbook завершилось с ошибкой, тут понятно, этот флаг не вносит изменения в системы, а выполнение playbook требует скачивания и установки пакетов приложений.

7. Запускаю playbook на prod.yml окружении с флагом --diff. Изменения в систему внесены:
![2](https://github.com/user-attachments/assets/a75ccac5-a806-43ab-a82b-f9c733f10933)



8. Повторно запускаю playbook с флагом --diff. Playbook идемпотентен, изменения связаны с перезапуском сервиса Vector:
![3](https://github.com/user-attachments/assets/d3972ebe-6e21-499d-b1a9-cde558ca4f0a)


9. Подготовил README.md-файл по своему playbook доступный по ссылке [https://github.com/slava1005/08_ansible_03/blob/main/playbook/README.md]
