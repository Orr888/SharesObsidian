# ПЕРЕМЕННЫЕ ОКРУЖЕНИЯ В LINUX: КАК ПОСМОТРЕТЬ, УСТАНОВИТЬ И СБРОСИТЬ

Переменные окружения (или переменные среды) - это набор пар ключ-значение, которые хранятся в вашем Linux и используются процессами для выполнения определенных операций. Они отвечают за стандартное поведение системы и приложений. При взаимодействии с вашим сервером через сеанс оболочки, есть много информации, которую ваша оболочка обрабатывает, чтобы определить ее поведение и доступы. Некоторые из этих параметров содержатся в настройках конфигурации, а другие определяются пользовательским вводом. Оболочка отслеживает все эти параметры и настройки через окружение. Окружение - это область, которую оболочка создает каждый раз при запуске сеанса, содержащего переменные, определяющие системные свойства. Например, это может быть часовой пояс в системе, пути к определенным файлам, приложения по-умолчанию, локали и многое другое. Переменные окружения также могут использоваться в программах оболочки или в подоболочках для выполнения различных операций.

В этом руководстве мы расскажем, как просматривать, устанавливать и сбрасывать переменные окружения в вашей системе.

## ПЕРЕМЕННЫЕ ОКРУЖЕНИЯ И ПЕРЕМЕННЫЕ ОБОЛОЧКИ

Переменные имеют следующий формат:
```
KEY=value
KEY="Some other value"
KEY=value1:value2
```
Должны соблюдаться следующие правила:

- Имена переменных чувствительны к регистру (регистрозависимы). Переменные окружения должны быть написаны большими буквами (UPPER CASE).
- Несколько значений переменных разделяются двоеточием `:`
- Вокруг символа `=` нет пробела


Переменные можно разделить на две категории:

- **Переменные окружения (Environmental Variables)** - это переменные, которые определены для текущей оболочки и наследуются любыми дочерними оболочками или процессами. Переменные окружения используются для передачи информации в процессы, которые порождаются из оболочки.
- **Переменные оболочки (Shell Variables)** - это переменные, которые содержатся исключительно в оболочке, в которой они были установлены или определены. Они часто используются для отслеживания эфемерных данных, например, текущего рабочего каталога.


## ВЫВЕСТИ СПИСОК ВСЕХ ПЕРЕМЕННЫХ ОКРУЖЕНИЯ И ОБОЛОЧКИ


Мы можем увидеть список всех наших переменных окружения, используя команды `env` или `printenv`. В состоянии по умолчанию они должны работать точно так же:

```
SHELL=/bin/bash
TERM=xterm
USER=demouser
LS_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:su=37;41:sg=30;43:ca:...
MAIL=/var/mail/demouser
PATH=/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games
PWD=/home/demouser
LANG=en_US.UTF-8
SHLVL=1
HOME=/home/demouser
LOGNAME=demouser
LESSOPEN=| /usr/bin/lesspipe %s
LESSCLOSE=/usr/bin/lesspipe %s %s
_=/usr/bin/printenv	
```


Это типичный вывод как для `env`, так и для `printenv`. Разница между этими двумя командами проявляется только в их более конкретной функциональности. Например, с помощью `printenv` вы можете запросить значения отдельных переменных:

```
printenv SHELL
```

Получим:

```
/bin/bash
```

А как посмотреть переменные оболочки?

Для этого можно использовать команду `set`. Если мы введем `set` без каких-либо дополнительных параметров, мы получим список всех переменных оболочки, переменных окружения, локальных переменных и функций оболочки:

```
BASH=/bin/bash
BASHOPTS=checkwinsize:cmdhist:expand_aliases:extglob:extquote:force_fignore:histappend:interactive_comments:login_shell:progcomp:promptvars:sourcepath
BASH_ALIASES=()
BASH_ARGC=()
BASH_ARGV=()
BASH_CMDS=()
. . .
```

Тут мы получим гигантский вывод, поэтому стоит использовать `less`, чтобы разделить содержимое на страницы:

```
set | less
```

