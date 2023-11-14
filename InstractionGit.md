# Глава 1. Настройка Git после установки

После установили git, нужно добавить немного настроек. 
Есть довольно много опций, с которыми можно играть, но мы настроим самые важные: наше имя пользователя и адрес электронной почты. 
Откройте терминал и запустите команды:

```sh
git config --global user.name "My Name"
```
```sh
git config --global user.email myEmail@example.com
```
Теперь каждое наше действие будет отмечено именем и почтой. Таким образом, пользователи всегда будут в курсе, кто отвечает за какие изменения — это вносит порядок.
Git хранит весь пакет конфигураций в файле .gitconfig, находящемся в вашем локальном каталоге. Чтобы сделать эти настройки глобальными, то есть применимыми ко всем проектам, необходимо добавить флаг –global. Если вы этого не сделаете, они будут распространяться только на текущий репозиторий.

Для того, чтобы посмотреть все настройки системы, используйте команду:
```sh
git config --list
```
Для удобства и легкости зрительного восприятия, некоторые группы команд в Гит можно выделить цветом, для этого нужно прописать в консоли:
```sh
git config --global color.ui true
git config --global color.status auto
git config --global color.branch auto
```
Если вы не до конца настроили систему для работы, в начале своего пути - не беда. Git всегда подскажет разработчику, если тот запутался, например:

1. Команда ```git --help``` - выводит общую документацию по git
2. Если введем ```git log --help``` - он предоставит нам документацию по какой-то определенной команде (в данном случае это - log)
3. Если вы вдруг сделали опечатку - система подскажет вам нужную команду
4. После выполнения любой команды - отчитается о том, что вы натворили
5. Также Гит прогнозирует дальнейшие варианты развития событий и всегда направит разработчика, не знающего, куда двигаться дальше

Тут стоит отметить, что подсказывать система будет на английском, но не волнуйтесь, со временем вы изучите несложный алгоритм ее работы и будете разговаривать с ней на одном языке.

# Глава 2. Создание нового репозитория
Git хранит свои файлы и историю прямо в папке проекта. Чтобы создать новый репозиторий, нам нужно открыть терминал, зайти в папку нашего проекта и выполнить команду ```git init```. Это включит приложение в этой конкретной папке и создаст скрытую директорию .git, где будет храниться история репозитория и настройки.
Как пример, создадим на рабочем столе папку под названием git_exercise. Для этого в окне терминала введите:

```sh
mkdir Desktop/git_exercise/
cd Desktop/git_exercise/
git init
```
Командная строка должна вернуть что-то вроде:
```sh
Initialized empty Git repository in /home/user/Desktop/git_exercise/.git/
```
Это значит, что наш репозиторий был успешно создан, но пока что пуст. Теперь создайте текстовый файл под названием hello.txt и сохраните его в директории git_exercise.

# Глава 3. Определение состояния
``` git status``` — это еще одна важнейшая команда, которая показывает информацию о текущем состоянии репозитория: актуальна ли информация на нём, нет ли чего-то нового, что поменялось, и так далее. Запуск ```git status``` на нашем свежесозданном репозитории должен выдать:

```sh
git status
On branch master
Initial commit
Untracked files:
(use "git add ..." to include in what will be committed)
hello.txt
```
Сообщение говорит о том, что файл hello.txt неотслеживаемый. Это значит, что файл новый и система еще не знает, нужно ли следить за изменениями в файле или его можно просто игнорировать. Для того, чтобы начать отслеживать новый файл, нужно его специальным образом объявить.

# Глава 4. Подготовка файлов
В git есть концепция области подготовленных файлов. Можно представить ее как холст, на который наносят изменения, которые нужны в коммите. Сперва он пустой, но затем мы добавляем на него файлы (или части файлов, или даже одиночные строчки) командой ```git add``` и, наконец, коммитим все нужное в репозиторий (создаем слепок нужного нам состояния) командой ```git commit -m "текст"```.
В нашем случае у нас только один файл, так что добавим его:

```sh
git add hello.txt
```
Если нам нужно добавить все, что находится в директории, мы можем использовать
```sh
git add -A
```
Проверим статус снова, на этот раз мы должны получить другой ответ:

```sh
git status
On branch master
Initial commit
Changes to be committed:
(use "git rm --cached ..." to unstage)
new file: hello.txt
```
Файл готов к коммиту. Сообщение о состоянии также говорит нам о том, какие изменения относительно файла были проведены в области подготовки — в данном случае это новый файл, но файлы могут быть модифицированы или удалены.

# Глава 5. Фиксация изменений
## Часть 1. Как сделать коммит
Представим, что нам нужно добавить пару новых блоков в html-разметку (index.html) и стилизовать их в файле style.css. Для сохранения изменений, их необходимо закоммитить. Но сначала, мы должны обозначить эти файлы для Гита, при помощи команды ```git add```, добавляющей (или подготавливающей) их к коммиту. Добавлять их можно по отдельности:

```sh
git add index.html
git add css/style.css
```
или вместе - всё сразу:
```sh
git add .
```
Конечно добавлять всё сразу удобнее, чем прописывать каждую позицию отдельно. Однако, тут надо быть внимательным, чтобы не добавить по ошибке ненужные элементы. Если же такое произошло изъять оттуда ошибочный файл можно при помощи команды

```sh
git reset:
git reset css/style.css
```
Теперь создадим непосредственно сам коммит
```sh
git commit -m "текст"
```
Флажок -m задаст commit message - комментарий разработчика. Он необходим для описания закоммиченных изменений. И здесь работает золотое правило всех комментариев в коде: **«Максимально ясно, просто и содержательно обозначь написанное!»**

## Часть 2. Как посмотреть коммиты
Для просмотра всех выполненных фиксаций можно воспользоваться историей коммитов. Она содержит сведения о каждом проведенном коммите проекта. Запросить ее можно при помощи команды:
```sh
git log
```
В ней содержится вся информация о каждом отдельном коммите, с указанием его хэша, автора, списка изменений и даты, когда они были сделаны. 
Bстория изменений, по одной строке на каждый коммит - ```git log --oneline```
Отследить интересующие вас операции в списке изменений, можно по хэшу коммита, при помощи команды ```git show```:

```sh
git show hash_commit
```
Ну а если вдруг нам нужно переделать commit message и внести туда новый комментарий, можно написать следующую конструкцию:

```sh
git commit --amend -m "Новый комментарий"
```
В данном случае сообщение последнего коммита перезапишется. Но злоупотреблять этим не стоит, поскольку эта операция опасная и лучше ее делать до отправки коммита на сервер.

## Часть 3. Отслеживание изменений, сделанных в коммитах
У каждого коммита есть свой уникальный идентификатор в виде строки цифр и букв. Чтобы просмотреть список всех коммитов и их идентификаторов, можно использовать команду ```git log```:

```sh
git log
commit ba25c0ff30e1b2f0259157b42b9f8f5d174d80d7
Author: Tutorialzine
Date: Mon May 30 17:15:28 2016 +0300
New feature complete
commit b10cc1238e355c02a044ef9f9860811ff605c9b4
Author: Tutorialzine
Date: Mon May 30 16:30:04 2016 +0300
Added content to hello.txt
commit 09bd8cc171d7084e78e4d118a2346b7487dca059
Author: Tutorialzine
Date: Sat May 28 17:52:14 2016 +0300
Initial commit
```
Как вы можете заметить, идентификаторы довольно длинные, но для работы с ними не обязательно копировать их целиком — первых нескольких символов будет вполне достаточно. Чтобы посмотреть, что нового появилось в коммите, мы можем воспользоваться командой ```git show [commit]```

```sh
git show b10cc123
commit b10cc1238e355c02a044ef9f9860811ff605c9b4
Author: Tutorialzine
Date: Mon May 30 16:30:04 2016 +0300
Added content to hello.txt
diff --git a/hello.txt b/hello.txt
index e69de29..b546a21 100644
--- a/hello.txt
+++ b/hello.txt
@@ -0,0 +1 @@
+Nice weather today, isn't it?
```
Чтобы увидеть разницу между двумя коммитами, используется команда ```git diff``` (с указанием промежутка между коммитами):

