# Отчёт по задаче 02b

Сделано:
- `..\multnews-patch-3.zip` распакован с заменой: `hero/bible_16.md`, `hero/bible_27.md`, `tools/make_passport.py` (только стилевые формулировки: «stylized 3D cartoon» → «semi-realistic 3D rendered»), `tasks/task-02b-passport-v2.md`. Закоммичено `hero: semi-realistic style`, запушено.
- Первый круг сохранён: `hero\passport_16` → `hero\passport_16_v1` (14 файлов: 12 png + sheet.png + .keep), создана пустая `hero\passport_16`.
- Сгенерирован второй круг: 8 из 8 картинок (4 анфаса, 2 три четверти, 2 полный рост), отказов нет, fallback на Seedream не понадобился. Ориентировочно $0.20.
- Собран `hero\passport_16\sheet.png` (8 картинок), скопирован в `multnews-reports\hero\passport_16_v2_sheet.png`. Отдельные png и фото-референсы в публичный репозиторий не попали.

Проверка:
- `.\venv\Scripts\python tools\make_passport.py --age 16 --n 4 --angles front` → вывод целиком:

```
модель: gemini-3.1-flash-image-preview
папка:  C:\Users\Warda\OneDrive\Desktop\multnews\hero\passport_16
референсы: hero\reference\16\front_a.jpg, hero\reference\16\front_b.jpg

  front #1 ... ок
  front #2 ... ок
  front #3 ... ок
  front #4 ... ок

готово: 4 картинок, ошибок: 0, ориентировочно $0.10
Открой папку C:\Users\Warda\OneDrive\Desktop\multnews\hero\passport_16, выбери по одному файлу на ракурс и скажи мне их имена.
```

- `.\venv\Scripts\python tools\make_passport.py --age 16 --n 2 --angles three_quarter,full_body` → вывод целиком:

```
модель: gemini-3.1-flash-image-preview
папка:  C:\Users\Warda\OneDrive\Desktop\multnews\hero\passport_16
референсы: hero\reference\16\front_a.jpg, hero\reference\16\front_b.jpg

  three_quarter #1 ... ок
  three_quarter #2 ... ок
  full_body #1 ... ок
  full_body #2 ... ок

готово: 4 картинок, ошибок: 0, ориентировочно $0.10
Открой папку C:\Users\Warda\OneDrive\Desktop\multnews\hero\passport_16, выбери по одному файлу на ракурс и скажи мне их имена.
```

- `.\venv\Scripts\python tools\sheet.py hero\passport_16` → `готово: hero\passport_16\sheet.png (8 картинок)`.
- Лист открыт и просмотрен. Стиль заметно ближе к фото: нормальные пропорции, глаза обычного размера, текстура кожи. Шнурок и рюкзак на всех кадрах. Замечание: `front_1.png` и `front_3.png` модель сделала в полный рост, а не «голова и плечи» — настоящих анфасов два (`front_2.png`, `front_4.png`). `three_quarter_1.png` и `three_quarter_2.png` — оба корректные, `full_body_1.png` и `full_body_2.png` — корректные.

Результат: 8 картинок. Лист — `multnews-reports/hero/passport_16_v2_sheet.png` (https://github.com/sifferee/multnews-reports/blob/master/hero/passport_16_v2_sheet.png). Первый круг для сравнения — `multnews-reports/hero/passport_16_sheet.png`.

Коммит: 60b4068 (multnews, `hero: semi-realistic style`); отчёт — следующим коммитом.

Ошибки: нет

Вопросы:
1. `hero/passport_16_v1/` не покрыта `.gitignore` (там только `hero/passport_16/` и `hero/passport_27/`), поэтому висит как untracked. В git её не добавлял, коммитил отчёт адресно. Добавить строку `hero/passport_16_v1/` в `.gitignore`?
2. Два из четырёх анфасов вышли в полный рост — если нужны ещё варианты «голова и плечи», скажи, догенерирую (по $0.025 за штуку).