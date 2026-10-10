# PixelLordsGame

Готовые веб-сборки [PixelLords](https://github.com/vetcat/PixelLords) для тестирования
на iPhone, Android и компьютерах.

Страница игры: **https://vetcat.github.io/PixelLordsGame/**.
На начальной странице пока размещено сообщение об отсутствии игровой сборки.

## Публикация

GitHub Pages публикует корень ветки `main` после push. Файл `.nojekyll`
включает раздачу готовых файлов без обработки Jekyll.

1. Собрать платформу **Web** в Unity из проекта PixelLords. Каталог результата
   держать вне исходного Unity-проекта, например в `~/Desktop/PixelLordsWeb/`.
2. Заменить в этом репозитории экспортированный `index.html` и каталоги `Build/`,
   `TemplateData/`, а также `StreamingAssets/`, если он есть в результате сборки.
   Сохранить `.git/`, `.gitignore`, `.nojekyll` и этот README. Каталоги предыдущей
   сборки заменять целиком, чтобы старые файлы не накапливались.
3. Перед коммитом проверить `git status --short` и список файлов: здесь должны
   находиться файлы веб-сборки и документация публикации.
4. Опубликовать обновление:

   ```sh
   git add -A
   git commit -m "Publish PixelLords web build"
   git push origin main
   ```

5. Дождаться успешного выполнения `pages build and deployment` на вкладке
   **Actions**, открыть страницу игры и проверить загрузку новой версии.

## Совместный тест с Android

Веб-сборку и APK создавать из одной версии симуляции. Клиенты должны использовать
одинаковые Photon AppId, сетевой AppVersion, регион и комнату; UserId у каждого
клиента должен быть свой. Веб-клиент подключается к Photon через защищённые
WebSockets. GitHub Pages раздаёт файлы игры, а игровой обмен проходит через Photon.

Открывать ссылку на iPhone непосредственно в Safari и держать игру на переднем
плане. Сворачивание, блокировку экрана и повторный вход проверять отдельно.

## Настройки Web

Версию Unity и зависимостей брать из README исходного проекта.
Для мобильного Safari использовать WebAssembly32. WebGPU можно поставить
первым в списке Graphics APIs, сохранив WebGL 2 для автоматического переключения
на устройствах без WebGPU. WebAssembly 2023 требует Safari 16.4 или новее.

Если в Unity включено предварительное сжатие gzip/Brotli, проверить заголовки
ответов опубликованных файлов. Когда сервер не отдаёт соответствующий
`Content-Encoding`, использовать Decompression Fallback. Проверка gzip для
AsteroidsBuild относится к файлам без предварительного сжатия Unity и сама по
себе не подтверждает корректность отдачи файлов `.gz` или `.br` в другой сборке.

Документация: [Unity Web deployment](https://docs.unity3d.com/6000.6/Documentation/Manual/webgl-deploying.html),
[Quantum Web](https://doc.photonengine.com/quantum/v3/manual/webgl).