Также для вывода переменной оболочки можно использовать команду `echo`:

```
echo $ BASH_VERSION
```

Получим ответ:

```
4.4.19 (1) -release
```

## ОБЩИЙ НАБОР ПЕРЕМЕННЫХ ОКРУЖЕНИЯ В LINUX

Посмотрим на общий набор переменных окружения, которые вы можете найти в своей системе.

- **USER**: текущее имя пользователя, использующего систему
- **EDITOR**: какая программа запускается для редактирования файла на вашем хосте
- **HOME**: домашний каталог текущего пользователя
- **PATH**: список каталогов, разделенных двоеточиями, в которых система ищет команды
- **PS1**: основная строка приглашения (для определения отображения приглашения оболочки)
- **PWD**: текущий рабочий каталог
- **_**: самая последняя команда, выполненная в системе пользователем
- **MAIL**: путь к почтовому ящику текущего пользователя
- **SHELL**: оболочка, используемая для интерпретации команд в системе, она может быть много разных (например, bash, sh, zsh или другие)
- **LANG**: кодировка языка, используемая в системе
- **DESKTOP_SESSION**: текущий рабочий стол, используемый на вашем хосте (GNOME, KDE)
- **HISTFILESIZE**: количество строк истории команд, сохраненных в файле истории
- **HISTSIZE**: количество строк истории, разрешенных в памяти
- **UID**: текущий UID для пользователя
- **HOSTNAME**: имя компьютера системы
- **TERM**: указывает тип терминала
- **OLDPWD**: предыдущий рабочий каталог
- **BASHOPTS**: список параметров, которые использовались при выполнении bash.
- **BASH_VERSION**: версия bash, выполняемая в удобочитаемой форме.
- **BASH_VERSINFO**: версия bash с машиночитаемым выводом.
- **COLUMNS**: Количество столбцов в ширину, которые используются для вывода вывода на экран.
- **DIRSTACK**: стек каталогов, доступных с помощью команд pushd и popd.
- **IFS**: внутренний разделитель полей для разделения ввода в командной строке. По умолчанию это пробел.
- **SHELLOPTS**: параметры оболочки, которые можно установить с помощью параметра set.


## УСТАНОВКА ПЕРЕМЕННЫХ ОКРУЖЕНИЯ В LINUX


В Linux у вас есть много разных способов установки переменных окружения в зависимости от того, хотите ли вы сделать их постоянными или нет.

Самый простой способ установить переменные окружения - использовать команду `export`.

```
export VAR="value"	
```


Для примера создаим новую переменную, а затем экспортируем ее.

Чтобы создать новую переменную оболочки с именем NEW_VARIABLE и значением "test", и затем сразу экспортировать ее введите:

```
export NEW_VARIABLE='test'
```

И проверяем:

```
printenv NEW_VARIABLE

test
```

Используя export, ваша переменная окружения будет установлена для текущего сеанса оболочки. Как следствие, если вы откроете другую оболочку или перезапустите свою систему, переменная окружения больше не будет доступна.

## УСТАНОВИТЬ ПОСТОЯННЫЕ ПЕРЕМЕННЫЕ ОКРУЖЕНИЯ В LINUX


Как вы видели в предыдущем разделе, переменные окружения не были постоянными при перезапуске оболочки. Однако существует способ сделать ваши изменения постоянными: с помощью системных файлов, которые читаются и выполняются в определенных условиях.

### ИСПОЛЬЗОВАНИЕ ФАЙЛА .BASHRC


Самый популярный способ постоянной установки переменных среды - это добавить их в файл `.bashrc`.

Файл `.bashrc` - это скрипт, выполняемый всякий раз, когда вы инициализируете сеанс интерактивной оболочки. Как следствие, когда вы запускаете новый терминал через интерфейс **GNOME** или просто используете screen сессию, вы будете использовать файл `.bashrc`.

Например, добавьте следующие записи в ваш файл `.bashrc`:

```
export TZ="America/New_York"
```

Сохраните ваш файл и используйте команду `source` для перезагрузки файла `bashrc` для текущего сеанса оболочки.

