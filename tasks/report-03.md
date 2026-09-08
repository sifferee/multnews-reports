# Отчёт по задаче 03

Сделано:
- Часть А. Утверждённый паспорт подростка скопирован в `hero/final_16/` (папка коммитится):
  - `front.png` ← `hero/passport_16/front_2.png`
  - `three_quarter.png` ← `hero/passport_16/three_quarter_1.png`
  - `full_body.png` ← `hero/passport_16/full_body_2.png`
  - `sheet_extra.png` ← `hero/passport_16/three_quarter_2.png`
- В `config.yaml` в блок `hero:` добавлена строка `final_16: hero/final_16` (больше в конфиге ничего не менялось). В `.gitignore` добавлена `hero/passport_16_v1/` — папка перестала висеть как untracked. Задача `tasks/task-03-adult.md` перенесена из `..\` в `tasks\`. Закоммичено `hero: approved teen passport` (`05cdeab`), запушено.
- Часть Б. `hero/bible_27.md` прочитана, не менялась. Сгенерирован паспорт взрослого: 12 из 12 картинок (3 ракурса × 4), отказов нет, fallback на Seedream не понадобился. Ориентировочно $0.30. Референсы в запросах: `hero\final_16\front.png` первым, затем три фото из `hero\reference\27\`.
- Собран `hero\passport_27\sheet.png` (12 картинок), скопирован в `multnews-reports\hero\passport_27_sheet.png`. Отдельные png и фото-референсы в публичный репозиторий не попали (`hero/passport_27/` в `.gitignore`).

Проверка:
- `git ls-files hero/final_16` → `front.png`, `full_body.png`, `sheet_extra.png`, `three_quarter.png`. `git status` чистый, `passport_16_v1` больше не показывается.
- `.\venv\Scripts\python tools\make_passport.py --age 27 --n 4 --derive-from hero\final_16\front.png` → вывод целиком:

```
модель: gemini-3.1-flash-image-preview
папка:  C:\Users\Warda\OneDrive\Desktop\multnews\hero\passport_27
референсы: hero\final_16\front.png, hero\reference\27\front_b.jpg, hero\reference\27\front_cap.jpg, hero\reference\27\full_body.jpg

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
Открой папку C:\Users\Warda\OneDrive\Desktop\multnews\hero\passport_27, выбери по одному файлу на ракурс и скажи мне их имена.
```

- `.\venv\Scripts\python tools\sheet.py hero\passport_27` → `готово: hero\passport_27\sheet.png (12 картинок)`.
- Лист открыт и просмотрен. На всех 12 кадрах: чёрная кепка, шнурок на шее, чёрная сумка через плечо, лёгкая щетина, полуулыбка одним уголком; лицо читается как повзрослевший подросток из `final_16`. Пропорции тела в рост реалистичные. Огрехи по отдельным файлам:
  - `front_1.png` — в полный рост вместо «голова и плечи».
  - `front_4.png` — анфас хороший, но по краям модель дорисовала врезки с другими видами.
  - `three_quarter_1.png` — снова мини-лист из нескольких ракурсов (без текста), как отдельный ракурс не годится, как справка по видам сзади/в профиль — можно.
  - Чистые кандидаты: анфас — `front_2.png`, `front_3.png`; вполоборота — `three_quarter_2.png`, `three_quarter_3.png` (по пояс), `three_quarter_4.png` (крупно); в рост — `full_body_1..4.png` все четыре.

Результат: 12 картинок. Лист — `multnews-reports/hero/passport_27_sheet.png` (https://github.com/sifferee/multnews-reports/blob/master/hero/passport_27_sheet.png).

Коммит: 05cdeab (multnews, `hero: approved teen passport`); отчёт — следующим коммитом.

Ошибки: нет

Вопросы: нет. Дальше владелец выбирает по одному файлу на ракурс из `hero\passport_27` (front_N, three_quarter_N, full_body_N).