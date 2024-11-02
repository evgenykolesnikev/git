## Вивчення Git. Колєснік Євгеній ІПЗ-4.01

## Налаштування середи

Встановимо пошту та ім'я користувача у git:

> git config --global user.name "evgenykolesnik"

> git config --global user.email "evgenykolesnikev@gmail.com"

Вставновимо правила обробки закінчень файлів:

> git config --global core.autocrlf true

> git config --global core.safecrlf warn

## Новий проєкт

Створимо папку `git` для нового проєкту та розмістимо в середині файл `hello.html`. Ініціалізуємо git:

> git init

Додамо файл `hello.html`:

> git add hello.html

Створимо коміт з повідомленням `init`:

> git commit -m "init"

Перевіримо статус:

> git status

Результат:

![git статус](screenshots/git_status.png)

Ми знаходимось на головній гілці, нічого додавати до коміту.

## Редагування файлу

Змінимо файл `hello.html`, новий вміст:

```html
<h1>Hello!</h1>
```

Перевіримо статус:

> git status

Результат:

![git статус 2](screenshots/git_status2.png)

Git побачив зміни файлу `hello.html`.

Додамо файл до наступного коміту та перевіримо статус:

> git add hello.html

> git status

Результат:

![git статус 3](screenshots/git_status3.png)

Git показав, що були додані до коміту зміни `hello.html`.

Створимо коміт та переглянемо логи репозиторію:

> git commit -m "add tag"

> git log --oneline

Результат:

![Логи репозиторію](screenshots/logs.png)

Git показав наявність двох комітів.

## Отримання попередніх версій

Перевіримо файл `hello.html`. Результат:

![Файл hello.html](screenshots/hello.html.png)

Переключимось на попередню версію репозиторію:

> git checkout 10eb4d0

Знову перевіримо файл `hello.html`. Результат:

![Файл hello.html після повернення на попередню версію](screenshots/hello.html2.png)

Файл знову став пустим.

Повернемося на останній коміт:

> git switch main

Знову перевіримо файл `hello.html`. Результат:

![Файл hello.html перевірка №3](screenshots/hello.html3.png)

У файлі вернувся тег h1.

## Додання тегів

Додамо теги до комітів:

```bash
git tag v1 10eb4d0
git tag v2 5f472f0
```

Перевіримо теги:

> git tag

Результат:

![Теги комітів](screenshots/tags.png)

Git знайшов два тега `v1` та `v2`.

## Скасування запланованих дій

Змінимо файл `hello.html`. Результат:

![Файл hello.html перевірка №4](screenshots/hello.html4.png)

Додамо зміну файлу `hello.html`:

> git add hello.html

Перевіримо статус:

> git status

Результат:

![git статус 4](screenshots/git_status4.png)

Відмінемо додання файлу `hello.html`:

> git reset HEAD hello.html

Переведемо файл `hello.html` до версії останнього коміту:

> git checkout hello.html

Перевіримо файл `hello.html`. Результат:

![Файл hello.html перевірка №5](screenshots/hello.html5.png)

Файл повернувся до версії з одним заголовком.

## Відкат коміту

Змінимо файл `hello.html` та створимо новий коміт:

```bash
git add hello.html
git commit -m "bad commit"
```

Перевіримо результат:

> git log --oneline

**Результат:**

![Список комітів](screenshots/12_git_log.png)

Створимо коміт, який відкатить зміни поточного:

> git revert HEAD

Перевіримо результат:

> git log --oneline

Результат:

![Логи репозиторію 2](screenshots/logs2.png)

Промаркуємо поточний коміт як `currpoint`:

> git tag currpoint

Перевіримо результат:

> git log --oneline

Результат:

![Логи репозиторію 3](screenshots/logs3.png)

Повернемося до версії `v1`:

> git reset --hard v1

Перевіримо результат:

> git log --all --oneline

Результат:

![Логи репозиторію 4](screenshots/logs4.png)

Новий поточний коміт — коміт з тегом `v1`.

Видалимо тег `currpoint`:

> git tag -d currpoint

Перевіримо результат:

> git log --all --oneline

Результат:

![Логи репозиторію 5](screenshots/logs5.png)

Зайві коміти зникли з історії комітів після видалення тегу.

## Зміна останнього коміту

У файл `hello.html` було додано новий рядок:

![Файл hello.html перевірка №6](screenshots/hello.html6.png)

Створимо коміт:

> git add hello.html

> git commit -m "add new row"

Перевіримо результат:

> git log --oneline

Результат:

![Логи репозиторію 6](screenshots/logs6.png)

Додамо точку у кінець рядка файлу `hello.html`:

![Файл hello.html перевірка №7](screenshots/hello.html7.png)

Виконаємо злиття:

> git add hello.html

> git commit --amend -m "add point"

Перевіримо результат:

> git log --oneline

Результат:

![Логи репозиторію 7](screenshots/logs7.png)

## Створення гілки

Створімо нову гілку для скриптів:

> git switch -c scripts

Перевіримо статус репозиторія:

> git status

Результат:

![git статус 5](screenshots/git_status5.png)

Створилася гілка `scripts`, яка стала поточною.

Створімо файл `script.js` для скрипту.

З вмістом:

```javascript
let a = 10;
```

Додамо зміни:

> git add script.js

> git commit -m "add js file"

Змінимо файл `hello.html`:

![Файл hello.html перевірка №8](screenshots/hello.html8.png)

Додамо зміни:

> git add hello.html

> git commit -m "changed html file"

## Безпечне перейменування файлів

Змінимо назву файлу `hello.html` на `trash.html`: 

> git mv hello.html trash.html

Додамо зміни:

> git add .

> git commit -m "change name of hello.html file"

## Завантаження репозиторія на github

Додамо віддалений репозиторій:

> git remote add origin https://github.com/evgenykolesnikev/git.git

Завантажимо обидві гілки:

> git push -u origin main

> git push -u origin scripts

Результат:

Перевіримо репозиторій на сайті `https://github.com`:

![Репозиторій на сайті](screenshots/github.png)

## Висновок

Виконуючи цю роботу я підтвердив теоретичний матеріал по роботі з системою git. Під час виконання роботи я ознайомився з роботою у системі git створивши тестовий репозиторій. Система Git дозволяє гнучко управляти версіями файлів розроблювальних програмних систем. Отриманні знання є основою при розробці систем пов'язаних з роботою з координатами.