# Отчёт по задаче 01

Сделано:
- Инструменты проверены, всё уже стояло, winget не понадобился: git 2.55.0, gh 2.97.0, Python 3.13.14 (`py -3.13` и `python` — одно и то же), ffmpeg 8.1.2-full_build (gyan.dev).
- `setup.ps1` выполнен: создан `.\venv`, установлены зависимости из `requirements.txt`, созданы папки `work`, `hero\passport_16`, `hero\passport_27`, создан `.env`.
- В `.env` записаны `APIYI_API_KEY`, `APIYI_BASE_URL=https://vip.apiyi.com`, `AIMLAPI_KEY`, `AIMLAPI_BASE_URL=https://api.aimlapi.com`. `TG_API_ID` и `TG_API_HASH` пустые (пока не нужны).
- GitHub: `gh auth status` — уже авторизован (аккаунт sifferee). `git init`, коммит `v0.1.1: setup, check_keys, passport`, создан приватный репозиторий `multnews`, запушен, ветка `master`.
- `git ls-files` — `.env` в индексе нет (в `.gitignore` есть `.env`, `venv/`, `work/`, `hero/passport_*`).
- Ключи проверены `tools\check_keys.py` — оба ключа рабочие, вывод ниже целиком.
- Создан публичный репозиторий отчётов `..\multnews-reports` с `README.md`, запушен.

Проверка:
- `git --version; gh --version; py -3.13 --version; ffmpeg -version` → версии выше.
- `.\setup.ps1` → в Windows PowerShell 5.1 напрямую НЕ запускается: файл сохранён в UTF-8 без BOM, и PowerShell 5.1 читает его в кодировке ANSI, из-за чего символ «—» внутри строк превращается в закрывающую кавычку и парсер падает (`Missing closing '}'`, `Unexpected token ')'`). Код по условию задачи не менял: сделал временную копию скрипта с UTF-8 BOM в папке проекта, запустил её через `powershell -File`, после запуска копию удалил. Вывод скрипта: `venv создан` → `зависимости установлены` → `ffmpeg найден` → `создан .env`. Вопрос владельцу ниже.
- `git ls-files | Select-String '\.env$'` → пусто, `.env` не отслеживается.
- `gh repo create multnews --private --source=. --push` → https://github.com/sifferee/multnews, ветка master.
- `gh repo create multnews-reports --public --source=. --push` → https://github.com/sifferee/multnews-reports.
- `.\venv\Scripts\python tools\check_keys.py` → вывод целиком:

