<div align="center">
  <p>
    <a href="https://github.com/OpenXRay">
      <img src="misc/media/OpenXRayCover.png" alt="Open for everyone" />
    </a>
  </p>
</div>

<h1 align="center">
  OpenXRay
</h1>

* [Build instructions for Linux and other platforms](https://github.com/OpenXRay/xray-16/wiki/%5BEN%5D-How-to-build-and-setup-on-Linux-and-MacOS).

**Общий пример сборки OpenXRay.**

Для сборки OpenXRay в системе должны быть установлены следующие пакеты

`git gcc cmake libglvnd libjpeg6-turbo ncurses glew sdl2 openal crypto++ freeimage libogg libtheora libvorbis lzo lzop libjpeg-turbo`

NOTE: На текущий момент поддерживаются только компиляторы GCC8, GCC9, GCC10

Для сборки и установки OpenXRay необходимо выполнить следующие команды в терминале

`mkdir -p ~/xray-16/bin
cd ~/xray-16/bin
cmake .. -DCMAKE_INSTALL_PREFIX=/usr
make
sudo make install`


NOTE: Для задействования всех ядер процессора во время компиляции их количество можно передать make через ключ -j, например make -j4 будет задействовано четыре ядра процессора.

Дополнительные параметры которые можно указать при настройке передав их cmake:

-DCMAKE_BUILD_TYPE=Release

Release - Релиз (значение по умолчанию, рекомендуется для игроков)  
Debug - Отладка
Mixed - Смешанная
RelWithDebInfo - Релиз с отладочными символами

Каталог установки -DCMAKE_INSTALL_PREFIX=/usr

NOTE: Обязательный параметр рекомендуемое значение для подавляющего числа дистрибутивов.

Каталог расположения библиотек. -DCMAKE_INSTALL_LIBDIR=lib

  lib Большинство дистрибутивов (Значение по умолчанию)
  lib64 Дистрибутивы с разделённой структурой каталогов (Fedora, CentOS, Slakware...)

NOTE: Определяется автоматически, как правило INSTALL_PREFIX/lib

Каталог расположения исполняемого файла -DCMAKE_INSTALL_BINDIR=bin

  По умолчанию большинство дистрибутивов bin
  Для Ubuntu рекомендуется games
  Для Gentoo рекомендуется games/bin

Выбор менеджера памяти -DMEMORY_ALLOCATOR=mimalloc
    
mimalloc (Значение по умолчанию)
standard

NOTE: За более подробной информацией обратитесь к документации вашего дистрибутива.

*Сборка пакета*

NOTE: Выше был описан метод ручной установки но он имеет ряд недостатков главный из них это то что OpenXRay устанавливается в систему в обход пакетного менеджера что может привести к не приятным последствиям в будущем во избежании этого рекомендуется собрать пакет для вашего дистрибутива.

*Сборка пакета для ArchLinux/Manjaro*

Для ArchLinux и основанных на нём дистрибутивах существе готовый PKGBULD для сборки и установки пакета выполните:

`cd ~/xray-16/ArchLinux/
makepkg`

В итоге будет собран pkg.tar.xz пакет который можно установить при помощи `sudo pacman -U *.pkg.tar.xz`

*Сборка пакета для Debian/Ubuntu*

`
sudo apt install git cmake make libglew-dev libopenal-dev libcrypto++-dev libogg-dev libtheora-dev libvorbis-dev libsdl2-dev liblzo2-dev libjpeg-dev libncurses5-dev gcc g++ dpkg-dev
mkdir -p ~/xray-16/bin
cd ~/xray-16/bin
cmake .. -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_INSTALL_LIBDIR=lib -DCMAKE_INSTALL_BINDIR=/usr/games
make
make package
`

NOTE: Для задействования всех ядер процессора во время компиляции их количество можно передать make через ключ -j, например make -j4 будет задействовано четыре ядра процессора.

В итоге будет собран deb пакет который можно установить при помощи `sudo dpkg -i *.deb`

*Сборка пакета для Fedora/CentOS*

`
sudo dnf install git cmake make gcc gcc-c++ glew-devel openal-devel cryptopp-devel libogg-devel libtheora-devel libvorbis-devel SDL2-devel lzo-devel libjpeg-turbo-devel
mkdir -p ~/xray-16/bin
cd ~/xray-16/bin
cmake .. -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_INSTALL_LIBDIR=lib64
make
make package
`

NOTE: Для задействования всех ядер процессора во время компиляции их количество можно передать make через ключ -j, например make -j4 будет задействовано четыре ядра процессора.

В итоге будет собран rpm пакет который можно установить при помощи `sudo rpm -i *.rpm`

4) Портативная (переносная) установка

