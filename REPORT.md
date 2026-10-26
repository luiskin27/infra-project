# Отчёт по практическому заданию (DevOps Midterm)
## Блок 1. Основы

### Задание 1.1. Настройка и первый коммит
**Выполненные команды:**
```bash
git config --global user.name "luiskin27"
git config --global user.email "arstanbekova_l@iuca.kg"
git config --global init.defaultBranch main
git add .gitignore
git commit -m "chore: add gitignore so extra files dont leak"
git push -u origin main

```

**Что произошло:** Настроил имя, почту и дефолтную ветку main. Создал пустой репозиторий на GitHub и первым коммитом закинул .gitignore, чтобы логи и секреты не слились в публичный доступ.

### Задание 1.2. Файлы проекта

**Выполненные команды:**

```bash
echo "DB_PASSWORD=secret123" > .env
echo "test log" > app.log
git status
git add README.md .env.example && git commit -m "docs: add readme and env example"
git add docker/ && git commit -m "feat: add docker files"
git add ansible/ && git commit -m "feat: add ansible playbooks"
git push

```

**Что произошло:** Распаковал файлы проекта и создал секреты .env и лог app.log. Через git status убедился, что .gitignore их скрывает. Разбил файлы проекта на три логических коммита и отправлю их на GitHub.

### Задание 1.3. Просмотр изменений

**Вывод `git diff` до `git add`:**
<img width="703" height="381" alt="Снимок экрана 2026-10-26 172127" src="https://github.com/user-attachments/assets/52d8e22a-2f5a-4b8e-9c95-d4cc71792e5c" />


**Вывод `git diff` после `git add`:** *(Пустой)*

**Вывод `git diff --staged`:**

<img width="558" height="117" alt="Снимок экрана 2026-10-26 175322" src="https://github.com/user-attachments/assets/ef31af10-e634-433b-bd29-7fd914ea51de" />



**Объяснение:** git diff без флагов сравнивает рабочий каталог со staging area (индексом). После git add изменения перешли в индекс, поэтому разница между диском и индексом стала нулевой. Чтобы увидеть изменения в индексе относительно последнего коммита, использовалась команда git diff --staged.

---

## Блок 2. История и ветки

### Задание 2.1. История коммитов

**Вывод `git log --oneline`:**
<img width="742" height="257" alt="Снимок экрана 2026-10-26 173501" src="https://github.com/user-attachments/assets/cd5ea9be-c95b-4747-a911-affdeb7ca033" />


**Вывод `git show HEAD~1`:**
<img width="575" height="398" alt="Снимок экрана 2026-10-26 173652" src="https://github.com/user-attachments/assets/f10472d2-7b9e-42f5-a6b8-38bd1d81ed07" />


**Коммит HEAD~1:** Это предпредыдущий коммит e5420cb docs: add project description.

### Задание 2.2. Ветка и слияние

**Вывод `git merge`:**
<img width="357" height="93" alt="Снимок экрана 2026-10-26 174017" src="https://github.com/user-attachments/assets/8891841b-c68a-4900-8a32-58ce35129df3" />


**Что произошло:** Создал ветку feature/healthcheck, добавил проверку в Dockerfile, замержил в main методом Fast-forward (так как в main новых коммитов не было) и удалил ветку.

### Задание 2.3. Конфликт слияния

**Маркеры конфликта в `ansible/group_vars/all.yml`:**
<img width="683" height="167" alt="Снимок экрана 2026-10-26 174208" src="https://github.com/user-attachments/assets/3fda951b-1f8f-4d56-9565-7266b3213413" />


**Что произошло:** Изменил порт приложения одновременно в main (8000) и в фиче-ветке (9090). При попытке мержа возник конфликт. Удалил маркеры, оставил порт 8000 и закоммитил слияние.

---

## Блок 3. Удалённый репозиторий и Merge Request

### Задание 3.1. Получение изменений с сервера