```sh
git diff 09bd8cc..ba25c0ff
diff --git a/feature.txt b/feature.txt
new file mode 100644
index 0000000..e69de29
diff --git a/hello.txt b/hello.txt
index e69de29..b546a21 100644
--- a/hello.txt
+++ b/hello.txt
@@ -0,0 +1 @@
+Nice weather today, isn't it?
```
Мы сравнили первый коммит с последним, чтобы увидеть все изменения, которые были когда-либо сделаны. Обычно проще использовать ```git difftool```, так как эта команда запускает графический клиент, в котором наглядно сопоставляет все изменения.

## Часть 4. Возвращение файла к предыдущему состоянию
Гит позволяет вернуть выбранный файл к состоянию на момент определенного коммита. Это делается уже знакомой нам командой ```git checkout```, которую мы ранее использовали для переключения между ветками. Но она также может быть использована для переключения между коммитами (это довольно распространенная ситуация для Гита - использование одной команды для различных, на первый взгляд, слабо связанных задач).
В следующем примере мы возьмем файл hello.txt и откатим все изменения, совершенные над ним к первому коммиту. Чтобы сделать это, мы подставим в команду идентификатор нужного коммита, а также путь до файла:
```sh
git checkout 09bd8cc1 hello.txt
```

## Часть 5. Исправление коммита
Если вы опечатались в комментарии или забыли добавить файл и заметили это сразу после того, как закоммитили изменения, вы легко можете это поправить при помощи ```git commit —amend```. Эта команда добавит все из последнего коммита в область подготовленных файлов и попытается сделать новый коммит. Это дает вам возможность поправить комментарий или добавить недостающие файлы в область подготовленных файлов.
Для более сложных исправлений, например, не в последнем коммите или если вы успели отправить изменения на сервер, нужно использовать revert. Эта команда создаст коммит, отменяющий изменения, совершенные в коммите с заданным идентификатором.
Самый последний коммит может быть доступен по алиасу HEAD:

```sh
git revert HEAD
```
Для остальных будем использовать идентификаторы:
```sh
git revert b10cc123
```
При отмене старых коммитов нужно быть готовым к тому, что возникнут конфликты. Такое случается, если файл был изменен еще одним, более новым коммитом. И теперь git не может найти строчки, состояние которых нужно откатить, так как они больше не существуют.

# Глава 6. Ветвление
Во время разработки новой функциональности считается хорошей практикой работать с копией оригинального проекта, которую называют веткой. Ветви имеют свою собственную историю и изолированные друг от друга изменения до тех пор, пока вы не решаете слить изменения вместе. Это происходит по набору причин:

- Уже рабочая, стабильная версия кода сохраняется.
- Различные новые функции могут разрабатываться параллельно разными программистами.
- Разработчики могут работать с собственными ветками без риска, что кодовая база поменяется из-за чужих изменений.
- В случае сомнений, различные реализации одной и той же идеи могут быть разработаны в разных ветках и затем сравниваться.

## Часть 1. Создание новой ветки
Основная ветка в каждом репозитории называется master. Чтобы создать еще одну ветку, используем команду ```git branch <имя ветки>```

```sh
git branch amazing_new_feature
```
Это создаст новую ветку, пока что точную копию ветки master.

## Часть 2. Переключение между ветками
Сейчас, если мы запустим команду ```git branch```, мы увидим две доступные опции:

```sh
git branch
amazing_new_feature
* master
```
master — это активная ветка, она помечена звездочкой. Но мы хотим работать с нашей “новой потрясающей фичей”, так что нам понадобится переключиться на другую ветку. Для этого воспользуемся командой ``` git checkout <имя ветки>```, она принимает один параметр — имя ветки, на которую необходимо переключиться.

```sh
git checkout amazing_new_feature
```
В Git ветка — это отдельная линия разработки. Git checkout позволяет нам переключаться как между удаленными, так и меду локальными ветками. Это один из способов получить доступ к работе коллеги или соавтора, обеспечивающий более высокую продуктивность совместной работы. Однако тут надо помнить, что пока вы не закомитили изменения, вы не сможете переключиться на другую ветку. В такой ситуации нужно либо сделать коммит, либо отложить его, при помощи команды ```git stash```, добавляющей текущие незакоммиченные изменения в стек изменений и сбрасывающей рабочую копию до HEAD'а репозитория.

