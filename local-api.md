# Локальный API codef

Локальный сервер позволяет вызвать установленную модель Ollama из скрипта или другой программы.

1. Установи модель в codef.
2. Открой «Настройки → Модели и API → Локальный API» и нажми «Запустить».
3. Скопируй базовый URL и ключ. Ключ меняется при новом запуске сервера. По умолчанию базовый URL — `http://127.0.0.1:1234/v1`.

## Список установленных моделей

Передай ключ в переменной окружения `CODEF_API_KEY`. Пример для терминала macOS или Linux.

```sh
curl --fail-with-body \
  -H "Authorization: Bearer $CODEF_API_KEY" \
  http://127.0.0.1:1234/v1/models
```

В Windows используй `curl.exe` и `$env:CODEF_API_KEY` в PowerShell.

## Запрос к модели

Возьми значение `id` из списка моделей и подставь его вместо `MODEL_ID` в файле `request.json`.

```json
{
  "model": "MODEL_ID",
  "messages": [{ "role": "user", "content": "Объясни рекурсию в двух предложениях." }]
}
```

```sh
curl --fail-with-body \
  -H "Authorization: Bearer $CODEF_API_KEY" \
  -H "Content-Type: application/json" \
  --data-binary @request.json \
  http://127.0.0.1:1234/v1/chat/completions
```

Ответ находится в `choices[0].message.content`. Сервер слушает только этот компьютер и останавливается при выходе из codef.

[Потоковые ответы, токены и коды ошибок](https://codef.su/ru/help/local-api/) · [Примеры на Node.js и Python](https://codef.su/ru/developers/) · [CLI для терминала](https://github.com/Fle3n/codef-cli)