**Вывод `git pull`:**
<img width="357" height="93" alt="Снимок экрана 2026-10-26 174017" src="https://github.com/user-attachments/assets/aabf0815-6948-4ce8-b146-f1c7c2aa86be" />


**Что произошло:** Отредактировал README через веб-интерфейс GitHub и затянул коммит себе на ПК с помощью git pull.

### Задание 3.2. Merge Request

**Что произошло:** Создал ветку feature/ansible-curl, добавил таску установки curl в playbook.yml, сделал коммит по Conventional Commits (feat(ansible): install curl package), открыл Pull Request на GitHub с описанием изменений и слей его в main.

### Задание 3.3. Уборка веток

**Вывод `git branch -a` после `git fetch --prune`:**

**Что произошло:** Удалил локальную и удалённую ветки feature/ansible-curl и почистил указатели.

---

<img width="547" height="107" alt="Снимок экрана 2026-10-26 174706" src="https://github.com/user-attachments/assets/f9d880a5-31bd-48a2-93eb-f26a4379ebb1" />


## Блок 4. Docker

### Задание 4.1. Сборка и запуск контейнера

**Вывод команды сборки и запуска:**

```bash
docker build -t infra-web:1.0 docker/
docker run -d --name infra-web -p 8080:80 infra-web:1.0

```
<img width="570" height="323" alt="Снимок экрана 2026-10-26 181252" src="https://github.com/user-attachments/assets/7395772c-c644-49cf-bf8a-02948c0e64de" />


**Что произошло:** Обновлена стартовая страница HTML, добавлена директива EXPOSE 80 в Dockerfile. Образ успешно собран, протестирован локально в контейнере и изменения добавлены в ветку main через Pull Request.

---

## Блок 5. Исправление ошибок и вопросы

### Задание 5.1. Отмена незакоммиченных изменений и редактирование коммита

**Отмена нескоммиченных изменений:**

Сброс нежелательных правок в рабочем каталоге выполнен командой:

```bash
git restore docker/Dockerfile

```
<img width="570" height="323" alt="Снимок экрана 2026-10-26 181252" src="https://github.com/user-attachments/assets/39d73c01-32f1-46b7-a0d9-b57044d1e940" />
**Исправление коммита с опечаткой:**

Изменение наименования последнего коммита без создания нового выполнено через:

```bash
git commit --amend -m "docs: update readme"

```


### Задание 5.2. Отмена опубликованного коммита

**Выполненные команды:**

```bash
git revert HEAD --no-edit
git push

```
<img width="576" height="155" alt="Снимок экрана 2026-10-26 185737" src="https://github.com/user-attachments/assets/31c5d63a-65d5-4f69-9efb-000cdd369892" />


**Объяснение:** Для публичных коммитов, загруженных на сервер, применение команды git reset с принудительной отправкой (--force) недопустимо, так как это нарушает историю у остальных участников команды. Команда git revert создает новый коммит, полностью отменяющий действия ошибочного коммита, сохраняя целостность истории.

### Задание 5.3. Контрольные вопросы

1. **Что такое коммит и зачем нужна область индекса (staging area)?**
это получается такого рода снимок состояния файла на конкретный момент когда мы работаем а staring area нужна для подгтовки комита с помощью него можно отобрать нужные нам файлы перед их закреплением в истоии
2. **Что такое ветка в Git?**
ветка гит нужна для того чтобы не испортить код в main. к примеру у нас есть основной код проекта мы хотим добавить новыу функции к проекту так чтобы не испортить основной код сначала мы пишем код для новых функций на гит ветке если код удался то после этого мы можем его добавить в майн
3. **Что такое HEAD?**
указатель места нахождения разработчика на ветке
4. **Чем git fetch отличается от git pull?**
fetch просто скачивает новые данные с сервера, а pull скачивает и сразу сливает их в твою локльную ветку
5. **Почему файл .env нельзя добавлять в репозиторий?**
для приватности так как там могут хранится токены пароль и другая конфид инфа.

```

```
