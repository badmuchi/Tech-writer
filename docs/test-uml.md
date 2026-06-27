# Sequence Diagram

```mermaid
sequenceDiagram
    autonumber
    actor User as Клиент (Браузер)
    participant API as Weather API Сервер
    participant DB as База Данных (Кэш)

    User->>API: GET /v1/weather?city=London&key=xyz
    Note over API: Проверка API-ключа и валидация города
    alt Если ключ валидный (Успех)
        API->>DB: Запрос данных по городу London
        DB-->>API: Возврат актуального JSON погоды
        API-->>User: 200 OK (Данные о погоде в JSON)
    else Если ключ неверный (Ошибка)
        API-->>User: 401 Unauthorized (Invalid API Key)
    end
