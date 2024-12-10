# Лабораторная работа 5

## Задание 1 - Автоматизация проверки формата файлов при коммите

1. Сначала мы создаем на рабочем столе папку ``projectgit``, переходим в нее и инициализируем работу git-репозитория с помощью команды ``git init``.
   Последняя команда создает скрытую папку ``.git``, и с помощью команды ``ls .git/hooks`` мы видим файлы с расширением ``.sample``:
<img width="574" alt="Снимок экрана 2024-12-10 в 20 19 01" src="https://github.com/user-attachments/assets/7e24d6a6-41b6-43d6-ae39-1dc3307bab61">

2. Переходим в папку ``.git/hooks``, создаем новый файл ``pre-commit``(делаем файл исполняемым с помощью команды ``chmod +x pre-commit``), открываем этот файл в текстовом редакторе и записываем определенный код:
<img width="546" alt="Снимок экрана 2024-12-10 в 20 39 08" src="https://github.com/user-attachments/assets/06ba5681-9ea7-4aa4-9d45-951cb40314eb">

<img width="653" alt="Снимок экрана 2024-12-10 в 20 38 07" src="https://github.com/user-attachments/assets/b0c73457-5731-4835-92b1-6aeca2c70f09">

3. С помощью ``cd ..`` выходим из hooks и переходим в папку ``projectgit``. Благодаря команде ``echo -e "Тестовый файл\nПользователь: Наида" > test.txt`` мы записываем определенный текст, который будет записан в файл test.txt. Благодаря команде ``cat test.txt``выводится содержимое файла ``test.txt``:
<img width="657" alt="Снимок экрана 2024-12-10 в 20 42 44" src="https://github.com/user-attachments/assets/569bc1f9-bc79-4ed6-a3cb-f79739ca0db6">

4. Добавляем файл ``test.txt`` в индекс Git, чтобы он был подготовлен для создания коммита. Создаем коммит, и система сообщает об ошибке, так как содержимое файла не прошло проверку -> коммит не записался:
<img width="537" alt="Снимок экрана 2024-12-10 в 20 45 09" src="https://github.com/user-attachments/assets/b6549775-7aad-4ac2-bf6b-cbf024298a11">

5. Сделаем те же действия, только поменяем слово "Пользователь" на "Автор" и система показывает, что проверка прошла и коммит записался:
<img width="613" alt="Снимок экрана 2024-12-10 в 20 51 06" src="https://github.com/user-attachments/assets/e76e57c7-15d5-42d6-a04d-ec7fa9be15c0">


## Задание 2 - Использование Git Flow в проекте
 1. Переходим на рабочий стол, создаем папку ``gitprojectinfo`` и инициализируем git-репозиторий:
<img width="420" alt="Снимок экрана 2024-12-10 в 22 55 51" src="https://github.com/user-attachments/assets/7d6bad4b-d0cc-4e96-a1d1-2e0d0cf97adb">

 2. С помощью команды ``git remote add origin`` связываем локальный репозиторий с удаленным, используя URL-key, проверяем подключился ли удаленный репозиторий командой ``git remote -v`` и устанавливаем Git Flow командой ``brew install`` (У меня уже был скачан менеджер пакетов Homebrew для MacOS):
<img width="800" alt="Снимок экрана 2024-12-10 в 22 56 56" src="https://github.com/user-attachments/assets/ca6508f1-223f-4f0b-93ed-67514c9e63a2">

3. Инициализируем git flow (задает вопросы о конфигурации веток, оставим настройки по умолчанию). Дальше создаем ветку для разработки функциональности с помощью команды ``git flow feature start task-management`` (git flow создает эту ветку и переключает на нее) и создаем файл, в котором записываем определенный текст:
```
def create_task(title, description):
    # Логика создания задачи
    print(f"Создана новая задача: {title}")
```
<img width="564" alt="Снимок экрана 2024-12-10 в 22 57 58" src="https://github.com/user-attachments/assets/52ec56c4-34e9-401d-8eda-9a1a204f97db">

4. Добавляем файл ``task_manager.py`` в индекс гит и делаем коммит. После завершения разработки функции завершаем фичу и объединяем ее с основной веткой. Git Flow автоматически переключается на ветку ``develop`` и выполняет слияние:
<img width="681" alt="Снимок экрана 2024-12-10 в 22 59 11" src="https://github.com/user-attachments/assets/abe1bd89-b2b9-4c82-8a87-8e79f9466396">

5. Переключаемся на ветку "develop" и начинаем создание релиза: Вносим изменения, связанные с релизом (обновим версию в файле version.txt). И фиксируем изменения с помощью команд ``git add`` и ``git commit -m``:
<img width="642" alt="Снимок экрана 2024-12-10 в 23 00 05" src="https://github.com/user-attachments/assets/3243558e-5220-4148-ad6e-9b9abb072eed">

6. Завершаем релиз и объединяем его с ветками "develop" и "main" с помощью команды ``git flow release finish v1.0.0``:
<img width="521" alt="Снимок экрана 2024-12-10 в 23 01 50" src="https://github.com/user-attachments/assets/0d5dd325-06eb-4dad-8b3f-9c2954267f88">

7. У нас никакой ошибки не возникает, но ветку ``hotfix`` все равно создадим ``git flow hotfix start hotfix-1.0.1``. Вносим изменения для исправления ошибки в файл и делаем коммит:
<img width="655" alt="Снимок экрана 2024-12-10 в 23 02 42" src="https://github.com/user-attachments/assets/bd3fb177-cfa1-4fb5-8992-27eab57f9765">

8. Завершаем ``hotfix`` и объединияем его с ветками "develop" и "main":
<img width="556" alt="Снимок экрана 2024-12-10 в 23 03 22" src="https://github.com/user-attachments/assets/4da9928c-538d-4b88-aa26-fead6055fb74">

9. Завершаем работы и отправляем изменения на удаленный репозиторий:
<img width="532" alt="Снимок экрана 2024-12-10 в 23 06 41" src="https://github.com/user-attachments/assets/67ea4c65-f0c9-4455-8160-fba266f594bc">
<img width="963" alt="Снимок экрана 2024-12-10 в 22 53 34" src="https://github.com/user-attachments/assets/159cf9ae-d65c-45c4-96d5-a74059bc6317">

