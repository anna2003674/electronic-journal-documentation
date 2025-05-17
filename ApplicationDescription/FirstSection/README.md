**[← Back](./README.md)**
## Второй раздел
Во второй главе описывается структура базы данных.

- **[глава 3 -> ](/ApplicationDescription/FirstSection/SecondScreen/README.md)** — 

## Структура базы данных

| **Таблица**         | **Описание**                                                                                   | **Основные поля**                                                                                                                                                          |
|---------------------|-----------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **users**           | Хранит информацию о пользователях системы.                                                    | `id`, `username`, `password`, `email`, `role`, `created_at`, `updated_at`                                                                                               |
| **roles**           | Хранит роли пользователей (администратор, учитель, ученик, родитель).                         | `id`, `name`, `description`                                                                                                                                              |
| **classes**         | Содержит информацию о классах.                                                                | `id`, `name`, `homeroom_teacher_id`, `school_year_id`, `created_at`, `updated_at`                                                                                        |
| **subjects**        | Хранит предметы, преподаваемые в школе.                                                       | `id`, `title`, `description`, `teacher_id`, `created_at`, `updated_at`                                                                                                   |
| **schedule**        | Хранит расписание уроков.                                                                     | `id`, `class_id`, `subject_id`, `room_id`, `day_of_week`, `start_time`, `end_time`                                                                                       |
| **lessons**         | Содержит данные о проведенных уроках.                                                         | `id`, `schedule_id`, `date`, `topic_id`, `created_at`, `updated_at`                                                                                                      |
| **topics**          | Хранит темы уроков.                                                                           | `id`, `title`, `description`, `created_at`, `updated_at`                                                                                                                 |
| **grades**          | Содержит оценки учеников.                                                                     | `id`, `lesson_id`, `student_id`, `grade`, `created_at`, `updated_at`                                                                                                     |
| **attendance**      | Учет посещаемости.                                                                            | `id`, `lesson_id`, `student_id`, `status`, `created_at`, `updated_at`                                                                                                    |
| **homework**        | Хранит домашние задания.                                                                      | `id`, `lesson_id`, `description`, `due_date`, `created_at`, `updated_at`                                                                                                |
| **school_years**    | Учет учебных годов.                                                                           | `id`, `start_year`, `end_year`, `created_at`, `updated_at`                                                                                                               |
| **quarters**        | Учет четвертей в учебном году.                                                                | `id`, `school_year_id`, `start_date`, `end_date`, `created_at`, `updated_at`                                                                                            |
| **class_pupil**     | Связь между классами и учениками.                                                             | `id`, `class_id`, `pupil_id`                                                                                                                                             |
| **class_subject**   | Связь между классами и предметами.                                                            | `id`, `class_id`, `subject_id`                                                                                                                                           |
| **notifications**   | Уведомления для пользователей.                                                               | `id`, `user_id`, `message`, `type`, `created_at`                                                                                                                         |
| **rooms**           | Список кабинетов в школе.                                                                     | `id`, `name`, `floor`, `created_at`, `updated_at`                                                                                                                        |

## Связи между таблицами

- **users → roles**: Один ко многим (у пользователя может быть одна роль, роль может быть у нескольких пользователей).
- **classes → users**: Один ко многим (у класса есть классный руководитель).
- **classes → school_years**: Один ко многим (один учебный год может включать несколько классов).
- **subjects → users**: Один ко многим (у предмета может быть один преподаватель).
- **schedule → classes, subjects, rooms**: Один ко многим (расписание связано с классом, предметом и кабинетом).
- **lessons → schedule**: Один ко многим (каждый урок связан с расписанием).
- **grades → lessons, users**: Один ко многим (оценка привязана к уроку и ученику).
- **attendance → lessons, users**: Один ко многим (учет посещаемости на уроке связан с учеником).
- **homework → lessons**: Один ко многим (домашнее задание привязано к уроку).
- **quarters → school_years**: Один ко многим (четверть принадлежит учебному году).

## Особенности реализации

- **Уникальность данных**: Индексы на уникальные поля, такие как `username`, `email` и другие идентификаторы.
- **История изменений**: Поля `created_at` и `updated_at` во всех таблицах для отслеживания изменений.
- **Оптимизация запросов**: Использование индексов на часто используемых полях (`class_id`, `subject_id`, `lesson_id`).


