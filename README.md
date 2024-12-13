# Домашнее задание к занятию 1 «Введение в Ansible»

### Подготовка к выполнению

Установите Ansible версии 2.10 или выше.

Создайте свой публичный репозиторий на GitHub с произвольным именем.

Скачайте Playbook из репозитория с домашним заданием и перенесите его в свой репозиторий.

### Основная часть

1. Попробуйте запустить playbook на окружении из test.yml, зафиксируйте значение, которое имеет факт some_fact для указанного хоста при выполнении playbook.

![alt text](https://github.com/MaratKN/08-ansible-01-base/blob/main/1.png)

2. Найдите файл с переменными (group_vars), в котором задаётся найденное в первом пункте значение, и поменяйте его на all default fact.

sed -i 's/12/all default fact/g'  ./group_vars/all/examp.yml

![alt text](https://github.com/MaratKN/08-ansible-01-base/blob/main/2.png)

3. Воспользуйтесь подготовленным (используется docker) или создайте собственное окружение для проведения дальнейших испытаний.

sudo docker compose -f /home/marat/ansible/08-ansible-01-base/docker/compose.yaml up -d

![alt text](https://github.com/MaratKN/08-ansible-01-base/blob/main/3.png)

4. Проведите запуск playbook на окружении из prod.yml. Зафиксируйте полученные значения some_fact для каждого из managed host.

sudo ansible-playbook -i /home/marat/ansible/08-ansible-01-base/playbook/inventory/prod.yml /home/marat/ansible/08-ansible-01-base/playbook/site.yml 

![alt text](https://github.com/MaratKN/08-ansible-01-base/blob/main/4.png)

5. Добавьте факты в group_vars каждой из групп хостов так, чтобы для some_fact получились значения: для deb — deb default fact, для el — el default fact.

sed -i 's/deb/deb default fact/g' /home/marat/ansible/08-ansible-01-base/playbook/group_vars/deb/examp.yml

sed -i 's/el/el default fact/g' /home/marat/ansible/08-ansible-01-base/playbook/group_vars/el/examp.yml 

6. Повторите запуск playbook на окружении prod.yml. Убедитесь, что выдаются корректные значения для всех хостов.

![alt text](https://github.com/MaratKN/08-ansible-01-base/blob/main/5.png)

7. При помощи ansible-vault зашифруйте факты в group_vars/deb и group_vars/el с паролем netology.

sudo ansible-vault encrypt /home/marat/ansible/08-ansible-01-base/playbook/group_vars/el/examp.yml

sudo ansible-vault encrypt /home/marat/ansible/08-ansible-01-base/playbook/group_vars/deb/examp.yml

![alt text](https://github.com/MaratKN/08-ansible-01-base/blob/main/7.png)

8. Запустите playbook на окружении prod.yml. При запуске ansible должен запросить у вас пароль. Убедитесь в работоспособности.

sudo ansible-playbook -i /home/marat/ansible/08-ansible-01-base/playbook/inventory/prod.yml /home/marat/ansible/08-ansible-01-base/playbook/site.yml --ask-vault-pass

![alt text](https://github.com/MaratKN/08-ansible-01-base/blob/main/8.png)

9. Посмотрите при помощи ansible-doc список плагинов для подключения. Выберите подходящий для работы на control node.

ansible-doc -l

Плагин: ansible.builtin.local.

10. В prod.yml добавьте новую группу хостов с именем local, в ней разместите localhost с необходимым типом подключения.

11. Запустите playbook на окружении prod.yml. При запуске ansible должен запросить у вас пароль. Убедитесь, что факты some_fact для каждого из хостов определены из верных group_vars.

sudo ansible-playbook -i /home/marat/ansible/08-ansible-01-base/playbook/inventory/prod.yml /home/marat/ansible/08-ansible-01-base/playbook/site.yml --ask-vault-pass

![alt text](https://github.com/MaratKN/08-ansible-01-base/blob/main/10.png)

12. Заполните README.md ответами на вопросы. Сделайте git push в ветку master. В ответе отправьте ссылку на ваш открытый репозиторий с изменённым playbook и заполненным README.md.

13. Предоставьте скриншоты результатов запуска команд.




