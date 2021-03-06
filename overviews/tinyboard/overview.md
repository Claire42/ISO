###Требования
1.  PHP >= 5.2.5
2. MySQL server
3. [mbstring](http://www.php.net/manual/en/mbstring.installation.php) 
4. [PHP GD](http://www.php.net/manual/en/intro.image.php)
5. [PHP PDO](http://www.php.net/manual/en/intro.pdo.php)

>Мы пытаемся сделать Tinyboard совместимым с большинством веб серверов и операционных систем. 
Tinyboard не включает Apache ```.htaccess``` файл. Он не понадобится совсем

### Рекомендуется
1. PHP >= 5.3
2. MySQL server >= 5.5.3
3. ImageMagick (command-line ImageMagick или GraphicsMagick).
4. [APC (Alternative PHP Cache)](http://php.net/manual/en/book.apc.php), [XCache](http://xcache.lighttpd.net/) или [Memcached](http://www.php.net/manual/en/intro.memcached.php)

###Установка
1. Загрузите и извлеките Tinyboard в ваш веб директорий или получите последнюю development версию с помощью следующей команды:<br />
`git clone git://github.com/savetheinternet/Tinyboard.git`
2. Запустите ```install.php``` в вашем веб браузере и следуйте подсказкам.
3. Запустите ```mod.php``` в браузере и авторизуйтесь. Логин/пароль: **admin / password**.

Не забудьте сменить пароль для администраторского аккаунта.

Смотрите также: [Configuration Basics](http://tinyboard.org/docs/?p=Config).

###Админ-панель

####Доски

* Список досок
* Создать новую доску

Параметры доски: URI, заголовок, подзаголовок.<br />
Удаление находится в форме редактирования доски.

Если перейти по доске из админки, то при просмотре списка тредов или же самих тредов<br />
дополнительно возле постов выводятся ссылки на админские фичи.<br />
Если же перейти просто к доске не из админки, то админские фичи не отображаются.<br />
Отлично. Не нужно сбрасывать сессию, для того, чтобы просматривать доски и постить анонимно.

####Сообщения

* Посмотреть все записи доски объявлений
* Новости
* Входящие сообщения

Доска объявлений отображается только в админке.<br />
Видимо нужна лишь для администраторов и модераторов.<br />
Так же здесь реализована приватная переписка между пользователями, о чем свидетельствует список входящих сообщений.<br />
Можно даже переписываться с самим собой.<br />
Новости. Без установки дополнений сами по себе они скорее всего не нужны, т.к. кроме админки их нигде не увидеть.

####Администрирование

* Очередь сообщений (reports queue)
* Бан лист
* Управление пользователями
* Управление темами
* Мод лог
* Ребилд
* Конфигурация

Управление пользователями:<br />
ID, Username, Type (Админ, модер, уборщик), Boards (либо все, либо какие-то конкретные), Last action<br />
Для каждого элемента списка так же доступны ссылки: \[log\] - Анальный зонд. \[edit\] - отредактировать (если есть полномочия). \[PM\] - Отправить приватное сообщение.<br />
Создание/Редактирование пользователя:<br />
Задаём юзернейм, пароль (при редактировании заполнять необязательно), группу, список досок и готово.

Управление темами:<br />
Незнаю, почему этот пункт назван именно так.<br />
Правильнее будет заменить слово "тема" на "дополнение".

Доступны следующие <span style="text-decoration: line-through;">дополнения</span> темы:

Имя: Categories<br />
Версия: v0.3<br />
Описание: Ориентированная на группы, category-aware модификация фреймовой темы,с удаляемым сайдбаром. Требует наличие параметра $config['categories'].

Имя: Sitemap Generator<br />
Версия: v1.0<br />
Описание: Генерирует XML карту сайта для помощи поисковикам в поиске всех тредов и страниц.

Имя: Basic<br />
Версия: v0.9.1<br />
Описание: Листинг новостей для главной страницы. Рекомендуется включить бордлинки для этой темы.

Имя: Catalog<br />
Версия: v0.1<br />
Описание: Показывает каталог поста.

Имя: RRDtool<br />
Версия: v0.2<br />
Описание: График основной статистики. Использует расширение PHP RRDtool.

Имя: RecentPosts<br />
Версия: v1.0<br />
Описание: Показывает недавние посты и изображения, как на 4chan.

Имя: Frameset<br />
Версия: v0.1<br />
Описание: Использует базовый макет фреймов, со списком досок и страниц на боковой панели слева страницы. Пользователям не придётся покидать главную страницу; они могут делать всё, просматривая одну страницу.

Для каждого дополнения доступны следующие действия:<br />
Reconfigure, Rebuild, Uninstall для установленного и Install для не установленного дополнения.<br />
Так же для некоторых дополнений имеются скриншоты. Если дополнение установлено, то скриншоты обводятся красной рамкой.

Ребилд:

* Очистка кэша
* Rebuild Javascript
* Rebuild index pages
* Rebuild thread pages
* Rebuild themes
* Rebuild replies
* Все доски или какие-либо конкретные

Конфигурация:

>Любые изменения, которые вы сделаете здесь будут просто добавлены к `inc/instance-config.php`<br />
Если вы хотите получить больше возможностей для кастомизации, вы можете отредактировать конфиг на прямую.<br />
Эта страница предназначена для быстрого внесения изменений и для тех, кто не имеет базовых знаний PHP.

Опций просто нереально много.<br />
Редактор представлен в виде таблицы со следующими колонками: Имя, Значение, Тип, Описание.<br />
Так же рядом со значением указывается значение по умолчанию.

Непонравилось только то, что все опции свалены в кучу и нет никакого разбиения по секциям.<br />
Читать немного сложновато, не говоря о том, чтобы найти что-либо.

####Поиск
Поиск регистронезависимый и основан на ключевых словах. Для поиска точной фразы используйте "кавычки". Для подстановки используйте звёздочку (*).<br />
Производится поиск по следующим направлениям: Посты, Ip addresses notes, модлог, баны. Можно выбрать только что-то одно.

###Доски

Форма: Имя, Email, Тема, Комментарий, Файл, Флаги(Прикрепленный, Закрытый, Raw HTML. Выводятся только для админа и только при создании треда), Пароль.<br />
При отправке поста также, как и в TinyIB перенаправляет на доску вместо треда.<br />
Разметка: `>цитата`, `>>номерПоста`, `**внезапноСпойлер**`<br />
Raw HTML позволяет использовать тег `<script />`<br />
Изображение раскрывается сразу в посте при клике по нему.

Для администратора при клике по IP Адресу попадаем на страницу со всеми постами под этим IP.<br />
На этой странице можно добавить заметки для этого IP или забанить, как на всех досках, так и на конкретной.<br />
Так же имеется модлог, где указывается кто, что и когда совершил с этим IP (добавил/удалил заметку, забанил/разбанил).<br />
Можно забанить самого себя, указать любое время бана или даже забанить навсегда.

Помимо IP адреса еще имеются следующие ссылки, названия которых, если я не ошибаюсь, можно изменить в конфиге: 

* \[D\] - Удалить пост
* \[D+\] - Удалить все посты по IP
* \[D++\] - Удалить все посты по IP во всех досках
* \[B\] - Бан
* \[B&D\] - Забанить и удалить
* \[Edit\] - Отредактировать пост.

Внизу страницы располагается форма для отправки жалобы, которая отобразится в админке в разделе Reports queue, а также массовое удаление постов/файлов.

###Стили

Их здесь овердохуя, но по умолчанию отображаются только два: Yotsuba и Yotsuba B.<br />
Для того, чтобы отображались все стили, нужно отредактировать конфиг.<br />
Если добавить все стили, то внизу страницы после ребилда отобразится ничем не прикрытый список, который немного портит внешний вид.<br />
Почему не поместили их в дропбокс - непонятно.

Смена стилей работает только в досках и тредах. Админской части почему-то не касается.

Список всех доступных стилей: `Yotsuba B, Yotsuba, Photon, Futaba, Dark, Dark Roach, Ferus, Futaba+Vichan, Futaba Light, Gentoochan, Jungle, Luna, Miku, Notsuba, Piwnichan, Ricechan, Roach, Stripes, Szalet, Terminal 2, Testorange, Wasabi`.

###Заключение
Движок впринципе не плохой. Очень гибко настраивается.<br />
Но меня почему-то не покидает ощущение того, что он слишком устаревший и его нужно пилить и пилить, хотя работа над ним ведётся и по сей день.<br />
Отдаленно очень напоминает TinyIB. Но эта борда более функциональнее. И если бы выбор стоял между Tinyboard и TinyIB, то безусловно я бы выбрал первое.