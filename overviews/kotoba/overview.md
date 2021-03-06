###Котоба<span style="vertical-align: super;font-size:x-small;">sm</span>
>Котоба (от японского 言葉 — слово, понятие) есть концепт движка для имиджбордов с рядом функций, которые доселе не находили себе применения в других движках (на момент создания идеи). Ежели говорить коротко, то это возможность пользователю борды в значительной степени настраивать интерфейс сайта в соответствие со своими собственными соображениями удобства. 

>Для этого предполагается включить в движок систему регистрации аккаунтов, дабы настройки привязывались к UID пользователя. При этом возможность постинга без регистрации сохраняется (конфигурация сайта будет просто доступна так, как её установил администратор ресурса). Впрочем, предполагается также возможность введения режима «только чтение» для незарегистрированных посетителей, которая остаётся на усмотрение создателя сайта. Опциональны манипуляции с капчей. Следует отметить, что в отличие от форумов с регистрацией, аватарами и смайликами, на Котобе сохраняется анонимность пользователей: ни зарегистрированные, ни незарегистрированные посетители не могут видеть ID друг друга и их «статус» никоим образом не отображается при постинге. То есть, зарегистрированый пользователь просто будет видеть в меню ссылку на страницу настроек и всё. 

>Среди планируемых настроек можно назвать, например, возможность выбора языка интерфейса, задание количества тредов на странице и многого из того, что ныне позволяют делать многочисленные пользовательские скрипты. Почему же тогда не продолжать использовать их? А потому, что скрипты корректно работают далеко не во всех браузерах, да и не всегда у человека будет возможность использовать для доступа в Интернеты именно свой браузер со всеми установленными дополнениями. Котоба же должна будет работать «как есть» — то есть все функции будут изначально заложены в неё, а настройки будут храниться для аккаунта, для которого достаточно помнить пароль. 

>В качестве языка выбран PHP, ибо он поддерживается большинством хостингов, в отличие от Перла и Питона (тем паче, что на них движок напишут и без нас).

### Установка