```
=== APIYI ===
  ключ рабочий, доступно моделей: 279

  текст (139):
    claude-fable-5
    claude-fable-5-1
    claude-fable-5-1-thinking
    claude-fable-5-thinking
    claude-haiku-4-5-20251001
    claude-haiku-4-5-20251001-thinking
    claude-opus-4-20250514
    claude-opus-4-20250514-thinking
    claude-opus-4-5-20251101
    claude-opus-4-5-20251101-thinking
    claude-opus-4-6
    claude-opus-4-6-thinking
    claude-opus-4-7
    claude-opus-4-7-thinking
    claude-opus-4-8
    claude-opus-4-8-thinking
    claude-opus-5
    claude-opus-5-thinking
    claude-sonnet-4-20250514
    claude-sonnet-4-20250514-thinking
    claude-sonnet-4-5-20250929
    claude-sonnet-4-5-20250929-thinking
    claude-sonnet-4-6
    claude-sonnet-4-6-thinking
    claude-sonnet-5
    claude-sonnet-5-thinking
    deepseek-r1
    deepseek-v3
    deepseek-v3.1
    deepseek-v3.2
    deepseek-v3.2-exp
    deepseek-v4-flash
    deepseek-v4-flash-0731
    deepseek-v4-flash-260425
    deepseek-v4-flash-ga-260731
    deepseek-v4-flash-vision-exp
    deepseek-v4-pro
    deepseek-v4-pro-0813
    deepseek-v4-pro-260425
    gemini-3-flash-preview
    ... ещё 99

  картинки (37):
    chatgpt-image-latest
    flux-2-flex
    flux-2-klein-4b
    flux-2-klein-9b
    flux-2-max
    flux-2-pro
    flux-dev
    flux-kontext-max
    flux-kontext-pro
    gemini-2.5-flash-image
    gemini-2.5-flash-image-preview
    gemini-3-pro-image
    gemini-3-pro-image-preview
    gemini-3-pro-image-preview-1k
    gemini-3-pro-image-preview-2k
    gemini-3-pro-image-preview-4k
    gemini-3.1-flash-image
    gemini-3.1-flash-image-4k
    gemini-3.1-flash-image-preview
    gemini-3.1-flash-image-preview-4k
    gemini-3.1-flash-lite-image
    gpt-image-1
    gpt-image-1-mini
    gpt-image-1.5
    gpt-image-1.5-2025-12-16
    gpt-image-2
    gpt-image-2-all
    gpt-image-2-vip
    grok-imagine-image
    grok-imagine-image-quality
    nano-banana
    nano-banana-2
    nano-banana-pro
    seedream-4-0-250828
    seedream-4-5-251128
    seedream-5-0-260128
    seedream-5-0-pro-260628

  видео (2):
    veo-3.1-fast-generate-preview
    veo-3.1-generate-preview

  сверка с config.yaml → models.apiyi:
    text            claude-sonnet-5                               есть
    vision          gemini-3.5-flash                              есть
    image           gemini-3.1-flash-image-preview                есть
    image_fallback  seedream-5.0-lite                             НЕТ — поправь ID в config.yaml
    video           doubao-seedance-2-0-mini-260615               НЕТ — поправь ID в config.yaml

=== AI/ML API ===
  ответ получен, моделей в каталоге: 785

  голос (23):
    alibaba/qwen3-tts-flash
    deepgram/nova-2-voicemail
    elevenlabs/eleven_multilingual_v2
    elevenlabs/eleven_music
    elevenlabs/eleven_turbo_v2_5
    elevenlabs/v3_alpha
    inworld/tts-1
    inworld/tts-1-5-max
    inworld/tts-1-5-mini
    inworld/tts-1-max
    microsoft/vibevoice-1.5b
    microsoft/vibevoice-7b
    minimax/speech-2.5-hd-preview
    minimax/speech-2.5-turbo-preview
    minimax/speech-2.6-hd
    minimax/speech-2.6-turbo
    minimax/speech-2.8-hd
    minimax/speech-2.8-turbo
    openai/gpt-4o-mini-tts
    openai/tts-1
    openai/tts-1-hd
    vibevoice
    vibevoice/7b

  видео (168):
    alibaba/wan-2-6-i2v
    alibaba/wan-2-6-image
    alibaba/wan-2-6-image-to-video-flash
    alibaba/wan-2-6-r2v
    alibaba/wan-2-6-t2v
    alibaba/wan-2-7-i2v
    alibaba/wan-2-7-image
    alibaba/wan-2-7-image-pro
    alibaba/wan-2-7-r2v
    alibaba/wan-2-7-t2v
    alibaba/wan-3-0-video
    alibaba/wan2.1-t2v-plus
    alibaba/wan2.1-t2v-turbo
    alibaba/wan2.2-14b-animate-move
    alibaba/wan2.2-14b-animate-replace
    alibaba/wan2.2-i2v-plus
    alibaba/wan2.2-t2i-flash
    alibaba/wan2.2-t2i-plus
    alibaba/wan2.2-t2v-plus
    alibaba/wan2.2-vace-fun-a14b-depth
    alibaba/wan2.2-vace-fun-a14b-inpainting
    alibaba/wan2.2-vace-fun-a14b-outpainting
    alibaba/wan2.2-vace-fun-a14b-pose
    alibaba/wan2.2-vace-fun-a14b-reframe
    alibaba/wan2.5-i2v-preview
    alibaba/wan2.5-t2i-preview
    alibaba/wan2.5-t2v-preview
    alibaba/wan2.6-i2v
    alibaba/wan2.6-i2v-flash
    alibaba/wan2.6-image
    alibaba/wan2.6-r2v
    alibaba/wan2.6-t2v
    alibaba/wan2.7-i2v
    alibaba/wan2.7-image
    alibaba/wan2.7-image-pro
    alibaba/wan2.7-r2v
    alibaba/wan2.7-t2v
    alibaba/wan3.0-video
    bytedance/dreamina-seedance-2-0
    bytedance/dreamina-seedance-2-0-fast
    ... ещё 128

  сверка с config.yaml → models.aimlapi:
    video           kling-video/v2.6/pro/image-to-video           есть
    video_draft     wan/v2.6/image-to-video                       НЕТ — возьми ID из списка выше
    voice           minimax/speech-2.8-hd                         есть
    voice_clone     minimax/voice-clone                           НЕТ — возьми ID из списка выше

=== Telegram ===
  не заполнено — нужно только для каналов без веб-превью, пока можно пропустить
```

Сверка ID моделей из `config.yaml` (конфиг не трогал, правило 4):
- APIYI: `text` claude-sonnet-5 — есть; `vision` gemini-3.5-flash — есть; `image` gemini-3.1-flash-image-preview — есть.
- APIYI: `image_fallback` seedream-5.0-lite — НЕТ. В каталоге есть `seedream-5-0-260128` и `seedream-5-0-pro-260628`.
- APIYI: `video` doubao-seedance-2-0-mini-260615 — НЕТ. В APIYI видео-семейство отдаёт только `veo-3.1-generate-preview` и `veo-3.1-fast-generate-preview`; seedance по этому ключу в APIYI не виден. (Видео по конфигу всё равно идёт через aimlapi.)
- AI/ML API: `video` kling-video/v2.6/pro/image-to-video — есть; `voice` minimax/speech-2.8-hd — есть.
- AI/ML API: `video_draft` wan/v2.6/image-to-video — НЕТ. Похожие в каталоге: `alibaba/wan2.6-i2v`, `alibaba/wan2.6-i2v-flash`, `alibaba/wan-2-6-i2v`, `alibaba/wan-2-6-image-to-video-flash`.
- AI/ML API: `voice_clone` minimax/voice-clone — НЕТ. В списке голосовых моделей клонирования minimax нет (список из 23 голосовых ID выше).

Коммит: b588ea1 (multnews, `v0.1.1: setup, check_keys, passport`); отчёт — следующим коммитом.

Ошибки:
- `setup.ps1` не запускается напрямую в PowerShell 5.1 из-за кодировки (описано выше). Обход — временная копия с BOM. Сам файл не менял.
- Четыре ID моделей в `config.yaml` не найдены по ключам (список выше). Не менял.

Вопросы:
1. Разрешить пересохранить `setup.ps1` в UTF-8 с BOM (содержимое без изменений), чтобы он запускался как написано в задаче? Иначе каждый запуск придётся делать через обходной путь.
2. Какие ID подставить в `config.yaml` вместо четырёх отсутствующих (`image_fallback`, `video` в apiyi; `video_draft`, `voice_clone` в aimlapi)? Кандидаты перечислены выше; сам не подбирал.

Репозитории:
- Код (приватный): https://github.com/sifferee/multnews
- Отчёты (публичный): https://github.com/sifferee/multnews-reports