# Архитектура данных

Исходный цифровой след хранится во внутреннем raw-слое. Не следует публиковать raw-профили в GitHub.

Слои:
- raw — исходные записи;
- normalized — единый формат;
- competency — маппинг в КРМ;
- analytics — профили, подразделения, проекты, дефициты;
- presentation — dashboard/API/отчёты.

Минимальный provenance: `employee_hash`, `source_system`, `source_record_id`, `record_date`, `activity_type`, `raw_value`, `normalized_value`, `knowledge_domain`, `competency_id`, `evidence_weight`, `competency_level`, `mapping_version`.

Варианты обновления:
1. Регламентный ETL/ELT — публикации, ДПО, кадровые и учебные данные.
2. API/event-driven — инкрементальный пересчёт после события.
3. Manual refresh — пилот.

Алгоритм: новая/изменённая запись → повторный маппинг → пересчёт затронутых компетенций → новая версия профиля → обновление аналитики подразделения и проектов.

Важно: JSON в `data/profile_example_from_trace.json` создан вручную по TXT только как демонстрация. Это не автоматическое извлечение.