Если вы не имеете возможности создать пакет для своей системы и(или) не хотите устанавливать движок в свою систему то можете воспользоватся данным способом.
`
cmake ..
make
`
    В домашней директории создайте каталог для игры например S.T.A.L.K.E.R.
  Из каталога xray-16/bin/x64/Release/ скопируйте следующие файлы:

xr_3da xrAICore.so xrAPI.so xrCDB.so xrCore.so xrEngine.so xrGame.so xrLuabind.so xrLuajit.so xrNetServer.so xrParticles.so xrRender_GL.so xrScriptEngine.so xrSound.so xrUICore.so

в каталог ~/S.T.A.L.K.E.R./bin/ Все остальные файлы сим линки не являются необходимыми и и х можно не копировать.

  Скопируйте каталог gamedata и файл fsgame.ltx из каталога xray-16/res в ~/S.T.A.L.K.E.R./
  В ~/S.T.A.L.K.E.R.CoP/ поместите игровые ресурсы levels, localization, mp, patches, resources. Должно получиться примерно так: S.T.A.L.K.E.R.CoP bin Для запуска откройте терминал перейдите в каталог ~/S.T.A.L.K.E.R. и выполните команду

`./bin/xr_3da -fsltx /home/Koshamur/S.T.A.L.K.E.R./fsgame.ltx`

Аналогично можно поступить с ресурсами S.T.A.L.K.E.R.: Чистое Небо но для его запуска следует добавить ключ -cs

`./bin/xr_3da -cs -fsltx /home/Koshamur/S.T.A.L.K.E.R./fsgame.ltx`

NOTE: На данный момент путь к fsgame.ltx должен быть абсолютным начиная от корня системы

NOTE: Для задействования всех ядер процессора во время компиляции их количество можно передать make через ключ -j, например make -j4 будет задействовано четыре ядра процессора.
5) Игровые ресурсы

Для запуска игры вам потребуются оригинальные ресурсы лицензионной копии S.T.A.L.K.E.R. Зов Припяти. и(или) S.T.A.L.K.E.R. - Чистое Небо. Поместите каталоги levels, localization, mp, patches, resources из дистрибутива S.T.A.L.K.E.R. Зов Припяти в ~/.local/share/GSC Game World/S.T.A.L.K.E.R. - Call of Pripyat/ и(или) в ~/.local/share/GSC Game World/S.T.A.L.K.E.R. - Clear Sky из дистрибутива S.T.A.L.K.E.R. - Чистое Небо.

!!!Внимание каталог ~/.../GSC Game World/S.T.A.L.K.E.R. -... необходимо создать самостоятельно

`
mkdir -p ~/.local/share/GSC\ Game\ World/S.T.A.L.K.E.R.\ -\ Call\ of\ Pripyat
mkdir -p ~/.local/share/GSC\ Game\ World/S.T.A.L.K.E.R.\ -\ Clear\ Sky
`

Если у вас есть цифровая копия игры в Steam то ресурсы можно скопировать из ~/.local/share/Steam/steamapps/common/Stalker... (Каталог установки игр Steam в Linux по умолчанию).

Если у вас есть физическая копия игры или копия из GoG то её можно распаковать воспользовавшись консольной утилитой innoextract скорее всего она имеется в репозитории вашего дистрибутива и её можно установить:

ArchLinux/Manjaro `sudo pacman -S innoextract`

