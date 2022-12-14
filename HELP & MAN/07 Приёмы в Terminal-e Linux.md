# Приёмы работы в командной строке Linux и экономия времени

## 0. Автозавершение команд с использованием клавиши Tab

Например, собираясь скопировать файл с именем my_best_file_1.txt, вы можете просто ввести cp m и нажать Tab для того, чтобы увидеть возможные варианты продолжения команды.

## 1. Переход в последнюю рабочую директорию

`cd -`

## 2. Возврат в домашнюю директорию

`cd ~`

## 3. Вывод на экран содержимого директории

`ll`

## 4. Вызов нескольких команд в одной строке

Представьте, что вам нужно последовательно выполнить несколько команд. Наверное, вы вводите одну команду, потом ждёте, когда она завершится, дальше — вводите следующую?

В подобной ситуации полезным окажется разделитель команд ; (точка с запятой). При таком подходе вы можете ввести несколько команд в одной строке. При этом, в отличие от обычного ввода команд, для выполнения следующей команды не надо ждать завершения предыдущей.

`command_1; command_2; command_3`

## 5. Выполнение нескольких команд в одной строке и условие на успешное завершение предыдущей команды

Только что мы рассмотрели способ вызова нескольких команд в одной строке. Это экономит время. Но что если вам нужно, скажем, при вызове двух команд, чтобы следующая команда была выполнена только в том случае, если предыдущая завершится без ошибок?

Представьте себе, что хотите собрать код, а затем, если сборка оказалась успешной, вызвать make?

В подобной ситуации можно использовать разделитель &&. Этот разделитель позволяет гарантировать то, что следующая команда будет выполнена лишь в том случае, если предыдущая отработает успешно.

`command_1 && command_2`

Вот хороший пример использования &&:

`sudo apt update && sudo apt upgrade`

## 6. Простой поиск и использование ранее введённых команд

Представьте себе, что вы, пару минут или пару часов назад, вводили длинную команду, и вам снова нужна эта команда. Причём, проблема заключается в том, что вспомнить точно эту команду вы не можете.

В подобной ситуации вас спасёт обратный поиск. Данная методика позволяет проводить поиск в истории команд по ключевому слову. Тут достаточно использовать комбинацию клавиш Ctrl + R для запуска обратного поиска и ввести что-то, имеющее отношение к команде. Система просмотрит историю команд и покажет команды, соответствующие введённому запросу.

`Ctrl + R search_term`

По умолчанию показан будет лишь один результат. Для того, чтобы увидеть больше результатов, соответствующих запросу, вам понадобится использовать комбинацию клавиш Ctrl + R снова и снова. Для того, чтобы выйти из режима обратного поиска, нажмите Ctrl + C.

## 7. Разблокировка терминала после случайного нажатия Ctrl + S

Возможно, вы привыкли пользоваться комбинацией клавиш Ctrl + S для сохранения файлов. Но если нажать эти клавиши в терминале Linux, вы его заблокируете.

Если раньше вы, для того, чтобы исправить положение, вынуждены были закрывать и снова запускать терминал — теперь может вздохнуть спокойно, больше вам этого делать не придётся. Для того, чтобы привести терминал в рабочее состояние, просто воспользуйтесь комбинацией клавиш Ctrl + Q.

## 8. Перемещение к началу или концу строки

Представьте себе, что вы вводите длинную команду и где-нибудь посередине понимаете, что должны что-нибудь изменить в её начале. Вероятно, вы используете клавиши-стрелки для того, чтобы сначала переместиться в начало строки, а потом вернуться в конец.

Конечно, в подобной ситуации можно использовать клавиши Home и End, но, как вариант, с помощью комбинации клавиш Ctrl + A можно перейти в начало строки, а с помощью комбинации Ctrl + E — в конец.

## 9. Использование команды less для чтения файлов

Если вам нужно просмотреть файл, особенно — большой, можно попробовать команду cat, но гораздо лучше поискать что-нибудь другое. Дело в том, что cat выведет на экран весь файл, что не так уж и удобно.

Для просмотра файлов можно воспользоваться редакторами вроде Vi или Vim, работающими в терминале, но если вам просто нужно прочесть файл, очень кстати окажется команда less.

less path_to_file

Во время сеанса работы с less можно искать нужные фрагменты текста по ключевым словам, перемещаться по страницам, выводить данные с номерами строк, и так далее.

## 10. Использование предыдущей команды в текущей команде с помощью !!

С помощью !! можно вызвать всю предыдущую команду. Этот приём оказывается особенно полезным, когда вам нужно выполнить команду и оказывается, что для её выполнения нужны привилегии суперпользователя. Например, на рисунке ниже показана ситуация, в которой команда sudo !! позволяет сэкономить немало времени.

## 11. Использование псевдонимов для исправления ошибок ввода

Возможно, вы уже знакомы с командой alias. Её можно использовать для исправления ошибок во введённых командах.

Например, может случиться так, что вы часто вводите gerp вместо grep. Если с вредной привычкой справиться никак не удаётся, запишите псевдоним в свой файл bashrc следующим образом:

`alias gerp=grep`

Теперь вам не придётся перенабирать эту команду если вы введёте её имя неправильно.

## 12. Очистка содержимого файла без удаления самого файла

Если вы хотите очистить содержимое текстового файла, не удаляя сам файл, можете использовать следующую команду:

 `> filename`

Для очистки больших файлов необходимо использовать:

`truncate -s 0 filename`