## Часть 3. Слияние веток
Наша “потрясающая новая фича” будет еще одним текстовым файлом под названием feature.txt. Мы создадим его, добавим и закоммитим:

```sh
git add feature.txt
git commit -m "New feature complete.”
```
Изменения завершены, теперь мы можем переключиться обратно на ветку master.
```sh
git checkout master
```
Теперь, если мы откроем наш проект в файловом менеджере, мы не увидим файла feature.txt, потому что мы переключились обратно на ветку master, в которой такого файла не существует. Чтобы он появился, нужно воспользоваться ``` git merge <name branch>``` для объединения веток (применения изменений из ветки amazing_new_feature к основной версии проекта).

```sh
git merge amazing_new_feature
```
Теперь ветка master актуальна. Ветка amazing_new_feature больше не нужна, и ее можно удалить.

```sh
git branch -d awesome_new_feature
```
Если хотите создать копию удаленного репозитория - используйте ```git clone```. Однако если вам нужна только определенная его ветка, а не все хранилище - после ```git clone ``` выполните следующую команду в соответствующем репозитории:

```sh
git checkout -b <имя ветки> origin/<имя ветки>
```
После этого, новая ветка создается на машине автоматически.

## Часть 4. Разрешение конфликтов при слиянии
Конфликты регулярно возникают при слиянии ветвей или при отправке чужого кода. Иногда конфликты исправляются автоматически, но обычно с этим приходится разбираться вручную — решать, какой код остается, а какой нужно удалить.
Давайте посмотрим на примеры, где мы попытаемся слить две ветки под названием ```john_branch``` и ```tim_branch```. И Тим, и Джон правят один и тот же файл: функцию, которая отображает элементы массива.
Джон использует цикл:
```ah
// Use a for loop to console.log contents.
for(var i=0; i<arr.length; i++) {
console.log(arr[i]);
}
```
Тим предпочитает forEach:
```sh
// Use forEach to console.log contents.
arr.forEach(function(item) {
console.log(item);
});
```
Они оба коммитят свой код в соответствующую ветку. Теперь, если они попытаются слить две ветки, они получат сообщение об ошибке:

```sh
git merge tim_branch
Auto-merging print_array.js
CONFLICT (content): Merge conflict in print_array.js
Automatic merge failed; fix conflicts and then commit the result.
```
Система не смогла разрешить конфликт автоматически, значит, это придется сделать разработчикам. Приложение отметило строки, содержащие конфликт:
```sh
<<<<<<< HEAD // Use a for loop to console.log contents. for(var i=0; i<arr.length; i++) { console.log(arr[i]); } ======= // Use forEach to console.log contents. arr.forEach(function(item) { console.log(item); }); >>>>>>> Tim's commit.
```
Над разделителем ======= мы видим последний (HEAD) коммит, а под ним - конфликтующий. Таким образом, мы можем увидеть, чем они отличаются и решать, какая версия лучше. Или вовсе написать новую. В этой ситуации мы так и поступим, перепишем все, удалив разделители, и дадим git понять, что закончили.

```sh
// Not using for loop or forEach.
// Use Array.toString() to console.log contents.
console.log(arr.toString());
```
Когда все готово, нужно закоммитить изменения, чтобы закончить процесс:

```sh
git add -A
git commit -m "Array printing conflict resolved."
```
Как вы можете заметить, процесс довольно утомительный и может быть очень сложным в больших проектах. Многие разработчики предпочитают использовать для разрешения конфликтов клиенты с графическим интерфейсом. (Для запуска нужно набрать ```git mergetool```).

# Глава 7. Как удалять ветки в Git?
Бывают ситуации, когда после слива каких-то изменений из рабочей ветки в исходную версию проекта, ее, по правилам хорошего тона, необходимо удалить, чтобы она более не мешалась в вашем коде. Но как это сделать?
Для локально расположенных веток существует команда:

