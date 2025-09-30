# supabase Connection String 
Session pooler
#Git
sudo apt install git
sudo apt install docker
# 1. Оновіть список пакетів і встановіть необхідні утиліти
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
# 2. Додайте ключ GPG для офіційного репозиторію Docker
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
# 3. Додайте репозиторій Docker до APT
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
# 4. Оновіть список пакетів APT ще раз
sudo apt-get update
# 5. Встановіть Docker Engine, containerd та Docker Compose
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo apt-get update
sudo apt-get install docker.io docker-compose
sudo usermod -aG docker vi_stor_dev
newgrp docker
sudo truncate -s 0 ./traefik_data/acme.json
chmod 600 ./traefik_data/acme.json
# 1. Для запуску міграцій:
# Використовуйте профіль migration, щоб запустити n8n_main для оновлення бази даних.
docker compose --profile migration up --force-recreate
# 2. Для запуску робочого середовища:
# Використовуйте профіль main, щоб запустити n8n у повноцінному робочому режимі (з n8n_main та n8n_worker).
docker compose --profile main up -d
