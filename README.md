# Автоматическое переключение сети
### Лабораторная работа #2
[[презентация]](https://www.dropbox.com/s/z2s29h62jtcwre7/Task%202.pptx?dl=0) [[репозиторий]](https://github.com/Andrew414/adaptertask)

## Условие
Необходимо написать приложение, которое может запускаться автоматически при старте системы. Это может быть служба Windows/демон Unix или обычное приложение, запускаемое автоматически средствами ОС (планировщиком задач, списком автозагрузки и др).

У приложения должен быть предоставить установщик, который может устанавливать (настраивать автоматический запуск) и удалять (отменять автоматический запуск) приложение. Установщиком может быть отдельный файл, скрипт или просто опция командной строки.

Приложение должно следить за состоянием сетевых адаптеров. В том случае, если есть включенный проводной адаптер, оно должна отключать все присутствующие беспроводные адаптеры.

Как только проводной адаптер становится неактивным, или если программа удаляется, все выключенные этой программой адаптеры должны быть включены. Поскольку в современных ноутбуках может не быть LAN-порта, в качестве проводного можно использовать виртуальный адаптер (VirtualBox, VMWare) или любой другой адаптер.

### Дополнительная информация

###### Службы Windows и демоны Unix
Службы ОС Windows (англ. Windows Service, сервисы) — приложения, автоматически (если настроено) запускаемые системой при запуске Windows и выполняющиеся вне зависимости от статуса пользователя. 

Демон — компьютерная программа в системах UNIX, запускаемая самой системой и работающая в фоновом режиме без прямого взаимодействия с пользователем. Демоны обычно запускаются во время загрузки системы.

###### Запуск служб Windows
Службы запускаются в адресном пространстве приложения-контейнера и взаимодействуют с системой только через callback-функции. Функция `main` служит только для запуска обработчика сервиса. Для запуска диспетчера сервисов используется функция `StartServiceCtrlDispatcher`, которая принимает массив неопределенной длины, каждый элемент которого содержит имя сервиса и адрес соответствующей точки входа.

Точка входа в сервис должна:
* Запускать обработчик управляющих команд (с помощью функции `RegisterServiceCtrlHandler`)
* Устанавливать и изменять состояние сервиса
* Выполнять работу сервиса в соответствии с состоянием
* Освобождать ресурсы при переходе в состояние STOPPED

Возможные управляющие команды:
* SERVICE_CONTROL_STOP — остановить сервис; 
* SERVICE_CONTROL_PAUSE — приостановить сервис; 
* SERVICE_CONTROL_CONTINUE — возобновить сервис; 
* SERVICE_CONTROL_INTERROGATE — обновить состояние сервиса; 
* SERVICE_CONTROL_SHUTDOWN — закончить работу сервиса.
* Коды, определенные пользователем – 128-255


###### Дополнительные ссылки
Функции для работы с сетью:
* Функции для работы с сетью в Windows https://msdn.microsoft.com/en-us/library/windows/desktop/aa366071(v=vs.85).aspx 
* Функции для работы с сетью в Unix http://man7.org/linux/man-pages/man3/getifaddrs.3.html

### Дополнительные требования
Программа должна быть написана с использованием общепринятого [**стандарта**](https://ru.wikipedia.org/wiki/Стандарт_оформления_кода). Если для выбранного языка есть один такой стандарт, используйте его, иначе выберите любой для своего языка программирования и укажите в комментариях к Pull Request, какой именно стандарт выбран.

### Дополнительные задания
Три задачи:
* Реализовать программу как службу Windows/демон Unix 
  * Запуск программы не должен производиться с помощью автозагрузки или планировщиков
* Реализовать установщик
  * Установщик должен регистрировать приложение для автоматического запуска
  * Установка программы должна выполняться запуском одной команды/скрипта
* Реализовать установщик в _общепринятом_ виде 
  * В Windows - как набор с диалогами (msi или аналогичный метод) 
  * В Unix - как пакет (make install либо unix-пакеты)

### Репозиторий
[Репозиторий](https://github.com/Andrew414/adaptertask) содержит главную страницу [`README.md`](https://github.com/Andrew414/adaptertask/blob/master/README.md) и одиннадцать персональных каталогов. Необходимо сделать копию (fork) репозитория и вносить все изменения только в свой персональный каталог. Все эти каталоги содержат пустой файл `.gitignore`, куда нужно вписать все временные файлы из лабораторной работы. Остальные файлы должны быть файлами кода (в т.ч. проекта).

### Сдача лабораторной работы
Можно выбрать любой язык программирования, IDE и фреймворки/библиотеки. Если для работы нужны какие-то нестандартные конфигурации или ПО, предоставьте инструкцию по настройке среды.

Сдача через **Pull Request** из вашего клонированного репозитория. Pull Request должен содержать код, файлы проекта и информационные файлы. Результаты сборок и временные файлы должны быть исключены из коммитов.

### Оценка
Максимум за лабораторную работу - **10 баллов**.
- **4 балла** за главную задачу
- **3 балла**, если работа сделана вовремя
- **1 балл** за реализацию лабораторной как *сервиса*/*демона*
- **1 балл** за реализацию *установщика*
- **1 балл** за реализацию установщика *в общепринятом виде*

### Сроки
На выполнение лабораторной дается 4 недели (1 марта - 29 марта). Лабораторная работа считается принятой, когда Pull Request переходит в состояние "approved". Дни, в течение которых лабораторная была на проверке, не учитываются.
![ ](https://i.snag.gy/lPOzf7.jpg)

Например, если вы сдаете лабораторную через две недели после выдачи (15 марта), но комментарии даны только через неделю (22 марта), у вас все еще будет две недели на устранение недочетов, все дни после коммита до получения ревью не считаются.

### Желаю удачи!