```sh
git branch -d <имя ветки>
```
где флажок -d являющийся опцией команды ```git branch``` - это сокращенная версия ключевого слова --delete, предназначенного для удаления ветки, а <имя ветки> – название ненужной нам ветки.
Однако тут есть нюанс: удалить текущую ветку, в которую вы, в данный момент просматриваете - нельзя. Если же вы все-таки попытаетесь это сделать, система отругает вас и выдаст ошибку с таким содержанием:
```sh
Error: Cannot delete branch local_branch_name checked out at название_директории
```
Так что при удалении ветвей, обязательно переключитесь на другой branch.

# Глава 8. Настройка .gitignore
В большинстве проектов есть файлы или целые директории, в которые мы не хотим (и, скорее всего, не захотим) коммитить. Мы можем удостовериться, что они случайно не попадут в ```git add -A``` при помощи файла .gitignore

Создайте вручную файл под названием .gitignore и сохраните его в директорию проекта.
Внутри файла перечислите названия файлов/папок, которые нужно игнорировать, каждый с новой строки.
Файл .gitignore должен быть добавлен, закоммичен и отправлен на сервер, как любой другой файл в проекте.
Вот хорошие примеры файлов, которые нужно игнорировать:
```sh
Логи
Артефакты систем сборки
Папки node_modules в проектах node.js
Папки, созданные IDE, например, Netbeans или IntelliJ
Разнообразные заметки разработчика.
```
Файл .gitignore, исключающий все перечисленное выше, будет выглядеть так:
```sh
*.log
build/
node_modules/
.idea/
my_notes.txt
```
Символ слэша в конце некоторых линий означает директорию (и тот факт, что мы рекурсивно игнорируем все ее содержимое). Звездочка, как обычно, означает шаблон.

# Глава 9. Удаленные репозитории
Сейчас наш коммит является локальным — существует только в директории .git на нашей файловой системе. Несмотря на то, что сам по себе локальный репозиторий полезен, в большинстве случаев мы хотим поделиться нашей работой или доставить код на сервер, где он будет выполняться.

## Часть 1. Что такое удаленный репозиторий
Репозиторий, хранящийся в облаке, на стороннем сервисе, специально созданном для работы с git имеет ряд преимуществ. Во-первых - это своего рода резервная копия вашего проекта, предоставляющая возможность безболезненной работы в команде. А еще в таком репозитории можно пользоваться дополнительными возможностями хостинга. К примеру -визуализацией истории или возможностью разрабатывать вашу программу непосредственно в веб-интерфейсе.
Клонирование. Это когда вы копируете удаленный репозиторий к себе на локальный ПК. Это то, с чего обычно начинается любой проект. При этом вы переносите себе все файлы и папки проекта, а также всю его историю с момента его создания. Чтобы склонировать проект, сперва, необходимо узнать где он расположен и скопировать ссылку на него. В нашем руководстве мы будем использовать адрес https://github.com/gulden-geekbrains/version_control, но вам посоветуем, попробовать создать свой репозиторий в GitHub:

```sh
git clone https://github.com/gulden-geekbrains/version_control
```
При клонировании в текущий каталог, там будет создана папка, в которую поместятся все проектные файлы и скрытая директория .git, с самим репозиторием, или с необходимой информацией о нем. В такой ситуации, для клонируемого репозитория, по умолчанию, будет создана папка с одноименным названием, но его можно залить и в другую директорию, например:
```sh
git clone https://github.com/gulden-geekbrains/version_control new-folder
```

## Часть 2. Подключение к удаленному репозиторию
Чтобы загрузить что-нибудь в удаленный репозиторий, сначала нужно к нему подключиться. Регистрация и установка может занять время, но все подобные сервисы предоставляют хорошую документацию.
Чтобы связать наш локальный репозиторий с репозиторием на GitHub, выполним следующую команду в терминале. Обратите внимание, что нужно обязательно изменить URL репозитория на свой.

```sh
git remote add origin https://github.com/BilykIgor1987/my_first_repo.git
```
Проект может иметь несколько удаленных репозиториев одновременно. Чтобы их различать, мы дадим им разные имена. Обычно главный репозиторий называется origin.

