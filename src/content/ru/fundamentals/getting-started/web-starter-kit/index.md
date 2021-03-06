project_path: /web/_project.yaml
book_path: /web/fundamentals/_book.yaml
description: Порой самое сложное в новом проекте – начать его. Веб-помощник Web Starter Kit даст вам прочную основу и надежные инструменты, которые помогут вам  в процессе разработки

{# wf_updated_on: 2014-10-20 #}
{# wf_published_on: 2014-07-16 #}

# Начните создавать свой сайт с помощью веб-помощника {: .page-title }

{% include "web/_shared/contributors/mattgaunt.html" %}


Это руководство шаг за шагом объяснит вам процесс создания нового сайта с помощью веб-помощника Web Starter Kit, а также поможет извлечь максимум пользы из его инструментов

<img src="images/wsk-on-pixel-n5.png">



## Этапы разработки 




Имеются 3 команды, которые вы будете использовать регулярно в процессе разработки: gulp serve, gulp и gulp serve:dist. Давайте рассмотрим, как каждая из этих задач помогает при разработке сайта


### Запуск локального сервера

Первая задача выглядит так: `$ gulp serve`.

На первый взгляд, эта задача запускает локальный сервер HTTP, чтобы вы могли видеть свой сайт
в браузере, но в действительности в работе участвует еще несколько инструментов.

#### Прямая перезагрузка

Прямая перезагрузка исключает традиционную необходимость перезагрузки браузера после внесения изменений в редакторе:
переход в браузер, нажатие CTRL-R и ожидание перезагрузки
страницы.

Прямая перезагрузка позволяет вносить изменения в редакторе и сразу видеть
результат в любом браузере, в котором открыт ваш сайт.

<div class="video-wrapper">
  <iframe class="devsite-embedded-youtube-video" data-video-id="JE-ejS8N3YI"
          data-autohide="1" data-showinfo="0" frameborder="0" allowfullscreen>
  </iframe>
</div>

<div class="clearfix"></div>

#### Тестирование в разных устройствах

Синхронизация браузера помогает тестировать сайт в нескольких устройствах. Все прокрутки,
касания или нажатия клавиш на клавиатуре будут отражаться в любом подключенном браузере.

<div class="video-wrapper">
  <iframe class="devsite-embedded-youtube-video" data-video-id="RKKBIs_3svM"
          data-autohide="1" data-showinfo="0" frameborder="0" allowfullscreen>
  </iframe>
</div>

Это работает только в том случае, если ваш сайт запущен командой `gulp serve`. Опробуйте ее: запустите
`gulp serve`, откройте URL в двух соседних окнах браузера и выполните прокрутку
одной из страниц.

<div class="clearfix"></div>

#### Автоматические префиксы

Если вы нацелены на совместимость с несколькими браузерами, вам потребуется использовать префиксы поставщиков, чтобы
можно было использовать возможности каждого из браузеров. Набор Web Starter Kit автоматизирует установку всех
префиксов.

Наш пример CSS (ниже) не содержит префиксов поставщиков:

    .app-bar-container {
      display: flex;

      width: 100%;
      height: 60px;
      position: relative;

      flex-direction: row;

      margin: 0 auto;
    }

В процессе сборки CSS пропускается через функцию автоматической установки префиксов, которая создает следующий
окончательный код:

    .app-bar-container {
      display: -webkit-flex;
      display: -ms-flexbox;
      display: flex;

      width: 100%;
      height: 60px;
      position: relative;

      -webkit-flex-direction: row;
          -ms-flex-direction: row;
              flex-direction: row;

      margin: 0 auto;
    }

#### Проверка кода Javascript

JSHint – этот инструмент, который сканирует ваш код JavaScript c с целью поиска возможных неполадок
в логике кода JavaScript и [реализации наилучших приемов кодирования](http://www.jshint.com/docs/){: .external }.

Этот инструмент запускается при каждом изменении файла JavaScript
независимо от того, выполняется ли сборка проекта или его запуск через gulp server.

#### Компиляция файлов Sass

Пока выполняется команда serve, любые изменения, внесенные в файлы Sass
вашего проекта, компилируются в формат CSS с добавлением префиксов, а затем ваша
страница перезагружается с использованием механизма прямой загрузки.

Для тех, кто не знаком с Sass, поясним, что проект описывается в виде текста на
"расширенном языке CSS". Фактически это язык CSS с некоторыми дополнительными функциями. Например,
в нем добавлена поддержка переменных и функций, которая позволяет создавать файлы CSS
с модульной структурой и возможностью неоднократного использования модулей.

### Сборка рабочей версии сайта

Вы можете скомпилировать рабочую версию вашего сайта с помощью простой
команды `gulp`. Эта команда запускает некоторые задачи, которые уже рассматривались, и дополнительные
задачи, призванные ускорить загрузку вашего сайта и повысить его эффективность.

Основные задачи компиляции рабочей версии состоят в следующем:

#### Создание стилей

Сначала будет выполнена компиляция Sass в вашем проекте. После компиляции Sass
 по всем файлам CSS запускается автоматическое добавление префиксов.

#### Проверка кода Javascript на наличие неполадок

На втором шаге сборки по всему коду JavaScript запускается JSHint.

#### Сборка страниц HTML

На следующем шаге выполняется проверка файлов HTML, выполняется поиск блоков, которые можно объединить, чтобы
уменьшить объем кода JavaScript. После оптимизации кода JavaScript процесс сборки минимизирует
страницу HTML.

Минимизация уменьшает число символов в окончательном файле JavaScript,
удаляя комментарии и ненужные пробелы, а также используя некоторые
другие приемы. При этом размер окончательного файла уменьшается, что ускоряет
загрузку вашего сайта.

Объединение означает вставку содержимого нескольких файлов в один файл. Причина, по которой
мы делаем это, состоит в том, что браузер должен выполнить только один, а не несколько запросов к серверу,
что выполняется быстрее для ваших пользователей.

Блок сборки содержит все необходимое для управления файлами JavaScript, которые мы минимизировали
и объединили. Рассмотрим пример блока сборки:

    <!-- build:js scripts/main.min.js -->
    <script src="scripts/example-1.js"></script>
    <script src="scripts/example-2.js"></script>
    <!-- endbuild -->

Блок сборки — это ни что иное, как комментарий в особом формате.
Все ваши файлы javascript из разных сборочных блоков будут слиты
(объединены) и минимизированы в одном файле с именем main.min.js, и
в окончательной сборке эти скрипты будут заменены тегом скрипта:

    <script src="scripts/main.min.js"></script>

#### Оптимизация изображений

Для изображений в формате JPEG и PNG метаданные в изображениях удалены, поскольку они не требуются для
обработки изображения. Метаданные содержат такую информацию, как тип камеры, использованной для
съемки фотографии.

Для изображений в формате SVG выполняется удаление всех ненужных атрибутов, а также имеющихся
пробелов и комментариев.

#### Копирование шрифтов

Эта простая задача копирует наши шрифты из приложения в каталог окончательной сборки.

#### Копирование всех файлов из корневого каталога

Если в процессе сборки в корневом каталоге проекта обнаруживаются файлы, они также копируются
в окончательную сборку.

### Тестирование рабочей версии

Перед публикацией необходимо проверить, что все работает
так, как вы ожидаете. Команда `gulp serve:dist` выполняет сборку рабочей версии вашего сайта,
запускает сервер и открывает браузер. Она **не запускает функции прямой перезагрузки или
синхронизации браузера**, но это надежный способ протестировать ваш сайт перед его развертыванием.




## Установка набора Web Starter Kit 




Для работы Web Starter Kit требуются NodeJS, NPM и Sass. Как только эти компоненты будут установлены на компьютере, можно сразу приступать к использованию Web Starter Kit в своих проектах


### Установка необходимых компонентов

Прежде чем приступить к созданию сайтов с помощью
Web Starter Kit, установите на компьютере следующие наборы инструментов: NodeJS, NPM и Sass.

#### NodeJS и NPM

Для работы инструментов Web Starter Kit необходимы компоненты Node и NPM. Node необходим для Gulp, средства
запуска задач. Компонент NPM предназначен для загрузки модулей, необходимых для выполнения определенных задач
в Gulp.

Если вы не знаете, установлены ли на компьютере эти компоненты,
перейдите в командную строку и выполните команду `node -v`. В случае получения ответа от Node убедитесь в том, что установлена актуальная версия компонента. Сведения о версиях
 размещены на сайте NodeJS.org.

Если ответа не последовало или на компьютере установлена устаревшая версия Node, перейдите на сайт NodeJS.org 
и нажмите на большую зеленую кнопку Install (Установить). NPM устанавливается автоматически вместе с
компонентом NodeJS.

### Установка набора Web Starter Kit и создание проекта

Сначала перейдите по ссылке [https://developers.google.com/web/starter-kit/](/web/starter-kit/) и загрузите архив,
после чего распакуйте его на компьютере. Папка с распакованными файлами будет служить основой для вашего проекта, поэтому присвойте ей соответствующее имя и поместите ее в подходящее место на компьютере. Далее в этом руководстве такая папка будет называться `my-project`.

Затем установите компоненты, необходимые для работы Web Starter Kit. Откройте
командную строку, перейдите в папку проекта и запустите следующие
скрипты установки NPM.

    cd my-project
    npm install
    npm install gulp -g

Вот и все! Теперь на вашем компьютере имеется все необходимое для работы с инструментами Gulp в Web Starter
Kit.

Note: -"При появлении сообщений об ошибках доступа, таких как <code>EPERM</code> или <code>EACCESS</code>, не используйте в качестве решения проблемы команду <code>sudo</code>. Более подходящее решение показано на <a href='https://github.com/sindresorhus/guides/blob/master/npm-global-without-sudo.md'>этой странице</a>."

В следующем разделе данного руководства рассматривается порядок использования Gulp. Чтобы ознакомиться с интерфейсом
, попробуйте запустить локальный сервер с помощью команды `gulp serve`.

<img src="images/wsk-on-pixel-n5.png">


