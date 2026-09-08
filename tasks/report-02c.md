# Отчёт по задаче 02c

Сделано:
- `..\multnews-patch-4.zip` распакован с заменой: `hero/bible_16.md`, `hero/bible_27.md`, `tools/make_passport.py` (реалистичные пропорции тела в промпте и в описаниях ракурсов), `tasks/task-02c-proportions.md`. Закоммичено `hero: realistic body proportions` (`fe8b377`), запушено. Вместо `git add -A` добавлял четыре файла патча адресно, чтобы не затащить в git untracked-папку `hero/passport_16_v1/` (см. вопрос в отчёте 02b).
- Анфасы второго круга `front_1..4.png` не тронуты. Из `hero\passport_16\` удалены `full_body_1..2.png`, `three_quarter_1..2.png`, `sheet.png`.
- Сгенерировано 6 из 6 картинок (4 в полный рост, 2 вполоборота), отказов нет, fallback на Seedream не понадобился. Ориентировочно $0.15.
- Собран `hero\passport_16\sheet.png` (10 картинок: 4 старых анфаса + 6 новых), скопирован в `multnews-reports\hero\passport_16_v3_sheet.png`. Отдельные png и фото-референсы в публичный репозиторий не попали.

Проверка:
- `.\venv\Scripts\python tools\make_passport.py --age 16 --n 4 --angles full_body` → вывод целиком:

```
модель: gemini-3.1-flash-image-preview
папка:  C:\Users\Warda\OneDrive\Desktop\multnews\hero\passport_16
референсы: hero\reference\16\front_a.jpg, hero\reference\16\front_b.jpg

  full_body #1 ... ок
  full_body #2 ... ок
  full_body #3 ... ок
  full_body #4 ... ок

готово: 4 картинок, ошибок: 0, ориентировочно $0.10
Открой папку C:\Users\Warda\OneDrive\Desktop\multnews\hero\passport_16, выбери по одному файлу на ракурс и скажи мне их имена.
```

- `.\venv\Scripts\python tools\make_passport.py --age 16 --n 2 --angles three_quarter` → вывод целиком:

```
модель: gemini-3.1-flash-image-preview
папка:  C:\Users\Warda\OneDrive\Desktop\multnews\hero\passport_16
референсы: hero\reference\16\front_a.jpg, hero\reference\16\front_b.jpg

  three_quarter #1 ... ок
  three_quarter #2 ... ок

готово: 2 картинок, ошибок: 0, ориентировочно $0.05
Открой папку C:\Users\Warda\OneDrive\Desktop\multnews\hero\passport_16, выбери по одному файлу на ракурс и скажи мне их имена.
```

- `.\venv\Scripts\python tools\sheet.py hero\passport_16` → `готово: hero\passport_16\sheet.png (10 картинок)`.
- Лист открыт и просмотрен. `full_body_1..4.png` — все четыре с реалистичными пропорциями: голова около одной седьмой роста, длинные ноги, узкая талия, шнурок и рюкзак видны; «большой головы на маленьком теле» больше нет (сравни с `front_1`/`front_3` из v2 на том же листе). `three_quarter_1.png` — корректный кадр по пояс, полуулыбка. `three_quarter_2.png` — модель вместо одного ракурса нарисовала «CHARACTER REFERENCE SHEET FOR KUZYA» с текстом и восемью видами, несмотря на «no text» в промпте; как отдельный ракурс не годится, но виды сзади и в профиль на нём могут пригодиться как справка.

Результат: 6 новых картинок, на листе 10. Лист — `multnews-reports/hero/passport_16_v3_sheet.png` (https://github.com/sifferee/multnews-reports/blob/master/hero/passport_16_v3_sheet.png).

Коммит: fe8b377 (multnews, `hero: realistic body proportions`); отчёт — следующим коммитом.

Ошибки: нет

Вопросы:
1. Вопрос из отчёта 02b остаётся: добавить `hero/passport_16_v1/` в `.gitignore`? Пока папка untracked, в git не добавляется.
2. Для выбора на ракурс «вполоборота» реально годен один файл (`three_quarter_1.png`). Догенерировать ещё пару (~$0.05)?