Debian/Ubuntu `sudo apt install innoextract`

Fedora `sudo dnf install innoextract`

Для распаковки дистрибутива выполните:

  Скопируйте содержимое компакт диска в домашний каталог например ~/CoP
Откройте терминал перейдите в каталог с дистрибутивом игры cd ~/CoP и выполните innoextract setup.exe -L

ключ -L переводит название всех файлов и каталогов в нижний регистр

ключ -d указывает каталог куда будут помещены распакованные файлы например -d CoP_unpack

ключ --gog необходим для распаковки инсталятора gog

  Дождитесь окончания распаковки, по завершению в каталоге ~/CoP появится каталог app или game из которого можно скопировать levels, localization, mp, patches, resources

Распакованный СD дистрибутив CD

Распакованный GOG дистрибутив GOG

Внимание!!! имена каталогов levels, localization, mp, patches, resources и файлы в них должны находиться в нижнем регистре то есть маленькими буквами актуально для копии игры из GOG.

   Если по каким либо причинам Вы не хотите занимать дополнительное место в домашнем каталоге но уже имеете установленную игру в Windows или Steam то можете создать символические ссылки на каталоги с ресурсами levels, localization, mp, patches, resources Ниже приведён пример создание символических ссылок S.T.A.L.K.E.R. Зов Припяти установленного в Steam:

`
mkdir -p ~/.local/share/GSC Game World/S.T.A.L.K.E.R.\ -\ Call\ of\ Pripyat
ln -s ~/.local/share/Steam/steamapps/common/Stalker\ Call\ of\ Pripyat/levels ~/.local/share/GSC\ Game\ World/S.T.A.L.K.E.R.\ - Call\ of\ Pripyat/levels
ln -s ~/.local/share/Steam/steamapps/common/Stalker\ Call\ of\ Pripyat/localization ~/.local/share/GSC\ Game\ World/S.T.A.L.K.E.R.\ - Call\ of\ Pripyat/localization
ln -s ~/.local/share/Steam/steamapps/common/Stalker\ Call\ of\ Pripyat/mp ~/.local/share/GSC\ Game\ World/S.T.A.L.K.E.R.\ -\ Call\ of\ Pripyat/mp
ln -s ~/.local/share/Steam/steamapps/common/Stalker\ Call\ of\ Pripyat/patches ~/.local/share/GSC\ Game\ World/S.T.A.L.K.E.R.\ - Call\ of\ Pripyat/patches
ln -s ~/.local/share/Steam/steamapps/common/Stalker\ Call\ of\ Pripyat/resources ~/.local/share/GSC\ Game\ World/S.T.A.L.K.E.R.\ - Call\ of\ Pripyat/resources
`

  Теперь игру можно запустить выбрав пункт S.T.A.L.K.E.R.: Call of Pripyat (OpenXRay) или S.T.A.L.K.E.R.: - Clear Sky (OpenXRay) из меню приложений или выполнив в терминале xr_3da для запуска S.T.A.L.K.E.R. Зов Припяти или xr_3da -cs для запуска S.T.A.L.K.E.R. - Чистое Небо

Внимание!!! работы по поддержке S.T.A.L.K.E.R. - Чистое Небо не завершены. Возможны баги и ошибки.
Возможные проблемы

  *Установленный движок не запускается.*

Откройте терминал и введите команду xr_3da если будет выдано сообщение вида:

bash: xr_3da: команда не найдена

возможно не правильно настроено расположение исполняемого файла на этапе настройки проекта, как правило значение по умолчанию переменной DCMAKE_INSTALL_BINDIR должно быть /usr/bin в ряде дистрибутивах она может отличатся. Если вы увидите сообщение вида:

./xr_3da: error while loading shared libraries: xrEngine.so: cannot open shared object file: No such file or directory

Возможно что на этапе настройки проекта неправильно определились одна из переменных (или обе сразу)

DCMAKE_INSTALL_PREFIX должна быть равна /usr, а DCMAKE_INSTALL_LIBDIR – lib или lib64.

Если если происходит инициализация после которой движок завершается аварийно с сообщением

