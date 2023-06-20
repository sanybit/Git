# Инструкция работы с Git

**Git** *— это система контроля версий, которая помогает отслеживать изменения в проекте. Этот инструмент можно использовать как для индивидуальной, так и для командной работы.*

*Git позволяет сохранять изменения локально и при необходимости возвращаться к предыдущим версиям проекта. Также можно создать удалённую копию на хостинг-платформе, которая работает с Git, и поделиться результатом с другими.*

### Сделать папку репозиторием

Чтобы Git начал отслеживать изменения в проекте, папку с файлами этого проекта нужно сделать **Git-репозиторием** (от англ. *repository* — «хранилище»). Для этого следует переместиться в неё и ввести команду `git init` (от англ. *initialize* — «инициализировать»).

`git init` выведет сообщение вида *Initialized empty Git repository in <*ваша папка с проектом*>/.git/* (англ. «инициализирован пустой Git-репозиторий в *<*ваша папка*>/.git/*»). В подпапке *.git* Git будет хранить всю служебную информацию.

Если вы случайно сделали Git-репозиторием не ту папку, её можно «разгитить». Для этого нужно удалить скрытую подпапку *.git*.

После инициализации репозитория запустите команду `git status` (от англ. *status* — «статус», «состояние») — она показывает текущее состояние репозитория.

Команда `git status` выведет:
- название текущей ветки: *On branch master* или *On branch main;*
- сообщение о том, что в репозитории ещё нет **коммитов**: *No commits yet;*
- сообщение, которое говорит: «чтобы что-нибудь закоммитить (то есть зафиксировать), нужно сначала это создать» — *nothing to commit (create/copy files and use "git add" to track).*

Состояние *untracked* значит, что Git ещё не хранит информацию о версиях файла и не может отследить, как он изменялся.

Мы хотим отслеживать состояние всех файлов, поэтому можем использовать команду `git add --all` (от англ. *add* — «добавить» + от англ. *all* — «всё»). Ключ, или флаг, `--all` позволяет подготовить к сохранению все файлы в репозитории.

Добавлять файлы можно и по одному, без ключа `--all`.

Также можно добавить текущую папку целиком — в этом случае все файлы в ней тоже будут добавлены. Обратиться к текущей папке в Bash позволяет точка (`.`).

Если сейчас отредактировать любой из «зелёных» файлов, он перейдёт в состояние *modified* (англ. «изменённый») и будет и в «зелёном», и в «красном» списках.

**Коммит** — это одна из основных сущностей в Git (и в других системах контроля версий). Коммит гарантирует, что изменения будут сохранены в истории и при необходимости к ним можно будет «откатиться». 

Сделать коммит можно командой `git commit` c ключом `-m` (от англ. *message* — «сообщение»), который присваивает коммиту сообщение.

Обычно в таком сообщении поясняется, в чём именно состояли изменения. Оно пишется после ключа `-m` в кавычках.

`git commit -m "Мой первый коммит!"`

Команда `git commit` выведет информацию о коммите.
- **[master (root-commit) baa3b6e]** значит:
  - коммит был в ветке *master*;
  - **root-commit** — это самый первый, или «корневой» (англ. *root*), коммит в ветке, у следующих коммитов такой надписи не будет;
  - **baa3b6e** — сокращённый идентификатор коммита.
- **2 files changed, 1 insertion(+)** значит:
  - изменились два файла;
  - одна строка была добавлена.
- Строки вида **create mode 100644 readme.txt** — это более подробная информация о новых (добавленных в Git) файлах.
  - **create** (англ. «создать») говорит, что файл был создан. Если бы файл был удалён, на этом месте было бы слово **delete** (англ. «удалить»).
  - **mode 100644** сообщает, что это обычный файл. Также возможны варианты **100755** для исполняемых файлов (например, **что-нибудь.exe**) и **120000** для файлов-ссылок в Linux. Файлы-ссылки не содержат данных сами по себе, а только ссылаются на другие файлы.
  
  *Обратите внимание: после того как вы сделали первый коммит, команда* `git status` *перестала выводить сообщение No commits yet (англ. «ещё нет коммитов»).*

Сначала команда `git add` сообщает Git, какие именно файлы нужно сохранить и какую их версию. Затем с помощью команды `git commit` происходит само сохранение. 

Чтобы увидеть коммиты нужно ввести команду `git log` (от англ. *log* — «журнал [записей]»).

По умолчанию `git log` выводит коммиты в обратном хронологическом порядке — последние коммиты оказываются первыми сверху.

#### **Чтобы поделиться репозиторием — например, с коллегами, — нужно завести его удалённую версию.**

**GitHub** — платформа для хранения IT-проектов и совместной работы над ними с использованием Git.

С английского языка слово **hub** переводится как «узловая станция».

Git и GitHub — это два разных проекта, которые развиваются независимо друг от друга. 

Git:
- консольный инструмент для работы с локальными и удалёнными репозиториями;
- проект с открытым исходным кодом.

GitHub:
- платформа для размещения удалённых репозиториев;
- принадлежит компании Microsoft.

Название удалённого репозитория необязательно должно совпадать с именем папки проекта у вас на компьютере.

## **Что такое SSH**
Когда компьютеры обмениваются данными в сети, они следуют **сетевым протоколам** (англ. *network protocols*) — правилам обмена данными между компьютерами.

Один из наиболее распространённых сетевых протоколов — **SSH** (от англ. *Secure Shell Protocol*). Он обеспечивает безопасный обмен данными в сети. С помощью этого протокола можно получать данные с удалённого компьютера или отправлять их на него. Трафик шифруется, поэтому протокол безопасен.

SSH использует пару ключей для обеспечения безопасности — публичный и приватный: 
- **Приватный ключ** (англ. *private key*) хранится только на вашем компьютере и не должен передаваться кому-либо ещё. Он используется для шифрования данных.
- **Публичный ключ** (англ. *public key*) доступен всем и используется для расшифровки данных, которые были зашифрованы приватным ключом.

Только вы можете зашифровать данные с помощью приватного ключа, но любой владелец публичного ключа может их расшифровать. Эти два ключа связаны и образуют **SSH-пару**.

По умолчанию директория с SSH-ключами находится в домашней директории пользователя.

Обычно SSH-ключи находятся в директории *.ssh/*. 

**Для генерации SSH-пары можно использовать программу ssh-keygen.**

`ssh-keygen -t ed25519 -C "электронная почта, к которой привязан ваш аккаунт на GitHub"`
или

`ssh-keygen -t rsa -b 4096 -C "электронная почта, к которой привязан ваш аккаунт на GitHub"`

После ввода отобразится такое сообщение.

> *Generating public/private rsa key pair. # сгенерированы публичный и приватный ключи*

Укажите место хранения ключей. Простой вариант — сделать домашний каталог пользователя путём по умолчанию.

### **macOS**

> *Enter a file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]*

### **Windows**

> *Enter a file in which to save the key (C:\Users\<имя_пользователя>\.ssh\):[Press enter]*

Теперь в указанной директории появится пара ключей.

Программа запросит **кодовую фразу** (англ. *passphrase*) для доступа к SSH-ключу. Вы можете оставить поле пустым. Для этого нажмите `Enter`, а затем ещё раз `Enter` для подтверждения.

> *Enter passphrase (empty for no passphrase): [Type a passphrase]*
>
> *Enter same passphrase again: [Type passphrase again]*

*Многие пользователи Git не используют кодовую фразу для защиты своего SSH-ключа. Если такой фразы нет, то её не нужно   вводить всякий раз при взаимодействии с удалённым репозиторием.*

Теперь осталось проверить, что ключи действительно сгенерировались. Для этого вызовите эту команду.

`ls -a ~/.ssh`

На экране должны появиться два файла — один с расширением **.pub**, другой — без. Файл в **.pub** — публичный, им можно делиться с веб-сайтами или коллегами. Файл без расширения **.pub** — приватный.

### **Инструкция по связыванию SSH-ключа и GitHub-аккаунта**

После выполнения команды `ssh-keygen` в директории *~/.ssh* будет создано два файла — **id_ed25519** и **id_ed25519.pub** (или **id_rsa** и **id_rsa.pub** — в зависимости от того, какой алгоритм вы использовали):

- **id_ed25519/id_rsa** — приватный ключ (файл без **.pub** в конце). 
- **id_ed25519.pub/id_rsa.pub** — публичный ключ (на это указывает расширение **.pub**).

1. Скопируйте содержимое файла с публичным ключом в буфер обмена.

2. Перейдите на GitHub и выберите пункт **Settings** (англ. «настройки») в меню аккаунта.

3. В меню слева нажмите на пункт **SSH and GPG keys**.

4. В открывшейся вкладке выберите **New SSH key** (англ. «новый SSH-ключ»).

5. В поле **Title** (англ. «заголовок») напишите название ключа. Например, **Personal key** (англ. «личный ключ»).

6. В поле **Key type** (англ. «тип ключа») должно быть **Authentication Key** (англ. «ключ аутентификации»).

7. В поле **Key** скопируйте ваш ключ из буфера обмена.

8. Нажмите на кнопку **Add SSH key** (англ. «добавить SSH-ключ»).

9. Проверьте правильность ключа с помощью следующей команды.

`ssh -T git@github.com.`

Если это первый раз, когда вы используете Git, чтобы поделиться проектом на GitHub, появится похожее предупреждение.

> *The authenticity of host 'github.com (140.82.121.4)' can't be established. ED25519 key fingerprint is 
> SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU. This key is not known by any other names.
> Are you sure you want to  continue connecting (yes/no/[fingerprint])?*

Это предупреждение сообщает, что вы никогда не соединялись с сервером GitHub. Поэтому Git не может гарантировать, что сервер является тем, за кого он себя выдаёт.

Для подтверждения подлинности сервер генерирует и публикует ключи SHA256. Вы можете проверить ключи GitHub [по этой ссылке](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints). Если ключ в предупреждении совпадает с тем, что вы видите на сайте, значит, сервер является действительным. Введите `yes`, чтобы продолжить. Вы увидите приветствие на экране.

> *i %ВАШ_АККАУНТ%! You've successfully authenticated, but GitHub does not provide shell access.*

### **Привязать удалённый репозиторий к локальному**

Перейдите на страницу удалённого репозитория, выберите тип `SSH` и скопируйте **URL**. Кнопка справа позволит сделать это мгновенно.

Откройте консоль, перейдите в каталог локального репозитория и введите команду `git remote add` (от англ. *remote* — «удалённый» и *add* — «добавить»).

Команде необходимо передать два параметра: имя удалённого репозитория и его URL. В качестве имени используйте слово `origin`. А `URL` вы скопировали со страницы удалённого репозитория.

`git remote add origin git@github.com:%ИМЯ_АККАУНТА%/first-project.git`

*В командную строку нельзя вставить текст из буфера обмена с помощью привычного сочетания Ctrl+V. На Windows (в Git Bash) и Linux для этого используется сочетание Ctrl+Shift+V, а на macOS — Cmd+V.*
*Также можно нажать правую кнопку мыши и выбрать пункт Paste (англ. «вставить») в выпадающем меню.*

*origin* (англ. «источник») — стандартный псевдоним, с помощью которого можно обращаться к главному удалённому репозиторию (обычно такой репозиторий один).

Убедиться, что репозитории связаны можно командой `git remote -v`

В выводе вы должны увидеть две строчки:

> origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (fetch)
>
> origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (push) 

Флаг `-v` — короткая форма флага `--verbose` (англ. «подробный»). Он позволяет показать больше информации в выводе.

Загрузить содержимое локального репозитория на GitHub можно командой `git push` (от англ. *push* — «толкать»).

В первый раз эту команду нужно вызвать с флагом `-u` и параметрами `origin` (имя удалённого репозитория) и `main` или `master` (название текущей ветки). Флаг `-u` свяжет локальную ветку с одноимённой удалённой. 

`git push -u origin main`

В дальнейшем при работе с удалённым репозиторием флаг `-u` можно опустить и писать просто `git push`.

Получить сокращённый лог можно с помощью команды `git log` с флагом `--oneline` (англ. «одной строкой»). В терминале появятся только первые несколько символов хеша каждого коммита и их комментарии.

`git log --oneline`

> **Обратите внимание:** если выход из просмотра логов не произошёл автоматически, нажмите клавишу `Q` (от англ. *Quit* — «выйти»)> в английской раскладке клавиатуры.

### Как исправить коммит

Иногда в только что выполненном коммите нужно что-то поменять: например, добавить ещё пару файлов или заменить сообщение на более информативное.
В таком случае можно внести правки в уже сделанный коммит с помощью опции `--amend` (от англ. *amend* — «исправить», «дополнить») у команды *commit*: `git commit --amend`.

> Важно: опция `--amend` работает только с последним коммитом (HEAD). Для исправления более ранних коммитов есть другие команды.

> `git add` Добавить файл как обычно
> `git commit --amend --no-edit` Изменить последний коммит

С опцией `--amend` команда `commit` не создаст новый коммит, а дополнит последний, просто добавив в него файл. 
При этом хеш последнего коммита изменится, потому что изменился список файлов в коммите.

Опция `--no-edit` сообщает команде `commit`, что сообщение коммита нужно оставить как было.

### Изменить сообщение коммита

`git commit --amend -m "Добавить новое сообщение коммита"`

Если забыть указать у команды `git commit --amend` один из флагов (`--no-edit` или `-m`), Git предложит отредактировать сообщение коммита вручную. Для этого он откроет текстовый редактор, который установлен в системе по умолчанию. Чаще всего это либо GNU nano, либо Vim.

Если вы не хотите менять сообщение через редактор, можно выйти из него с помощью `Ctrl+X`, а затем выбрать `N` (от англ. *no*). В таком случае редактор закроется, и Git оставит сообщение последнего коммита «как было».

Вот как выйти из Vim:

1. Нажмите клавишу `Esc`.

2. Наберите последовательность символов *:qa!*.

3. Нажмите `Enter`.

Допустим, вы создали или изменили какой-то файл и добавили его в список «на коммит» (staging area) с помощью `git add`, но потом передумали включать его туда. Убрать файл из staging поможет команда `git restore --staged <file>` (от англ. *restore* — «восстановить»).

Чтобы «сбросить» все файлы из **staged** обратно в **untracked/modified**, можно воспользоваться командой `git restore --staged .`: она сбросит всю текущую папку (`.`).

Иногда нужно «откатить» то, что уже было закоммичено, то есть вернуть состояние репозитория к более раннему. Для этого используют команду `git reset --hard <commit hash>` (от англ. *reset*  — «сброс», «обнуление» и *hard* — «суровый»).

#### «Откатить» изменения, которые не попали ни в staging, ни в коммит

Может быть так, что вы случайно изменили файл, который не планировали. Теперь он отображается в *Changes not staged for commit (modified)*. Чтобы вернуть всё «как было», можно выполнить команду `git restore <file>`.

Запустите `git diff`, чтобы выяснить детали. Эта команда сравнит последнюю закоммиченную версию файла file.txt с текущей (изменённой) версией.

Самое важное `git diff` выводит в конце:

- красный цвет строки никого нет значит, что эта строка была удалена;

- зелёный цвет строки Мышка-норушка значит, что она была добавлена.

Не все консоли умеют выводить цвета, поэтому строки помечаются не только цветом, но и знаком - или +. Минус — это удалённые строки, плюс — это добавленные.

Коротко разберём остальные строки вывода команды:

- Первые две строки (diff --git a/... b/... и index 901da07..ac459e1 100644) — это низкоуровневая техническая информация.

- Строки --- a/teremok.txt и +++ b/teremok.txt говорят, что дальше будет выведен результат сравнения файлов a/teremok.txt и b/teremok.txt — исходной и текущей версий.

- Строка @@ -1,2 +1,2 @@ сообщает, какие строки файла попали в сравнение. Выражение 1,2 (неважно, с плюсом или с минусом) говорит, что были использованы две строки, начиная с первой. Если бы было, например, написано +15,7, это значило бы, что в сравнении участвуют 7 строк, начиная с 15-й.

Выражение со знаком минус (-1,2) относится к «оригинальной» версии файла (a/teremok.txt), а со знаком плюс (+1,2) — к «изменённой» (b/teremok.txt).

По умолчанию команда `git diff` не показывает изменения в **staged**-файлах — только в **modified**.
Чтобы всё-таки просмотреть изменения в **staged**, нужно использовать флаг `--staged`: `git diff --staged`.

Передайте команде `git diff` хеши обоих коммитов. Состояние файлов на момент первого переданного коммита будет сравниваться с состоянием файлов на момент второго.

По сути команда `git diff A B` выводит список инструкций: как превратить состояние A в состояние B. Если поменять A и B местами (`git diff B A`), то и инструкции будут обратные: как превратить B в A. При этом все зелёные строки станут красными, и наоборот.

### Игнорирование файлов в Git

Часто бывает так, что в папке-репозитории есть файлы, для которых не нужно хранить историю изменений.

Чтобы Git игнорировал такие файлы и не пытался добавить их в репозиторий, нужно создать файл **.gitignore** (от англ. *ignore* — «игнорировать») и записать в него названия игнорируемых файлов. 

С точки зрения Git **.gitignore** — это обычный текстовый файл. Его добавляют в корень репозитория и тоже коммитят.
В простейшем случае в **.gitignore** указывают все файлы, которые нужно игнорировать (по одному имени на строку). Но часто удобнее использовать шаблоны. Шаблон, или правило, — это способ указать сразу на несколько файлов с однотипными названиями.

*Правила из .gitignore применяются только к новым (untracked) файлам. Если файл уже попал в staging area или в коммит, то правила на него не распространяются.*

Если строка начинается с #, то это комментарий, и **.gitignore** не будет его учитывать.

Допустим, нужно, чтобы Git игнорировал все файлы **.DS_Store**. Для этого достаточно добавить в **.gitignore** строку с названием файла.

В таком случае Git будет игнорировать файлы с именем **.DS_Store**, причём не только в корне репозитория, но и во всех вложенных папках.

Символ звёздочки (`*`) соответствует любой строке, включая пустую. Если такой символ используется в шаблоне в .gitignore, значит, файл будет проигнорирован вне зависимости от того, что будет на месте звёздочки.

`*.jpeg`

Вопросительный знак ? соответствует одному любому символу.

Квадратные скобки, как и вопросительный знак, соответствуют одному символу. При этом символ не любой, а только из списка, который указан в скобках.

Косая черта, или слеш (`/`), указывает на каталоги. Если шаблон в .gitignore начинается со слеша, то Git проигнорирует файлы или каталоги только в корневой директории.

Функция парных звёздочек (`**`) похожа на функцию одинарной (`*`). Отличие в том, как они работают с вложенными папками. Двойная звёздочка может соответствовать любому количеству таких папок (в том числе нулю). Одинарная может соответствовать только одной.

 *Для двойной звёздочки верно то же самое, что и для одной: если задать правило `**`, то будут проигнорированы все файлы.*
 
Любое правило в файле .gitignore можно инвертировать с помощью восклицательного знака (`!`).



```mermaid
graph LR;
  untracked -- "git add" --> staged;
  staged    -- "???"     --> tracked/comitted;

%% стрелка без текста для примера: 
  A --> B;
```