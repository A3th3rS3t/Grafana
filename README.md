# Grafana
Эта конфигурация предназначена для развертывания системы мониторинга Grafana с использованием Docker Compose.

## 1. Подготовка окружения
Убедитесь, что у вас установлены `Docker` и `Docker Compose`, если нет воспользуйтесь следующей инструкцией: https://docs.docker.com/engine/install/

Убедитесь, что `Git` установлен. Если нет, установите его: https://git-scm.com/downloads

## 2. Клонирование репозитория
Перейдите в директорию, в которой вы хотите развернуть Zabbix:
```bash
cd /opt/docker/
```
Клонируйте репозиторий с GitHub:
```bash
git clone https://github.com/A3th3rS3t/Grafana.git
```
```bash
cd Grafana
```
В репозитории должны быть файлы `docker-compose.yaml` и `.env`.

## 3. Запуск сервисов через Docker Compose
В директории с проектом выполните команду для запуска сервисa:
```bash
docker compose up -d
```
Это запустит контейнер:
```bash
grafana_app — сервис grafana.
```
После выдаем права приложению на запись, для возможности создания таблиц в `volumes`:
```bash
chmod 775 volumes/grafana-storage
```

## 4. Проверка работоспособности
Откройте браузер и перейдите по адресу: localhost:3000 (или другой порт, если вы изменили его в docker-compose.yaml)

Стандартные данные для входа:
```
log: admin
pass: admin
```

Если что-то не работает, проверьте логи контейнеров:
```bash
docker logs grafana_app
```

## 5. Остановка и удаление сервисов
Если вам нужно изменить порты или другие параметры, отредактируйте файл 
docker-compose.yaml и перезапустите сервисы:
```bash
docker compose down
docker compose up -d
```

## Postscriptum
Если нужно править `grafana.ini`, то предварительно копируем файл в `volumes`:
```bash
docker cp grafana_app:/etc/grafana/grafana.ini /opt/docker/grafana/volumes/grafana.ini
```
После снимаем комментарий с строчки в `docker-compose.yml`