FATAL ERROR
 
[error] Expression    : setupSelectedRenderer
[error] Function      : InitializeRenderers
[error] File          : /home/chip/OpenXray/xray-16/src/xrEngine/EngineAPI.cpp
[error] Line          : 128
[error] Description   : Can't setup renderer

В случае портативной установки скорее всего вы не скопировали шейдеры из каталога xray-16/res/ скопируйте каталог xray-16/res/gamedata в каталог с ресурсами игры
Известные баги и ошибки.

  При выходе из игры процесс может зависнуть (по состоянию на май 2020 данная проблема наблюдается при сборке с использованием gcc9 )
    Сохранения и логи не поддерживают UTF-8
    На видеокартах AMD замечены баги с включенным SSAO, поэтому рекомендуется его полностью отключить.
    Не создаются превью для сохранения
    При первом запуске могут сбиться настройки разрешения экрана в вашем DE

Вылет при приближении к персонажу в начале игры

Подобный вылет в большинстве случаев сопровождается подобным сообщением в логе игры

[error] Expression  : !m_error_code
[error] Function    : ~raii_guard
[error] File        : /.../.../xray-16/src/xrSCRIPTENGINE/script_engine.cpp
[error] Line        : 569
[error] Description : ...R. -Call of Pripyat\gamedata\scripts\sound_theme.script:225: bad argument #1 to 'gsub' (string expected, got nil)

Данная проблема выявлена только на копиях игры из GOG. Для её решения Вам необходимо:

  Перейти в каталог с ресурсами по умолчанию это ~/.local/share/GSC Game World/S.T.A.L.K.E.R. - ...
    Убедится в том что имя каталога каталог localization находится в нижнем регистре (То есть маленькими буквами). Правильное имя каталога localization Не правильное имя каталога Localization
    В каталоге localization должны находится архивы с желаемой локализацией игры все остальные файлы и каталоги должны быть удалены. Ниже приведён список локализации для всех поддерживаемых языков.

    English base_sounds.db xefis_movies.db xenglish.db
    French base_sounds.db xefis_movies.db xfrench.db
    German base_sounds.db xger_movies.db xgerman.db
    Italian base_sounds.db xefis_movies.db xitalian.db
    Polish base_sounds.db xpolish_texts.db xrus_sounds.db xxpolish_sounds.db
    Russian base_sounds.db xefis_movies.db xrussian.db
    Spanish base_sounds.db xefis_movies.db xspanish.db Выше перечисленные файлы находятся в подкаталогах localization/En localization/Fr localization/Ge ...

Также в файле настроек ~/.local/share/GSC Game World/S.T.A.L.K.E.R. - .../user.ltx следует удалить параметр g_language или задать значение выбранной локализации примеры ниже:

g_language eng
g_language fra
g_language ger
g_language ita
g_language pol
g_language rus
g_language spa

Как переключить язык игры

Данная проблема выявлена только на копиях игры из GOG. Для её решения перейдите в каталог ~/.local/share/GSC Game World/S.T.A.L.K.E.R. - ... В каталоге localization должны находится архивы с желаемой локализацией игры все остальные файлы и каталоги должны быть удалены. Ниже приведён список локализации для всех поддерживаемых языков.

    English base_sounds.db xefis_movies.db xenglish.db
    French base_sounds.db xefis_movies.db xfrench.db
    German base_sounds.db xger_movies.db xgerman.db
    Italian base_sounds.db xefis_movies.db xitalian.db
    Polish base_sounds.db xpolish_texts.db xrus_sounds.db xxpolish_sounds.db
    Russian base_sounds.db xefis_movies.db xrussian.db
    Spanish base_sounds.db xefis_movies.db xspanish.db Выше перечисленные файлы находятся в подкаталогах localization/En localization/Fr localization/Ge ...

Также в файле настроек ~/.local/share/GSC Game World/S.T.A.L.K.E.R. - .../user.ltx следует удалить параметр g_language или задать значение выбранной локализации примеры ниже:

