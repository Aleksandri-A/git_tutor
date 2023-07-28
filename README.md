# Шпаргалка по работе с Git
## Инициализируем репозиторий

Например, создайте папку first-project и сделайте её Git-репозиторием: перейдите в неё с помощью команды cd и выполните git init.
```bash
$ mkdir first-project
$ cd ~/dev/first-project # перешли в нужную папку
$ git init # создали репозиторий 
```
После инициализации репозитория first-project запустите команду git status (от англ. status — «статус», «состояние») — она показывает текущее состояние репозитория.
```bash
$ git status
```
Добавляем необходимые файлы в репозиторий.
```bash
$ touch README.md
$ touch todo.txt
```
Сейчас в first-project два файла. Мы хотим отслеживать состояние обоих, поэтому можем использовать команду git add --all (от англ. add — «добавить» + от англ. all — «всё»). Ключ, или флаг, --all позволяет подготовить к сохранению все файлы в репозитории.
```bash
$ git add --all # подготовили к сохранению все файлы в репозитории
$ git status # проверили статус 
```
Добавлять файлы можно и по одному, без ключа --all.
```bash
$ git add todo.txt
$ git add README.md
```
Также можно добавить текущую папку целиком — в этом случае все файлы в ней тоже будут добавлены. Обратиться к текущей папке в Bash позволяет точка (.).
```bash
$ git add . # добавить всю текущую папку
```

## Делаем первый коммит

Сделать коммит можно командой git commit c ключом -m (от англ. message — «сообщение»), который присваивает коммиту сообщение.
Например, перейдите в папку first-project и выполните коммит со следующим комментарием.
Например, перейдите в папку first-project и выполните коммит со следующим комментарием.
```bash
$ git commit -m ‘Мой первый коммит!’ 
```

## Просматриваем историю коммитов

Просмотреть историю коммитов — git log
```bash
$ git log
```
> Обратите внимание, что по умолчанию git log выводит коммиты в обратном хронологическом порядке — последние коммиты оказываются первыми сверху. В этом можно убедиться, если посмотреть на дату и время их создания.

## Регистрация на GitHub

### Инструкция по регистрации
1. В правом верхнем углу главной страницы GitHub нажмите на Sign up (англ. «зарегистрироваться»).
2. На экране будут последовательно появляться поля для ввода.  
2.1. Введите адрес электронной почты (англ. Enter your email).  
2.2. Придумайте пароль (англ. Create a password).  
2.3. Введите имя пользователя (англ. Enter a username).  
3. Платформа спросит, хотите ли вы получать на почту рассылку с обновлениями и новостями (англ. Would you like to receive product updates and announcements via email?). Введите y, если хотите получать рассылку, или n, если не хотите.
4. Нажмите кнопку Continue (англ. «продолжить»).
5. GitHub предложит вам пройти капчу. Сделайте это.
6. После прохождения капчи нажмите Create account (англ. «создать аккаунт»).
7. Введите короткий код, который будет отправлен на указанный вами почтовый адрес.

## Создаём удалённый репозиторий

### Инструкция по созданию репозитория на GitHub

1. Зайдите в свой профиль по ссылке https://github.com/username, где username — имя, которое вы указали при регистрации.
2. Создайте репозиторий. Для этого перейдите на вкладку Repositories (англ. «репозитории»), а затем нажмите на зелёную кнопку New (англ. «новый») справа.
3. Открылось окно создания нового репозитория. Назовите его first-project. Название удалённого репозитория необязательно должно совпадать с именем папки проекта у вас на компьютере. Но чтобы не путаться, будем называть их одинаково.
4. При необходимости заполните остальные поля и нажимайте на зелёную кнопку Create repository (англ. «создать репозиторий») внизу.

## Генерируем SSH-ключ

>Когда компьютеры обмениваются данными в сети, они следуют сетевым протоколам (англ. network protocols) — правилам обмена данными между компьютерами.
Один из наиболее распространённых сетевых протоколов — SSH (от англ. Secure Shell Protocol). Он обеспечивает безопасный обмен данными в сети. С помощью этого протокола можно получать данные с удалённого компьютера или отправлять их на него. Трафик шифруется, поэтому протокол безопасен.
SSH использует пару ключей для обеспечения безопасности — публичный и приватный: 
Приватный ключ (англ. private key) хранится только на вашем компьютере и не должен передаваться кому-либо ещё. Он используется для расшифровки данных.
Публичный ключ (англ. public key) доступен всем и используется для шифрования данных. Они могут быть расшифрованы парным приватным ключом.

### Проверка наличия SSH-ключа
Прежде чем генерировать SSH-ключи, убедитесь, что у вас их ещё нет. По умолчанию директория с SSH-ключами находится в домашней директории пользователя. Перейдите в неё.
```bash
$ cd ~ # перешли в домашнюю директорию 
```
Обычно SSH-ключи находятся в директории .ssh/. Проверить наличие этой директории и файлов в ней можно с помощью следующей команды.
```bash
$ ls -la .ssh/ # вывели список созданных ключей 
```

