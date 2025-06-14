# 🤖 AI-парсер решений решений арбитражных судов, загружаемых из Kontur.Focus

**Проект для автоматического анализа судебных документов с помощью локальной LLM (GPT4All).**  
Извлекает решения арбитражных судов, фильтрует по региону (Санкт-Петербург) и генерирует краткие пересказы с указанием сторон и итогов дела.

> ⚠️ **Важно**: 1) Код предназначен только для образовательных целей (с учётом лицензионных и других юридических аспектов). 2) Нужен платный аккаунт "Контур. Фокуса" для его работы.

---

## 🔧 Технологии
- **Парсинг**: `BeautifulSoup4`, `PyPDF2`, `requests`  
- **AI-обработка**: Локальная модель `GPT4All` (saiga_yandexgpt_8b)  
- **Хранение данных**: Pandas + CSV (через кастомный модуль `vkp_db`)  
- **Безопасность**: Конфиг-файл user_data.py  

---

## 🚀 Быстрый старт

### 1. Установка зависимостей
```bash
pip install -r requirements.txt
```

### 2. Настройка конфига

2.1 Получите curl-запрос к странице наблюдения за компаниями через отладчик браузера
2.2 Преобразуйте заголовки запроса в питон-словарь headers при помощи curlconverter.com
2.3. Создайте файл user_data.py и вставьте в него словарь headers, а также переменную odel_path, содержащую путь к модели ИИ (в формате gguf).

# Пример user_data.py:

```python
headers = {...} # В словаре несколько строк загловков запроса
model_path = r"C:\Users\alfab\AppData\Local\nomic.ai\GPT4All\saiga_yandexgpt_8b.Q4_0.gguf" #Путь к загруженной заранее модели
```
### 3. Запуск

```bash
python vkp_mon_arbitr.py
```

### 📁 Структура проекта

.
├── vkp_mon_arbitr.py     # Основной скрипт парсера
├── vkp_pdf.py            # Модуль для работы с PDF
├── vkp_db.py             # Модуль для работы с БД
└── requirements.txt      # Зависимости

### 🔍 Пример работы

Входные данные:
PDF-документ судебного решения из Kontur.Focus.

Выходные данные: CSV-файл "arbitr.csv"

Пример записи из CSV-файла:

**Истец:** Общество с ограниченной ответственностью ""Альянс Электро""  
**Ответчик:** Государственное унитарное предприятие ""Водоканал Санкт - Петербурга""  
**Суть дела:** Взыскание денежных средств по иску ООО «Альянс Электро» против ГУП «Водоканал Санкт-Петербурга». Третьи лица: временный управляющий ООО «Альянс Электро», общество с ограниченной ответственностью «СетеСервис».  
**Итог:** Апелляционная жалоба принята к производству Тринадцатого арбитражного апелляционного суда.</s>. 
