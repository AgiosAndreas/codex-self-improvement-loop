Установи переносимый Codex skill `self-improvement-loop` из публичного GitHub bundle:

https://raw.githubusercontent.com/AgiosAndreas/codex-self-improvement-loop/main/self-improvement-loop-transfer.zip

Checksum SHA-256:

https://raw.githubusercontent.com/AgiosAndreas/codex-self-improvement-loop/main/self-improvement-loop-transfer.sha256

Сделай это как установку skill, а не как запрос на изменение памяти.

Требования:

1. Определи фактический `<CODEX_HOME>` текущего job; используй `<CODEX_HOME>/skills`, а если переменная не задана — `~/.codex/skills`.
2. Скачай оба URL во временный каталог через `curl -fL`. Проверь SHA-256 ZIP по checksum-файлу; при несовпадении остановись и ничего не устанавливай.
3. Распакуй ZIP и прочитай `README.md` и `SKILL.md`. Внутри архива должен быть каталог `self-improvement-loop-transfer` с единственным `SKILL.md`.
4. Перед копированием выполни dry-run установщика на распакованном каталоге:

   `python3 <bundle>/scripts/install_from_gist.py --source <bundle> --dest <CODEX_HOME>/skills --dry-run`

5. Если `<CODEX_HOME>/skills/self-improvement-loop` уже существует, остановись и сообщи об этом. Не перезаписывай и не удаляй локальную версию без отдельного разрешения.
6. Если destination свободен, выполни ту же команду без `--dry-run`.
7. Проверь установленный каталог валидатором Codex:

   `/usr/bin/python3 <CODEX_HOME>/skills/.system/skill-creator/scripts/quick_validate.py <CODEX_HOME>/skills/self-improvement-loop`

   Если в этом job валидатор лежит в другом месте, найди именно `quick_validate.py` внутри `<CODEX_HOME>/skills/.system/skill-creator/` и используй его.
8. Не изменяй `CODEX_MEMORY.md`, `AGENTS.md`, историю сессий, `auth.json`, `.hermes` или другие skills. Не добавляй credentials и не публикуй содержимое локальной памяти.
9. В конце сообщи: установленный абсолютный путь, список установленных файлов, результат validator и требуется ли перезапуск/reload Codex.