```
source ~/.bashrc	
```

Вы можете вывести новую переменную окружения с помощью `printenv` и посмотреть, дату в Linux, изменив TZ.

```
$ printenv TZ
America/New_York

$ date
Sat 19 Jan 2020 10:03:00 AM EDT
```

Отлично, ваши изменения теперь сохраняются после перезагрузки оболочки или системы!

### ИСПОЛЬЗОВАНИЕ ФАЙЛА .BASH_PROFILE

В качестве альтернативы, если вы планируете подключаться к своим сеансам с помощью login оболочек, вы также можете добавить переменные окружения непосредственно в файл `.bash_profile`.

```
$ export TZ="America/New_York"

$ source ~/.bash_profile
```


### ИСПОЛЬЗОВАНИЕ ETC/ENVIRONMENT
Если вам нужно применить определенные переменные окружения для всех, то определить общесистемные переменные окружения. Чтобы установить общесистемные переменные окружения в Linux, вам нужно экспортировать переменные в файл `/etc/environment`.

Например, чтобы изменить редактор, используемый глобально, вы можете изменить переменную `EDITOR` в файле окружения.

```
$ export EDITOR="vi"
```

Теперь попробуйте войти в систему как под разными пользователями в вашей системе, и вы увидите, что переменная `EDITOR` установлена для всех на сервере.

### УСТАНОВИТЬ ПЕРЕМЕННЫЕ ОКРУЖЕНИЯ В ОДНОЙ СТРОКОЙ

Теперь, когда вы знаете все подробности о том, как устанавливать переменные окружения, вы можете использовать эти шорткаты для их легкой установки.

Для `.bashrc`:

```
echo "export VAR="value"" >> ~/.bashrc && source ~/.bashrc
```

Для `.bash_profile`:

```
echo "export VAR="value"" >> ~/.bash_profile && source ~/.bash_profile
```

Для `/etc/environment`:

```
echo "export VAR="value"" >> /etc/environment && source /etc/environment
```



## СБРОСИТЬ ПЕРЕМЕННЫЕ ОКРУЖЕНИЯ В LINUX


Теперь, когда вы установили много переменных окружения в своей системе, вы можете отменить некоторые из них, если вы больше не используете их. В Linux существует два способа сброса переменных окружения: с помощью команды unset или путем удаления записей переменных в ваших системных файлах.

### ИСПОЛЬЗОВАНИЕ КОМАНДЫ UNSET

Чтобы удалить переменную окружения, используйте команду `unset` со следующим синтаксисом:

```
unset <variable>
```

Выглядит это так:

```
unset USERNAME

printenv USERNAME
<nothing>
```

### ИСПОЛЬЗОВАНИЕ КОМАНДЫ SET -N

Кроме того, вы можете сбросить переменные окружения, используя команду `set` с флагом `-n-n`.

```
set -n USERNAME

printenv USERNAME
<nothing>
```

### УСТАНОВИТЬ ПЕРЕМЕННУЮ ОКРУЖЕНИЯ PATH В LINUX

В системах Linux очень часто задают переменную окружения `PATH`, чтобы система могла находить команды.

Чтобы отобразить текущую переменную окружения `PATH`, выполните команду `printenv`:

```
printenv PATH

/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games
```

Чтобы установить переменную окружения `PATH`, добавьте строку `export` в файл `.bashrc` и используйте с ним команду `source`:

```
echo "export PATH=":$PATH"" >> ~/.bashrc && source ~/.bashrc

printenv PATH
:/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games
```

Успех! Вы успешно обновили переменную окружения `PATH` в Linux.

## ЗАКЛЮЧЕНИЕ

В сегодняшнем руководстве вы узнали, что переменные окружения в Linux можно задавать несколькими способами: с помощью команды `export`, а также путем изменения некоторых системных файлов, чтобы сделать их постоянными.

Вы также узнали, что можно сбросить переменные окружения и как легко обновить переменную окружения `PATH`.


[Дополнительная информация в Arch-Wiki (Environment variables (Русский))](https://wiki.archlinux.org/title/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9))