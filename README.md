# Python_Selenium_Allure

## Описание проекта и задачи
Автоматизировать часть проверок на авторизацию на сайт https://pokemonbattle.ru/ и сформировать отчеты в Allure Report

## Подготовка
В проекте используется VS Code и классический вариант Selenium WebDriver - фреймворк для программного взаимодействия с браузером. Также понадобится учетка в https://pokemonbattle.ru/. Актуальная документация и лучшие практики в Selenium WebDriver - на [сайте разработчиков](https://www.selenium.dev/documentation/webdriver/)

## Локальный запуск тестов (из терминала)

### 1. Клонировать себе репозиторий в VS Code

### 2. Создание и активация виртуального окружения
Хорошей практикой при работе с проектами на Python является использование виртуального окружения. 
Выполнять в командной строке в корне проекта
1. Создаём виртуальное окружение
``` markdown
python -m venv env   # возможно не python, а python3
```
2. Активируем окружение
Для Windows есть два варианта:
* Первый. Выполнение powershell-скрипта
``` markdown
.\env\Scripts\Activate.ps1
```
> При активации виртуального окружения пользователи Windows могут столкнуться с невозможностью загрузить файл и ошибкой безопасности.  
> - **Решение 1**: Запустите PowerShell от администратора и выполните:
> ``` markdown
> - Set-ExecutionPolicy RemoteSigned
> ```
> На вопрос отвечаем: A (Да, для всех)  
> - **Решение 2**: Выполнить команду:
> ``` markdown
> Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
> ```
* Второй. Переключиться в терминал cmd и выполнить команду
``` markdown
.\env\Scripts\activate
```
Для MacOS и Linux
``` markdown
source env/bin/activate
```
3. Деактивация окружения
``` markdown
deactivate
```

### 3. Установка необходимых модулей
Для Windows
``` markdown
pip install -r .\requirements.txt   # установка необходимых библиотек из файла
```
Для macOS и Linux
``` markdown
pip install -r ./requirements.txt   # установка необходимых библиотек из файла
```
Тем самым мы установили требуемые модули, в том числе модуль allure-pytest. Allure-pytest – библиотека для формирования данных, которые Allure Report использует для построения отчетов.

### 4. Установка Allure
* Скачиваем [архив по ссылке](https://repo.maven.apache.org/maven2/io/qameta/allure/allure-commandline/2.19.0/allure-commandline-2.19.0.zip) и кладем **распакованный** каталог в одну папку со всеми твоими проектами.
* С этим архивом можно работать во всех операционных системах.

Проверим, что Allure работоспособен
* Для Windows
``` markdown
cd allure-2.19.0\bin    # первая команда — выполняем, находясь в каталоге, в котором есть распакованный архив с allure report

.\allure                # вторая команда — результатом выполнения будет вывод справочной информации об аргументах запуска allure report
```
* На Linux/Mac выполняем те же действия, только слеш / в другую сторону
``` markdown
cd allure-2.19.0/bin    # первая команда — выполняем, находясь в каталоге, в котором есть распакованный архив с allure report

./allure                # вторая команда — результатом выполнения будет вывод справочной информации об аргументах запуска allure report
```
### 5. Подготовить валидные логин и пароль в файле ​​​​common/conf.py​​​​
### 6. Далее нужно создать каталог ​​​​my_allure_results​​​​ в папке проекта — там в дальнейшем появятся результаты прогона в виде JSON-файлов

Ещё нужно создать в корне проекта папку .vscode, в ней создать файл settings.json, в него вставить следующий объект:
```
{
    "python.testing.pytestArgs": [
        "tests",
        "--alluredir=my_allure_results"
    ],
    "python.testing.unittestEnabled": false,
    "python.testing.pytestEnabled": true
}
```

### 7. Выполнение прогона автотестов с формированием отчета
Вот так мы запустим позитивный тест на авторизацию - test_positive_login
``` markdown
pytest tests/test_pokemon_web.py::test_positive_login --alluredir=my_allure_results 
```
а вот так - все тесты проекта
``` markdown
pytest tests/test_pokemon_web.py --alluredir=my_allure_results
```
Если при запуске Allure будет ошибка, связанная с отсутствием каких-то компонентов, то необходимо проверить, установлена ли виртуальная [Java](https://www.java.com/ru/download/manual.jsp) машина. Также стоит проверить, что в названии каталогов отсутствуют кириллические символы.

### 8. Запуск Allure для визуализации результатов прогона автотестов
Команды ниже написаны для Windows. Для macOS и Linux нужно заменить все "\" на "/"

cd <путь до каталога allure\bin>

В моем случае это получилось так:
``` markdown
cd С:\projects\allure-2.19.0\bin\ # первая команда — найти путь к файлу
```
.\allure serve <путь до каталога с результатами>

В моем случае это получилось так:
``` markdown
.\allure serve С:\projects\pokemonbatlle\my_allure_results # вторая команда
```
Итогом выполнения последней команды будет запуск и открытие в браузере страницы с отчетами ;)
![image](https://raw.githubusercontent.com/zaoivan/Python_Selenium_Allure/refs/heads/main/static/allure_report.png)
Какие-то тесты могут падать. Это не страшно, всегда есть что улучшать в коде :)

## Автор
Иван Заостровских ([telegram](https://t.me/franklstone))
