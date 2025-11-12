# Ansible Homework

## Описание

Этот репозиторий содержит решения для домашнего задания по продвинутым концепциям Ansible. Каждый плейбук демонстрирует определенную концепцию:

- `task1_tags.yml`: Управление веб-приложением с использованием тегов.
- `task2_blocks.yml`: Безопасное обновление с автоматическим откатом при ошибках.
- `task3_delegation.yml`: Последовательное обновление серверов через load balancer.
- `task4_complex.yml`: Комплексный CI/CD pipeline для микросервисов.

## Требования

- **Ansible**: 2.9+
- **ОС**: Ubuntu/Debian (для работы с apt)
- **Пакеты**: `python3`, `python3-pip`, `nginx`, `python3-venv`

## Инструкции

### Настройка inventory

Файл `inventory/hosts` настроен для работы с localhost. Для `task3_delegation.yml` используются разные порты для эмуляции нескольких серверов. Убедитесь, что у вас есть доступ по SSH к этим хостам или измените inventory для вашей среды.

### Примеры команд

**Задание 1:**
```bash
# Полная установка
ansible-playbook -i inventory/hosts playbooks/task1_tags.yml

# Только установка пакетов
ansible-playbook -i inventory/hosts playbooks/task1_tags.yml --tags "packages"

# Обновление без переустановки пакетов
ansible-playbook -i inventory/hosts playbooks/task1_tags.yml --skip-tags "packages"
```

**Задание 2:**
```bash
# Успешное обновление
ansible-playbook -i inventory/hosts playbooks/task2_blocks.yml

# Неуспешное обновление (с откатом)
ansible-playbook -i inventory/hosts playbooks/task2_blocks.yml -e "simulate_error=true"
```

**Задание 3:**
```bash
# Последовательное обновление
ansible-playbook -i inventory/hosts playbooks/task3_delegation.yml
```

**Задание 4:**
```bash
# Полный деплой
ansible-playbook -i inventory/hosts playbooks/task4_complex.yml -e "version=v1.2.0"

# Деплой одного сервиса
ansible-playbook -i inventory/hosts playbooks/task4_complex.yml --tags "deploy-service1"

# Откат
ansible-playbook -i inventory/hosts playbooks/task4_complex.yml --tags "rollback"
```

## Демонстрация

Для демонстрации работы плейбуков можно использовать Docker или выполнять их на localhost. Вывод команд покажет последовательность выполнения задач, а в случае ошибок – срабатывание механизмов отката.