Для того, чтобы установить котобу, воспользуйтесь этим [скриптом](http://code.google.com/p/kotoba-ib/downloads/detail?name=install-1320755092.php&can=2&q=)<br />
Достаточно скачать скрипт и запустить его в терминале, предварительно отредактировав параметры в исходном коде установщика.<br />
Использование установочного скрипта предполагает, что у вас уже установлена и сконфигурирована связка Apache2 MySQL PHP<br />
Конфигурационный файл Apache должен быть доступен по адресу /etc/httpd/conf/httpd.conf<br />
Так же нужно будет установить subversion и 7z, если они не установлены.<br />
После завершения работы скрипта необходимо будет скачать и установить PHPTAL.<br />
Как это сделать описано в разделе ручная установка этого обзора.

Если возникнут какие-либо проблемы при установке, то можно попробовать воспользоваться инструкцией, которую я приведу ниже.<br />
Для того, чтобы установить его в винде, придётся разбираться самому, ибо установочный скрипт предназначен только для линуксов.

### Ручная установка
Создать директорий, где будет создана рабочая копия котобы:

	mkdir /tmp/kotoba
Создать директорий назначения, где будет работать движок:

	mkdir /var/www/kotoba

Установить [mbstring](http://php.net/manual/ru/mbstring.installation.php), если не установлен.

Загрузить котобу:

	svn checkout https://kotoba-ib.googlecode.com/svn/trunk/kotoba-ib/ /tmp/kotoba

Скопировать всё из `/tmp/kotoba`, кроме следующих директорий: `res`, `nbproject`, `phpdoc`, `docs`

Создать базу данных и таблицы для неё:

	mysql -u пользователь -pпароль < /tmp/kotoba/res/create_struct.sql
	mysql -u пользователь -pпароль -D kotoba < /tmp/kotoba/res/create_procedures.sql

Скопировать `/tmp/kotoba/config.default` в `/var/www/kotoba/config.php`

Скачать и установить Smarty:

	wget -P /tmp/ http://www.smarty.net/files/Smarty-3.0.4.tar.gz
	tar -zxvf /tmp/Smarty-3.0.4.tar.gz -C /tmp/
	cp -r /tmp/Smarty-3.0.4/* /var/www/kotoba/smarty/

Скачать и установить shi:

	wget -P /tmp/ http://kotoba-ib.googlecode.com/files/shi-1320754922.7z
	7z x -o/tmp /tmp/shi-1320754922.7z
	cp /tmp/shi/shi_save.php /var/www/kotoba/lib/shi_save.php
	cp /tmp/shi/spainter_all.jar /var/www/kotoba/shi/spainter_all.jar
	cp /tmp/shi/spainter_normal.html /var/www/kotoba/shi/spainter_normal.html
	cp /tmp/shi/sp.js /var/www/kotoba/shi/sp.js
	cp /tmp/shi/res/* /var/www/kotoba/shi/res/

Скачать и установить PHPTAL:
	
	wget -P /tmp/ http://phptal.org/files/PHPTAL-1.2.2.tar.gz
	tar -zxvf /tmp/PHPTAL-1.2.2.tar.gz -C /tmp/
	cp -r /tmp/PHPTAL-1.2.2/* /var/www/kotoba/

Скопировать .htaccess Файлы:

	cp /tmp/kotoba/res/.htaccess1 /var/www/kotoba/.htaccess
	cp /tmp/kotoba/res/.htaccess2 /var/www/kotoba/smarty/.htaccess
	cp /tmp/kotoba/res/.htaccess2 /var/www/kotoba/log/.htaccess
	cp /tmp/kotoba/res/.htaccess2 /var/www/kotoba/sessions/.htaccess

Добавить обязательные директивы в конфиг апача:
	
	### Kotoba
	#
	# Options requied or recommended for Kotoba.

	<Directory "/var/www/kotoba">
	    AllowOverride FileInfo Limit Indexes
	</Directory>

Перезапустить Apache

	/etc/init.d/apache2 restart

Отредактировать `/var/www/kotoba/config.php`

Установить необходимые права доступа на директории и файлы в `/var/www/kotoba`

Открыть страницу настроек котобы в вашем браузере
	http://your-server-domain-or-ip/edit_settings.php

Отредактировать настройки и сохранить их

Открыть скрытыю информационную страницу котобы в браузере:
	http://your-server-domain-or-ip/my_id.php

Вы увидите ваш ID. Например, 2

Теперь переместите вашего пользователя в админскую группу, выполнив следующую команду:
	
	~# mysql -u root -p
	> use kotoba;
	> update `user_groups` set `group`=4 whete `user`=ваш_ид;
	> exit

Перейдите назад к странице настроек и загрузите ваши настройки.<br />
Тогда вы должны увидеть ссылку на меню управления вверху справа на странице.<br />
Удачи!

###Административные функции и функции модераторов

####Основной скрипт модератора

Здесь располагается форма, которая позволяет выбрать сообщения по следующим параметрам:<br />
\- Доска.<br />
\- Дата.<br />
\- Номер.<br />
\- IP-адрес.<br />
\- Только с вложениями или нет.<br />

С выбранными сообщениями можно совершить следующие действия:<br />
\- Забанить авторов<br />
Тип бана: Бан или Бан в фаерволе<br />
\- Удалить сообщения<br />
Тип удаления: Удалить сообщение, Удалить файл, Удалить последние сообщения.

####Жалобы

Отображение жалоб конкретной доски или со всех досок сразу.
Бан постера, на сообщение которого пожаловались. Удаление сообщения. Возможно удалить жалобу.

####Баны

>Чтобы удалить баны, пометьте нужные строки. Чтобы забанить определёный ip, введите его
в качестве начала и конца диапазона, опционально введите причину и выберите время бана из предложенного списка.
Чтобы забанить сеть, введите начало и конец диапазона её адресов. Чтобы разбанить определённый ip, введите его
в соотвествующее поле ввода; помните, при этом будут удалены все баны, в диапазон которых входит этот ip.

Время истечения от 10 секунд до месяца.<br />
Возможно разбанить IP и удалить запись.

####Бан в фаерволе
Пустая страница, если не считать заголовок. Видимо ещё не доделано.

####Бан по списку

>Выберите файл , содержащий диапазоны блокируемых адресов.<br />
Каждый новый диапазон должен начинаться с новой строки (быть разделены символом \n).<br />
Например:<br />
127.0.0.1 127.0.0.3<br />
127.0.0.5 127.0.0.5<br />
Забанит поциентов с адресами с 127.0.0.1 по 127.0.0.3 включительно и поциента с адресом 127.0.0.5

####Доски

>Чтобы добавить доску, введите все необходимые параметры (помечены звёздочкой*).
 Чтобы отредактировать параметры существующих досок, отредактируйте соотвествующие поля таблицы.
 Чтобы удалить доску, отметьте её.

Параметры:

* Имя	
* Заголовок	
* Аннотация	
* Бамплимит
* Флаг скрытия имени отправителя
* Имя отправителя по умолчанию
* Флаг вложений
* Включение интеграции с макрочаном
* Включение вложения видео с ютуба
* Включение капчи 
* Включение перевода текста сообщения
* Включение отображения страны автора сообщения
* Включение рисования
* Включение идентификатора сообщения
* Политика загрузки одинаковых файлов
* Обработчик автоматического удаления нитей
* Категория
* Удалить доску

По умолчанию доступно 2 скрытые доски: /n/ и /misc/<br />
Но не ясно, как всё-таки скрывать доски.

####Категории

>Пометьте категории для удаления или введине имя новой категории, чтобы создать новую категорию.

По умолчанию доступна одна категория: default

####Нити

Редактирование настроек нитей<br />
Измените параметры и сохраните изменения.

Список доступных параметров:

* Идентификатор.
* Доска.
* Оригинальное сообщение.
* Бамплимит специфичный для нити.
* Флаг закрепления.
* Флаг поднятия нити при ответе.
* Флаг загрузки изображений.
* Нить закрыта.


####Обработчики автоматического удаления нитей

>Редактирование обработчиков удаления нитей<br />
Пометьте обработчики для удаления или введине имя нового обработчика, чтобы зарегистрировать новый обработчик.

####Перенос нити

>Чтобы перенести нить выберите доску, на которой она расположена и введите номер нити. Затем выберите доску, на которую нужно перенести нить.

####Типы загружаемых файлов.

>Чтобы изменить обработчик загружаемых файлов для этого типа файлов, выберите другой обработчик из списка.
 Чтобы изменить сохраняемый тип файла или изменить имя картинки для файлов, не являющихся изображением, измените значение
 в соотвествующих полях ввода. Чтобы удалить тип файлов, пометьте его в соотвествующей колонке. Чтобы добавить тип файлов,
 введите все необходимые данные и сохраните изменения.

Список доступных параметров:

* Тип файла.
* Сохраняемый тип файла.
* Файл является изображеним.
* Обработчик.
* Имя картинки.
* Удалить тип.

####Закрепление типов загружаемых файлов за досками

>Чтобы удалить связи типов файлов с доской, пометьте соответствующие записи.
 Чтобы добавить связь типа файла с доской, выберите доску, тип и сохраните изменения (дублирующиеся записи
 будут проигнорированы).

####Обработчики загружаемых файлов

>Пометьте обработчики для удаления или введине имя нового обработчика,
 чтобы зарегистрировать новый обработчик.

####Удаление висячих вложений
####Загрузка новых данных с Макрочана

####Группы пользователей

>Пометьте группы для удаления или введине имя новой группы, чтобы создать новую группу.

Группы доступные по умолчанию:

* Guests	
* Users	
* Moderators	
* Administrators

####Закрепления пользователей за группами

>Редактирование закреплений пользователей за группами
Введите id пользователя и выберите ему группу из списка, чтобы закрепить пользователя ещё за одной группой
 или найдите id пользователя в списке и измените группу, за которой он закреплён.
 Чтобы удалить закрпление, пометьете его и сохраните изменения.

####Список контроля доступа

>Чтобы изменить права в существующей записи, измение их с помощью флажков. Помните, что если, к примеру, вы
 запретили какой-то группе просматривать какую-то доску, то права на редактирование и модерирование этой доски для этой группы
 не имеют смысла и будут сняты автоматически. Чтобы удалить запись, пометьте её в соотвествующей колонке. Чтобы добавить запись
 введите все необходимые данные и установите желаемые права.

####Произвести архивирование.
####Удалить помеченные на удаление сообщения, нити, связи сообщений и вложений.

####Разное

* Стили.
* Языки.
* Фильтрация слов.
* Спамфильтр.

**Фильтрация слов:**

>Чтобы добавить слово, введите все необходимые параметры. Чтобы отредактировать параметры существующих слов, отредактируйте соотвествующие поля таблицы. Чтобы удалить слово, отметьте её.

Параметры:

* Доска
* Слово
* Замена
* Удалить слово

**Спамфильтр:**

>Введите новый шаблон и нажмите Сохранить, чтобы добавить новый шаблон. Пометьте шаблоны и нажмите Сохранить, чтобы удалить помеченные шаблоны.

####Просмотр лога
Вводим кол-во строк, которое нужно просмотреть в поле "Rows count" и жмём сабмит.<br />
В таблице должны отобразится действия пользователей.<br />
Для каждого действия указаны: Дата, id пользователя, Группы пользователя, IP-адрес, Описание самого действия.

На этом описание админки можно окончить.
****

###Поиск
>Минимальная длина слова: 4.
Отметьте доски для поиска. Если ни одна доска не отмечена, то поиск производится по всем доскам.

Поиск производится только по тексту сообщения.
****
###Настройки

В самом начале отображается идентификатор сессии и через сколько она истекает.

Например:

>Идентификатор сессии: opu8pf5bcu893ntbpu5aumhsj0<br />
Сессия истекает через 6:59

Список доступных параметров:

* Число нитей на странице просмотра доски
* Число сообщений в нити на странице просмотра доски
* Сообщения, в которых число строк превышает это число, будут урезаны при просмотре доски
* Перенаправление: К нити или к доске
* Язык
* Стиль оформления

Так же на этой странице отображается список избранных и скрытых тредов.

Для сохранения настроек нужно ввести ключевое слово.<br />
Потом можно будет загрузить настройки, введя это слово на этой же странице.
Хорошо сделали, годно.
***
### Доски

**Форма постинга:**

* Тема
* Сообщение
* Файл
* Youtube
* Пароль
* Перейти: нить или доска

Сажа доступна только при ответе в тред.

**Блоттер:**

* Типы файлов, доступных для загрузки: jpg png gif jpeg
* Бамплимит доски: 500
* Каталог нитей
Если указана аннотация для доски, то она выводится здесь же.

Над полем ввода сообщения располагается панель BB-кодов<br />
**Доступные BB-коды:**

* курсив
* жирный
* код
* спойлер
* зачёркнутый
* подчёркнутый
* несортированный список
* сортированный список
* урл
* гугл
* википедия
* цитата

**Просмотр нити:**

Под формой для администрации располагается таблица с параметрами треда.<br />
Список параметров:

* Идентификатор (неизменяемый параметр)
* Доска (неизменяемый параметр)
* Оригинальное сообщение (неизменяемый параметр)
* Бамплимит специфичный для нити
* Флаг закрепления
* Флаг поднятия нити при ответе
* Флаг загрузки изображений
* Нить закрыта

Удалить тред можно только кликнув по соответствующей иконке возле ОП-поста.

Возле ОП-поста также располагаются ссылки: скрыть тред, добавить тред в избранное, пожаловаться на пост, удалить файл.
Для остальных постов так же доступны ссылки для жалобы и удаления поста или файла.

Для администраторов возле IP адреса постера находятся следующие кнопки:<br />
Бан, Бан с добавлением текста, Бан и удалить сообщение, Бан и удалить последние сообщения, Бан в фаерволе.
***
###Заключение
Количество функционала впечатляет. Оформление мягкоговоря уёбищное.

Необошлось и без недочётов. Интерфейс админки не очень удобный.<br />
Подробно расписывать нет необходимости, так как всё можно увидеть на скриншотах.

Для того, чтобы загружать пикчи к доске, необходимо сначала указать разрешённые типы файлов и затем настроить их для нужной доски.<br />
Слишком много телодвижений.

Для того, чтобы войти в админку нужно загрузить настройки, созданные при установке движка. Иначе неизвестно как это сделать.<br />
При постинге в тред с сажей, она не отображается.<br />
Ошибки, возникшие при постинге отображаются на отдельной странице.<br />
Прикреплённые пикчи открываются в новом окне.<br />
Ссылки на ответы не обрабатываются.<br />
Ответы на сообщение не показываются.

Если пользователь залогинен под администратором, то нет возможности постить без капкода.<br />
Алсо капкод для админа имеет следующий вид: <span style="color: #800080">❀❀ Админ ❀❀</span>

Последняя ревизия датирована 3 октября 2012 года. И похоже, что движок заброшен.<br />
На этом, думаю, обзор можно считать оконченым.