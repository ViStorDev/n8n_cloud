# 1. Встановіть Git
```bash
sudo apt install git
sudo apt install docker
```
# 2. Оновіть список пакетів і встановіть необхідні утиліти
```bash
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
```
# 3. Додайте ключ GPG для офіційного репозиторію Docker
```bash
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```
# 4. Додайте репозиторій Docker до APT
```bash
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
# 5. Оновіть список пакетів APT ще раз
```bash
sudo apt-get update
```
# 6. Встановіть Docker Engine, containerd та Docker Compose
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo apt-get update
sudo apt-get install docker.io docker-compose
sudo usermod -aG docker vi_stor_dev
newgrp docker
```
# 7. Клонуйте репозиторій в деректорію на сервері.
```bash
git clone https://github.com/ViStorDev/n8n_cloud.git
```
# 8. Надайте права на файл acme.json доя traefik
```bash
sudo truncate -s 0 ./traefik_data/acme.json
chmod 600 ./traefik_data/acme.json
```
# 9. Для запуску міграцій:
```bash
# Використовуйте профіль migration, щоб запустити n8n_main для оновлення бази даних.
docker compose --profile migration up --force-recreate
```
# 10. Для запуску робочого середовища:
```bash
# Використовуйте профіль main, щоб запустити n8n у повноцінному робочому режимі (з n8n_main та n8n_worker).
docker compose --profile main up -d
```
# n8n_worker
Воркер який запускажтся нм іншій віртуальній машині і підключаєтся до черги Redis 
для безпеки бажано щоб віртуальні машини знаходились в олній приватній мережі або в одному проекті Google cloud 
На машині для worker виконайте кроки 1-5. Або створіть .sh скрипт.
* supabase Connection String 
Session pooler
