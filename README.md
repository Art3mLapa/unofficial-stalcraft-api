# LAUNCHER STALCRAFT API
Документация внутреннего HTTP/HTTPS API лаунчера игры.

## POST http://launcher.stalcraft.net/metrics
Ссылка, отвечающая за отправку метрики игрока для аналитики.
Метрика содержит:
- Сетевые данные (Объём трафика, длительность загрузок)
- Ошибки (Повреждённые файлы)
- Поведение пользователя в игре или на сайтах *exbo.net
- Профилирование (время выполнения операций)
- IP и геолокация 

## GET http://launcher.stalcraft.net/listServers
Ссылка, отвечающая за получение информации об игровом сервере и игре STALCRAFT, такие как онлайн на сервере, HTTP сиды, размер игры в байтах и т.д.

Пример короткого ответа (full=false)
```json
{
  "success": true,
  "data": [
    {
      "id": "stalcraft", // ID сервера
      "onlineCurrent": 19862, // Онлайн на сервере в данный момент
      "onlineMax": 50000, // Максимальный онлайн сервера
      "runCommand": "\"<java>/java/bin/stalcraft.exe\" -classpath \"classes.jar;libs.jar;modassets\" -XX:-PrintCommandLineFlags -XX:ErrorFile=crash-reports/hs_err_pid%p.log -Xmx<mem>m \"-Djava.library.path=<java>/java/bin\" -Dfile.encoding=UTF-8 -Dshow_globally_enabled=false -Dread_derived=true -DCustomNpcsSoundCache=true -Dload_dumped_event_classes=true -DusePrestitchedAtlas=true -Ddisable_item_atlas=true -Ddisable_mod_parsing=true -Duse_system_class_loader=true -XX:+UseG1GC -XX:MaxGCPauseMillis=3 -Dmanagement-metrics=true exbo.stalcraft.client.Main --username=<usr> --session <sess> --gameDir \"<cd>\" --assetsDir \"<cd>/assets\" --dlogin \"<dlogin>\"", // Аргументы для запуска игры (stalcraft.exe)
      "version": "3f39f5281ec4c5c69d768769b6a1fe497b62956" // Версия игры
    }
  ],
  "preventRelog": true
}
```

Пример полного ответа (full=true):
```json
{
  "success": true,
  "data": "
  [
    {
      "background": "https://launcher.stalcraft.net/files?name=stalcraft.jpg", // Ссылка для подкачки фонового изображения в лаунчере
      "caption": "STALCRAFT: X", // Титульное название сервера
      "desc": [ // Описание
        "Stalcraft - это массовый многопользовательский онлайн-шутер от первого лица,",
        "погружающий Вас в альтернативную историю Чернобыльской зоны отчуждения.",
        "",
        "Сможете ли Вы выжить в этом мире?",
        "Опасные мутанты, уникальные артефакты, непроходимые катакомбы, кишащие ",
        "аномалиями и, конечно же, другие авантюристы, желающие разгадать загадки Зоны.",
        "",
        "Правда, даже самые сильные игроки не смогут добиться успеха в одиночку. ",
        "Объединяйтесь в Группировки, участвуйте в Захватах, бросайте вызов соперникам,",
        "планируйте вылазки и исследования.",
        "",
        "Зона ждёт.",
        "Всё в твоих руках, Сталкер!"
      ],
      "exclusions": [ // Исключения
        "activitylog",
        "autosaves",
        "crash-reports",
        "config",
        "saves",
        "screenshots",
        "logs",
        "stats",
        "customnpcs",
        "map_cache",
        "options.txt",
        "optionsof.txt",
        "optionsof_new1.txt",
        "gloomyoptions.txt",
        "gloomyoptions_new.txt",
        "smart_moving_options.txt",
        "alsoftrc.txt",
        "radio"
      ],
      "httpSeeds": [ // HTTP сиды для подкачки ассетов во время игры
        "http://exbo.b-cdn.net/stalcraft/",
        "http://m-cdn.exbo.net/stalcraft/"
      ],
      "icon": "https://launcher.stalcraft.net/files?name=stalcraft_icon.png", // Ссылка для подкачки иконки сервера
      "id": "stalcraft", // ID сервера
      "info": null, // info сервера
      "onlineCurrent": 20565, // Онлайн на сервере на данный момент
      "onlineMax": 50000, // Максимальный онлайн сервера
      "pingTarget": "85.119.149.112:30037", // IP адрес сервера
      "runCommand": "\"<java>/java/bin/stalcraft.exe\" -classpath \"classes.jar;libs.jar;modassets\" -XX:-PrintCommandLineFlags -XX:ErrorFile=crash-reports/hs_err_pid%p.log -Xmx<mem>m \"-Djava.library.path=<java>/java/bin\" -Dfile.encoding=UTF-8 -Dshow_globally_enabled=false -Dread_derived=true -DCustomNpcsSoundCache=true -Dload_dumped_event_classes=true -DusePrestitchedAtlas=true -Ddisable_item_atlas=true -Ddisable_mod_parsing=true -Duse_system_class_loader=true -XX:+UseG1GC -XX:MaxGCPauseMillis=3 -Dmanagement-metrics=true exbo.stalcraft.client.Main --username=<usr> --session <sess> --gameDir \"<cd>\" --assetsDir \"<cd>/assets\" --dlogin \"<dlogin>\"", // Аргументы для запуска игры (stalcraft.exe)
      "totalSize": 36295702714, // Размер игры (в байтах)
      "version": "3f39f5281ec4c5c69d768769b6a1fe497b62956" // Версия игры
    }
  ]",
  "preventRelog": true
}
```

Имеет параметры:
- `full=false` - Отвечает за количество информации в ответе. если равен true, ответ будет содержать более детальную информацию об серверах, файлах и ссылках
- `token=11111111-2222-3333-4444-555555555555` - Токен сессии пользователя EXBO (не токен из реестра!)
- `login=User` - Логин пользователя EXBO

Пример ссылки с правильными параметрами:
- ```http://launcher.stalcraft.net/listServers?full=false&token=11111111-2222-3333-4444-555555555555&login=User```

## http://tracker1.stalcraft.net  |   http://tracker2.stalcraft.net
Torrent трекеры, используются для скачивания и раздачи файлов игры через файл `stalcraft.torrent.bin`

Имеет параметры:
- `info_hash=12345678900987654321` - Хеш скачиваемого файла
- `peer_id=-LT12J0-abc-de123456` - ID пира скачивания/раздачи
- `port=52525` - Порт
- `uploaded=0` `downloaded=0` `left=292552704` `corrupt=0` - Информация об скачивании/раздаче файлов (в байтах)
- `key=C87A7012` - Ключ для доступа к трекеру
- `event=paused` - Состояние скачивания/раздачи
- `numwant=200` `compact=1` `no_peer_id=1` `supportcrypto=1` `redundant=0` - Прочая информация, необходимая для трекера

Пример ссылки с правильными параметрами:
```http://tracker1.stalcraft.net:6767/announce?info_hash=%af%1e%3d%ad%25j%b7%0d%bcrH0Z%a8%d3%a68%3c%27%7b&peer_id=-LT12J0-nMr-gyluoL.3&port=52580&uploaded=0&downloaded=0&left=292552704&corrupt=0&key=C87A7012&event=paused&numwant=200&compact=1&no_peer_id=1&supportcrypto=1&redundant=0```
