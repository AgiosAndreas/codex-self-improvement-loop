# Переносимый пакет `self-improvement-loop`

Пакет переносит только сам Codex skill: инструкции, справочник Hermes, метаданные интерфейса и безопасный установщик. Он намеренно не содержит память пользователя, историю сессий, `auth.json`, `.hermes`, токены или другие skills.

## Самый простой способ

В новом Codex отправьте содержимое [INSTALL_PROMPT.md](INSTALL_PROMPT.md). Prompt скачает bundle из GitHub, проверит SHA-256, установит skill и не будет менять память.

### Установка через prompt

1. Откройте [INSTALL_PROMPT.md](INSTALL_PROMPT.md) в этом репозитории.
2. Скопируйте весь текст файла.
3. На другом компьютере вставьте текст в новый Codex и отправьте одним сообщением.
4. Codex сам скачает ZIP и checksum из интернета, проверит файл, установит skill в `<CODEX_HOME>/skills` и запустит validator.

Никакие файлы, флешки или ручное копирование каталога на другой компьютер не нужны. Если skill уже установлен, prompt остановится и не перезапишет его.

## Установка из терминала

Из интернета:

```bash
bundle_tmp="$(mktemp -d -t self-improvement-loop.XXXXXX)"
curl -fL https://raw.githubusercontent.com/AgiosAndreas/codex-self-improvement-loop/main/self-improvement-loop-transfer.zip \
  -o "$bundle_tmp/self-improvement-loop-transfer.zip"
unzip -q "$bundle_tmp/self-improvement-loop-transfer.zip" -d "$bundle_tmp"
python3 "$bundle_tmp/self-improvement-loop-transfer/scripts/install_from_gist.py" \
  --source "$bundle_tmp/self-improvement-loop-transfer"
```

Если ZIP уже скачан:

```bash
bundle_tmp="$(mktemp -d -t self-improvement-loop.XXXXXX)"
unzip -q self-improvement-loop-transfer.zip -d "$bundle_tmp"
python3 "$bundle_tmp/self-improvement-loop-transfer/scripts/install_from_gist.py" \
  --source "$bundle_tmp/self-improvement-loop-transfer"
```

По умолчанию skill попадёт в `<CODEX_HOME>/skills` или `~/.codex/skills`. Для отдельного job укажите его skills-root через `--dest`.

После установки перезапустите Codex или перезагрузите skills. Установщик откажется перезаписывать уже существующий `self-improvement-loop`; это преднамеренная защита от потери локальной версии.

## Что нужно передавать другому человеку

Самый надёжный комплект — ссылка на GitHub и prompt из `INSTALL_PROMPT.md`. ZIP остаётся доступным как резервный офлайн-артефакт.

Публичный источник: <https://github.com/AgiosAndreas/codex-self-improvement-loop>