g_language eng
g_language fra
g_language ger
g_language ita
g_language pol
g_language rus
g_language spa

У меня низкий FPS

Ограничения некоторых расширенных настроек графики существенно увеличены, по сравнению с оригинальной игрой. Следует быть осторожным со следующими настройками графики:

  Детализация объектов. Данная опция оказывает значительное влияние на производительность.
    Дальность прорисовки травы. Данной опции просто не было в оригинальном движке и её значение было «зашито» прямо в движке.
    Плотность травы. Лимит данной опции был увеличен в два-три раза.
    Качество теневых карт. Этой опции также не было в оригинальном движке, значения были «зашиты» и единственным методом смены были ключи запуска, однако даже через ключ запуска максимальным значением было 4096, в то время как у нас максимум – 16384.

Не могу собрать ошибка версии GCC

  Некоторые пользователи сталкиваются с проблемой не совместимости версии GCC поскольку в ряде дистрибутивов по умолчанию предоставляется GCC версии 7, для сборки рекомендуется использовать GCC версии 8 и выше для решения этой проблем вы можете установить GCC 8 штатными средствами вашего дистрибутива и на этапе конфигурации выполнить cmake -DCMAKE_C_COMPILER=gcc-8 -DCMAKE_CXX_COMPILER=g++-8 -DCMAKE_BUILD_TYPE=Debug -w ..
    Не рекомендуется исправить в файле CMakeLists.txt но если в репозитории вашего дистрибутива нет GCC 8 то измените строку CMAKE_CXX_COMPILER_VERSION VERSION_LESS 8.0.0 на свой GCC к примеру CMAKE_CXX_COMPILER_VERSION VERSION_LESS 7.4.0. Однако возможны проблемы.

Звук плохо позиционируется

Нужно принудительно включить HRTF в OpenAL: echo "hrtf = true" >> ~/.alsoftrc

Если это не заработало, проверьте, что в системе присутствуют файлы default-44100.mhr и default-48000.mhr (В Ubuntu это пакет libopenal-data)

Если и после этого не заработало, запускайте игру с переменными ALSOFT_LOGLEVEL=3 ALSOFT_LOGFILE=/tmp/openallog.txt ./xr_3da и анализируйте лог на предмет HRTF.

Не загружаются сохранения S.T.A.L.K.E.R.: Чистое Небо из оригинальной игры

Обратной совместимости с форматом сохранения S.T.A.L.K.E.R.: Чистое Небо нет.

Не запускается S.T.A.L.K.E.R.: Тень Чернобыля

Я установил движок и скопировал игровые ресурсы S.T.A.L.K.E.R.: Тень Чернобыля в ~/.local/share/GSC Game World/S.T.A.L.K.E.R. - Shadow of Chernobyl/ но он у меня не запускается.

На данный момент работы по поддержке S.T.A.L.K.E.R.: Тень Чернобыля только начаты.

Игра запускается на английском языке как переключить язык на русский?

Данная проблема наблюдается для копии игры из GOG для её решения зайдите в .../S.T.A.L.K.E.R.../localization в ней должен находится только файлы base_sounds.db, xefis_movies.db, xrussian.db всё остальное нужно удалить

Игра вылетает с установленным модом

К сожалению, совместимость с некоторыми модификациями неполная, это связанно со следующим:

  Многие разработчики при разработке модов вносят свои изменения в движок которых нет в OpenXRay такой мод полностью не совместим. Даже если разработчик мода использовал OpenXRay, не исключено что он внёс свои изменения в свою ветку.
    Разработчики модификаций часто используют разный регистр (Заглавные и строчные буквы) в путях и названиях файлов игровых ресурсов. Файловая система Linux устроена иначе: если в Windows файлы с именем A.dds и a.dds считаются одним и тем же файлом, то в Linux это разные файлы и в таком случае можно получить вылет связанный с отсутствием файла.

Для того чтобы модификация могла запустится нужно выполнить несколько условий:

1. Модификация не должна затрагивать сам движок
2. Должны быть правильно прописаны пути и имена файлов в скриптах

