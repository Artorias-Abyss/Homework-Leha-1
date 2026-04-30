> [!INFO] Этап 1. Подготовка к началу проведения выполнения

## Устанавливаем пакеты :

```bash
sudo apt update
sudo apt install -y redis-server docker.io python3-venv python3-pip ansible git curl jq neofetch fish
```
---
## Доп настройки (Что бы Docker работал без `sudo`)

```bash
sudo usermod -aG docker $USER
```
### После этого нужно выйти и зайти заново или выполнить:

```bash
newgrp docker
```
## Авто запуск сервисов

```bash
sudo systemctl enable --now redis-server 
sudo systemctl enable --now docker
```
## Проверка установки

```bash
redis-cli ping         # должен ответить PONG
docker --version       # версия Docker
python3 -m venv --help # справка venv
ansible --version      # версия Ansible
docker run --rm hello-world  # Ожидаемый вывод: "Hello from Docker!"
```

> [!INFO] Этап 2. Подготовка к началу проведения выполнения