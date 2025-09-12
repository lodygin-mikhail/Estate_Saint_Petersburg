# 🏠 Предсказание стоимости недвижимости Санкт-Петербурга / Real Estate Price Prediction in Saint-Petersburg

Проект для предсказания стоимости недвижимости в Санкт-Петербурге с использованием машинного обучения. Включает полный цикл: от анализа данных до интерактивного веб-приложения.

## 📊 О проекте

Этот проект представляет собой end-to-end решение для предсказания цен на недвижимость в Санкт-Петербурге. Система включает:

- **Полный EDA и предобработку** данных
- **Обучение нескольких ML-моделей** с выбором лучшей
- **REST API** на FastAPI для предсказаний
- **Интерактивный интерфейс** на Streamlit
- **Docker-контейнеризацию** для простого развертывания

## 🚀 Быстрый старт

### Предварительные требования

- Docker
- Docker Compose
- Python 3.9+ (для локальной разработки)

### Запуск через Docker Compose

```bash
# Клонируйте репозиторий
git clone https://github.com/lodygin-mikhail/Real_Estate_Saint_Petersburg.git
cd Real_Estate_Saint_Petersburg

# Запустите все сервисы
docker-compose up -d

# Или с выводом логов
docker-compose up
```

После запуска сервисы будут доступны:

**FastAPI API:** http://localhost:5000

**Streamlit App:** http://localhost:8501

**FastAPI Docs:** http://localhost:5000/docs

## 📁 Структура проекта

```text
spb-real-estate-prediction/
├── fastapi_service/             # FastAPI сервис
│   ├── fastapi_app.py           # Основное FastAPI приложение
│   ├── requirements.txt
│   └── Dockerfile
├── streamlit_app/               # Streamlit интерфейс
│   ├── streamlit_app.py
│   ├── requirements.txt
│   └── Dockerfile
├── model_train/                 # Jupyter ноутбуки
│   ├── data/
│   │   └── Spb_flats_prices.csv # Исходный csv файл
│   ├── main.ipynb               # Предобработка, EDA и обучение моделей
│   └── requirements.txt   
├── data/                        # Данные
│   ├── features/                # Уникальные значения полей
│   └── pipeline/                # Лучший пайплайн
├── docker-compose.yml
└── README.md
```

## 🔌 API Endpoints

### **Предсказание цены**
**POST** `/predict`

**Тело запроса:**
```json
{
    "flat_status": false,
    "num_of_rooms": 2,
    "total_area_m2": 45.5,
    "living_area_m2": 28.0,
    "kitchen_area_m2": 10.5,
    "floor": 5,
    "metro_station": "Площадь Восстания",
    "minutes_to_metro": 15,
    "transfer_type": "пешком",
    "house_age": 20,
    "is_future_building": false
}
```
**Ответ:**
```json
{
  "prediction": {
    "price": 7610252.757031128
  }
}
```
### Другие endpoints
- **GET** `/` - Информация о API
- **GET** `/health` - Проверка здоровья сервиса

## 📸 Интерфейс Streamlit приложения
### 1. Форма ввода параметров
![screenshot](/images/streamlit_app.png)
_Интерфейс для ввода характеристик недвижимости с выпадающими списками и ползунками ввода_
### 2. Результат предсказания
![screenshot](/images/streamlit_app_2.png)
_Отображение предсказанной цены после нажатия кнопки "Предсказать цену"_

## 🛠️ Локальная разработка

### Установка зависимостей для каждого сервиса
```bash
# Установка зависимостей FastAPI
cd fastapi_service
pip install -r requirements.txt

# Установка зависимостей Streamlit
cd streamlit_service
pip install -r requirements.txt

# Установка зависимостей для обучения
cd model_train
pip install -r requirements.txt
```

### Запуск FastAPI локально
```bash
cd fastapi_service
uvicorn fastapi_app:app --reload --host 0.0.0.0 --port 5000
```

### Запуск Streamlit локально
```bash
cd streamlit_service
streamlit run streamlit_app.py
```

## 🐳 Docker команды
```bash
# Сборка и запуск всех сервисов
docker-compose up --build

# Сборка и запуск конкретного сервиса
docker-compose up --build fastapi_app
docker-compose up --build streamlit_app

# Остановка сервисов
docker-compose down

# Просмотр логов
docker-compose logs -f
docker-compose logs fastapi_app
docker-compose logs streamlit_app
```

## 📜 Лицензия
MIT License © 2025
