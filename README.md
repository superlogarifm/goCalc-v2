# goCalc-v2

<div align="center">
  <img src="https://img.shields.io/badge/Go-1.20+-00ADD8?style=for-the-badge&logo=go&logoColor=white" alt="Go 1.20+"/>
  <img src="https://img.shields.io/badge/Docker-Supported-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker Supported"/>
  <img src="https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge" alt="MIT License"/>
</div>

## 📋 Описание проекта

**goCalc-v2** - это распределенный калькулятор, реализованный на языке Go. Проект состоит из оркестратора, который распределяет вычислительные задачи между агентами, и агентов, выполняющих математические операции.

## 🔧 Требования

- Go 1.20 или выше
- Docker и Docker Compose (для запуска в контейнерах, необязательно)
- Git

## 🚀 Установка

### Клонирование репозитория

```bash
git clone https://github.com/superlogarifm/goCalc-v2.git
cd goCalc-v2
```

### Установка зависимостей

```bash
go mod download
```

## ▶️ Запуск проекта

### Локальный запуск

#### Запуск оркестратора

```bash
go run cmd/orchestrator/main.go
```

#### Запуск агента

```bash
go run cmd/agent/main.go
```

### Запуск с использованием Docker Compose

Для запуска всех компонентов системы в Docker-контейнерах:

```bash
docker-compose up --build
```

Для запуска в фоновом режиме:

```bash
docker-compose up -d --build
```

## 🔐 Переменные окружения

### Оркестратор

| Переменная | Описание | Значение по умолчанию |
|------------|----------|------------------------|
| `TIME_ADDITION_MS` | Время выполнения операции сложения в мс | 5000 |
| `TIME_SUBTRACTION_MS` | Время выполнения операции вычитания в мс | 5000 |
| `TIME_MULTIPLICATIONS_MS` | Время выполнения операции умножения в мс | 5000 |
| `TIME_DIVISIONS_MS` | Время выполнения операции деления в мс | 5000 |

### Агент

| Переменная | Описание | Пример значения |
|------------|----------|-----------------|
| `ORCHESTRATOR_URL` | URL оркестратора | http://localhost:8080 |
| `COMPUTING_POWER` | Вычислительная мощность агента | 2 |

## 📡 API и отправка запросов

Поддерживаемые операции:
- `addition` - сложение
- `subtraction` - вычитание
- `multiplication` - умножение
- `division` - деление

### Отправка математических выражений

#### Запрос на выполнение выражения

```bash
curl --location 'localhost:8080/api/v1/calculate' --header 'Content-Type: application/json' --data '{"expression": "2+2*2"}'
```

#### Пример ответа

```json
{
  "id": "1",
  "expression": "2+2*2",
  "status": "processing"
}
```

### Получение статуса выражения

```bash
curl --location 'localhost:8080/api/v1/expressions/1'
```

#### Пример ответа

```json
{
  "id": "1",
  "expression": "2+2*2",
  "status": "completed",
  "result": 6,
}
```
## ⚠️ Устранение неполадок

### Проблемы с подключением к оркестратору

Убедитесь, что оркестратор запущен и доступен по указанному URL. При использовании Docker проверьте, что контейнеры запущены:

```bash
docker-compose ps
```

### Логи контейнеров

Для просмотра логов контейнеров:

```bash
docker-compose logs orchestrator
docker-compose logs agent1
docker-compose logs agent2
```

 