... или создайте новый репозиторий в командной строке на ПК
```sh
echo "# POSOW" >> README.md     *создаем файл README*
git init                        *инициализация репозитория на ПК*
git add README.md               *добавили в отслеживание файл README*
git commit -m "first commit"    *добавили первый коммит*
git branch -M main              *переименовали ветку в "main"*
git remote add origin https://github.com/BilykIgor1987/POSOW.git    *связали папку на ПК с папкой на GitHub*
git push -u origin main         *отправили ветку "main" в репозиторий на GitHub*
```
... или запустите существующий репозиторий из командной строки
```sh
git remote add origin https://github.com/BilykIgor1987/POSOW.git
git branch -M main
git push -u origin main
```

## Часть 3. Отправка изменений на сервер
Этот процесс происходит каждый раз, когда мы хотим обновить данные в удаленном репозитории.
Команда, предназначенная для этого ```git push -u origin main```. Она принимает два параметра: имя удаленного репозитория (мы назвали наш origin) и ветку, в которую необходимо внести изменения (master — это ветка по умолчанию для всех репозиториев).

```sh
git git push -u origin main
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 924 bytes | 924.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/BilykIgor1987/my_first_repo.git
branch 'main' set up to track 'origin/main'.
```
Эта команда немного похожа на ```git fetch```, с той лишь разницей, что при помощи fetch мы импортируем коммиты в локальную ветку, а применив ```git push```, мы экспортируем их из локальной в удаленную. Если вам необходимо настроить удаленную ветку используйте ```git remote```. Однако пушить надо осторожно, ведь рассматриваемая команда перезаписывает безвозвратно все изменения. В большинстве случаев, ее используют, чтобы опубликовать выгружаемые локальные изменения в центральный репозиторий. А еще ее применяют для того, чтобы поделиться, внесенными в локальный репозиторий, нововведениями, с коллегами или другими удаленными участниками разработки проекта. Подытожив сказанное, можно назвать ```git push``` - командой выгрузки, а ```git pull``` и ```git fetch``` - командами загрузки или скачивания. После того как вы успешно запушили измененные данные, их необходимо внедрить или интегрировать, при помощи команды слияния ```git merge```.
В зависимости от сервиса, который вы используете, вам может потребоваться аутентифицироваться, чтобы изменения отправились. Если все сделано правильно, то когда вы посмотрите в удаленный репозиторий при помощи браузера, вы увидите файл репозитория.

## Часть 4. Запрос изменений с сервера
Если вы сделали изменения в вашем удаленном репозитории, другие пользователи могут скачать изменения при помощи команды pull.

```sh
git pull --rebase
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 2), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), 731 bytes | 11.00 KiB/s, done.
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
hint: Resolve all conflicts manually, mark them as resolved with
hint: "git add/rm <conflicted_files>", then run "git rebase --continue".
hint: You can instead skip this commit: run "git rebase --skip".
hint: To abort and get back to the state before "git rebase", run "git rebase --abort".
```
Так как были изменения они наложились на версию ПК и скопировались в репозиторий на ПК.
Далее разрешаем конфликт, то что есть, что пришло, оба варианта, либо правим и делаем свою версию. Дальше Принимаем изменения.

## Часть 5. Как удалить локальный репозиторий
Вам не понравился один из ваших локальных Git-репозиториев и вы хотите стереть его со своей машины. Для этого вам всего лишь надо удалить скрытую папку «.git» в корневом каталоге репозитория. Сделать это можно 3 способами:

1. Проще всего вручную удалить эту папку «.git» в корневом каталоге «Git Local Warehouse».
2. Также удалить, не устраивающий вас, репозиторий можно на github. Открываете нужный вам объект и переходите в пункт меню Настройки. Там, прокрутив ползунок вниз, вы попадете в зону опасности, где один из пунктов будет называться «удаление этого хранилища».
3. Последний метод удаления локального хранилища через командную строку, для этого в терминале необходимо ввести следующую команду:

```sh
cd repository-path/
rm -r .git
```