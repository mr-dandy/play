# infra


## BETA Мастер-репа Ansible для управления инфраструктурой linux 

Содержание репозитория:

- plays/ - список плейбуков. Скачивается как зависимость reqs/plays.yml из https://gitlab.eksmo-office.ru/iac/ansible/playbooks 
- roles/ - список ролей. Скачивается как зависимость reqs/roles.yml из https://gitlab.eksmo-office.ru/iac/ansible/roles
- reqs/ - списки зависимостей. Скачать зависимости: ```ansible-playbook reqs/install.yml```


## Начало работы

Перед использованием нужно подготовить рабочее место. Чтобы не страдать в будущем из-за поломанного питона или зависимостей, рекомендую пользоваться *venv*

```bash
# создаем место для наших окружений
mkdir -p ~/work/venvs/

# создаем окружение под ансибл
python3 -m venv ~/work/venvs/ansible-env

# активируем окружение
source ~/work/venvs/ansible-env/bin/activate

# устанавливаем ansble внутри окружения
pip3 install -r reqs/requirements.txt

# Скачиваем зависимости
ansible-playbook reqs/install.yml

# Создаем файлик с ключом от ansible-vault чтобы не вводить постоянно пароль при запуске плейбуков
echo "MEGAPASS" > ~/.ssh/ansible-vault-pass

# деактивация окружения
deactivate
```

для удобства можно на активацию окружения настроить alias
```bash
alias vaa="source ~/work/venvs/ansible-env/bin/activate"
```

## Использование

перед запуском убеждаемся в актуальности всех зависимостей ```ansible-playbook reqs/install.yml```

примеры:
```bash
# запускаем без изменений
ansible-playbook -i plays/all-hosts/inventory/inventory.yml plays/all-hosts/main.yml --check

# если изменения валидные то запускаем без --check
ansible-playbook -i plays/all-hosts/inventory/inventory.yml plays/all-hosts/main.yml

# можно ограничить раскатку по группе или имени хоста в переметре -l 'host1,host2' или -l 'group1,group2'
ansible-playbook -i plays/all-hosts/inventory/inventory.yml plays/all-hosts/main.yml -l 'co-test-sergey'
```
