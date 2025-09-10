# Momo-store - Пельменная №2

## Как запустить проект? 

```bash

git clone https://github.com/Vulkii/cloud-services-engineer-docker-project-sem2.git
cd cloud-services-engineer-docker-project-sem2
docker-compose up -d

```

## Как проверить работоспособность проекта?

```bash
sudo docker ps # В Status должно быть Uptime + (healthy) у обоих контейнеров

Открыть в браузере http://localhost:80

```

## Размер образов
Размеры образов:
docker-project-frontend - 50MB
docker-project-backend - 24.7MB

Достигнуто это с помощью multi-stage сборок.
Backend: Используется минимально базовый образ alpine linux + образ содержит только исполняемый файл
Frontend: Используетя минимально базовый образ alpine linux
Установки зависимостей кэшируются, сборка триггерится только при изменении исходного кода.