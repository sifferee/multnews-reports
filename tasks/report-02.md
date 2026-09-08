# Отчёт по задаче 02

Сделано:
- Часть А. `..\multnews-patch-2.zip` распакован поверх проекта с заменой. Относительно коммита `75aec90` изменились `config.yaml`, `setup.ps1` (добавлен UTF-8 BOM), `tools/check_keys.py` (пустые ID → «пропуск»), `tasks/task-02-passport.md`; библии и фото-референсы совпали с уже закоммиченными. Закоммичено как `v0.1.5`, запушено в `multnews`.
- Часть Б. `hero/bible_16.md` прочитана, не менялась. Сгенерирован паспорт подростка: 12 из 12 картинок (3 ракурса × 4 варианта), отказов нет, fallback на Seedream не понадобился. Собран `hero\passport_16\sheet.png`, скопирован в `multnews-reports\hero\passport_16_sheet.png`. Сами `.png` паспорта и фото из `hero/reference/` в публичный репозиторий не попали (`hero/passport_16/` в `.gitignore`).

Проверка:
- `.\setup.ps1` напрямую → теперь запускается: `venv уже есть` → `зависимости установлены` → `ffmpeg найден` → `.env уже есть`, exit 0.
- `.\venv\Scripts\python tools\check_keys.py` → строки сверки:

```
  сверка с config.yaml → models.apiyi:
    text            claude-sonnet-5                               есть
    vision          gemini-3.5-flash                              есть
    image           gemini-3.1-flash-image-preview                есть
    image_fallback  seedream-5-0-260128                           есть
    video           (не задано)                                   пропуск

  сверка с config.yaml → models.aimlapi:
    video           kling-video/v2.6/pro/image-to-video           есть
    video_draft     alibaba/wan2.6-i2v-flash                      есть
    voice           minimax/speech-2.8-hd                         есть
    voice_clone     (не задано)                                   пропуск
```

- `.\venv\Scripts\python tools\make_passport.py --age 16 --n 4` → вывод целиком:

```
модель: gemini-3.1-flash-image-preview
папка:  C:\Users\Warda\OneDrive\Desktop\multnews\hero\passport_16
референсы: hero\reference\16\front_a.jpg, hero\reference\16\front_b.jpg

  front #1 ... ок
  front #2 ... ок
  front #3 ... ок
  front #4 ... ок
  three_quarter #1 ... ок
  three_quarter #2 ... ок
  three_quarter #3 ... ок
  three_quarter #4 ... ок
  full_body #1 ... ок
  full_body #2 ... ок
  full_body #3 ... ок
  full_body #4 ... ок

готово: 12 картинок, ошибок: 0, ориентировочно $0.30
Открой папку C:\Users\Warda\OneDrive\Desktop\multnews\hero\passport_16, выбери по одному файлу на ракурс и скажи мне их имена.
```

- `.\venv\Scripts\python tools\sheet.py hero\passport_16` → `готово: hero\passport_16\sheet.png (12 картинок)`.
- Файлы в `hero\passport_16`: front_1..4.png, three_quarter_1..4.png, full_body_1..4.png, sheet.png. Лист открыт и просмотрен: на всех 12 кадрах один и тот же стилизованный 3D-подросток, чёрная футболка, шнурок на шее, рюкзак. На `three_quarter_2.png` модель вместо одного ракурса нарисовала лист с несколькими ракурсами — при выборе учитывать.

Результат: 12 картинок. Лист — `multnews-reports/hero/passport_16_sheet.png` (https://github.com/sifferee/multnews-reports/blob/master/hero/passport_16_sheet.png).

Коммит: ecd6a0d (multnews, `v0.1.5: Kuzya bibles + reference photos, model IDs, setup.ps1 BOM`); отчёт — следующим коммитом.

Ошибки: нет

Вопросы: нет. Дальше владелец выбирает по одному файлу на ракурс из `hero\passport_16` (front_N, three_quarter_N, full_body_N) — это следующая задача.