### Инструкция по генерации SSH-ключа
Для генерации SSH-пары можно использовать программу ssh-keygen. Откройте терминал и введите следующую команду.
```bash
$ ssh-keygen -t ed25519 -C "электронная почта, к которой привязан ваш аккаунт на GitHub" 
```
Используйте электронную почту, к которой привязан ваш GitHub-аккаунт.
>Если вы видите сообщение об ошибке, то, скорее всего, ваша система не поддерживает алгоритм шифрования ed25519. Ничего страшного: используйте другой алгоритм.
```bash
$ ssh-keygen -t rsa -b 4096 -C "электронная почта, к которой привязан ваш аккаунт на GitHub" 
```
После ввода отобразится такое сообщение.
```bash
> Generating public/private rsa key pair. # сгенерированы публичный и приватный ключи 
```
Укажите место хранения ключей. Простой вариант — сделать домашний каталог пользователя путём по умолчанию. Для этого нажмите Enter.
macOS
```bash
> Enter a file in which to save the key (C:\Users\<имя_пользователя>\.ssh\):[Press enter] 
```
Теперь в указанной директории появится пара ключей.
Программа запросит кодовую фразу (англ. passphrase) для доступа к SSH-ключу. Вы можете оставить поле пустым. Для этого нажмите Enter, а затем ещё раз Enter для подтверждения.
```bash
> Enter passphrase (empty for no passphrase): [Type a passphrase]
> Enter same passphrase again: [Type passphrase again] 
```
Теперь осталось проверить, что ключи действительно сгенерировались. Для этого вызовите эту команду.
```bash
ls -a ~/.ssh 
```
На экране должны появиться два файла — один с расширением .pub, другой — без. Файл в .pub — публичный, им можно делиться с веб-сайтами или коллегами. Файл без расширения .pub — приватный. Ни в коем случае не передавайте его никому! 

### Инструкция по связыванию SSH-ключа и GitHub-аккаунта
>После выполнения команды ssh-keygen из предыдущего урока в директории ~/.ssh будет создано два файла — id_ed25519 и id_ed25519.pub (или id_rsa и id_rsa.pub — в зависимости от того, какой алгоритм вы использовали):
id_ed25519/id_rsa — приватный ключ (файл без .pub в конце). Ни в коем случае не копируйте его и не делитесь им.
id_ed25519.pub/id_rsa.pub — публичный ключ (на это указывает расширение .pub).
1. Скопируйте содержимое файла с публичным ключом в буфер обмена.
```bash
# скопировать содержимое ключа в буфер обмена:
$ clip < ~/.ssh/id_rsa.pub
# для ed25519:
$ clip < ~/.ssh/id_ed25519.pub 
```
Если clip не сработает, выведите содержимое файла с помощью cat ~/.ssh/id_rsa.pub или cat ~/.ssh/id_ed25519.pub и скопируйте вывод в буфер обмена из консоли.
2. Перейдите на GitHub и выберите пункт Settings (англ. «настройки») в меню аккаунта.
3. В меню слева нажмите на пункт SSH and GPG keys.
4. В открывшейся вкладке выберите New SSH key (англ. «новый SSH-ключ»).
5. В поле Title (англ. «заголовок») напишите название ключа. Например, Personal key (англ. «личный ключ»).
6. В поле Key type (англ. «тип ключа») должно быть Authentication Key (англ. «ключ аутентификации»).
7. В поле Key скопируйте ваш ключ из буфера обмена.
8. Нажмите на кнопку Add SSH key (англ. «добавить SSH-ключ»).
9. Проверьте правильность ключа с помощью следующей команды.
```bash
$ ssh -T git@github.com 
```

## Связываем локальный и удалённый репозитории

Привязать удалённый репозиторий к локальному — git remote add
```bash
$ cd ~/dev/first-project
$ git remote add origin git@github.com:%ИМЯ_АККАУНТА%/first-project.git 
```
>Команде необходимо передать два параметра: имя удалённого репозитория и его URL. В качестве имени используйте слово origin. А URL вы скопировали со страницы удалённого репозитория.

Убедиться, что репозитории связаны, — git remote -v
```bash
$ git remote -v
origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (fetch)
origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (push) 
```
>В выводе вы должны увидеть две строчки, аналогичные тем, что показаны выше.
Флаг -v — короткая форма флага --verbose (англ. «подробный»). Он позволяет показать больше информации в выводе.

## Синхронизируем локальный и удалённый репозитории

Отправить изменения на удалённый репозиторий — git push
Вы уже прошли весь «цикл коммита»: подготовили файлы с помощью git add, закоммитили их с комментарием командой git commit -m. Осталось загрузить содержимое локального репозитория на GitHub. За это отвечает команда git push (от англ. push — «толкать»).
В первый раз эту команду нужно вызвать с флагом -u и параметрами origin (имя удалённого репозитория) и main или master (название текущей ветки). Флаг -u свяжет локальную ветку с одноимённой удалённой. Как вы связывали локальный и удалённый репозитории в предыдущем уроке, так же и здесь нужно дополнительно связать ветки.
```bash
$ git push -u origin main # Если команда приведёт к ошибке, попробуйте 
                          # заменить main на master. 
```
