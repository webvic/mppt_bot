# mppt_bot
Бот для поиска троек в институте МПТТ

🌐 Сценарий работы Telegram-бота для формирования троек
🎯 Цель
Автоматизация подбора троек участников для тренировки терапевтических навыков.
Учет предпочтений по ролям и времени в удобном формате.
Оперативное уведомление участников о ходе формирования и изменения условий.
🔹 Основные роли:
Терапевт – проводит сессию.
Клиент – играет роль клиента.
Наблюдатель – анализирует процесс и даёт обратную связь.
📋 Функциональность бота:
1. Регистрация пользователя
Участник запускает бота и регистрируется, указывая:
Имя или никнейм (по желанию)
Часовой пояс (определяется по городу или вручную)
2. Создание новой тройки
Участник отправляет команду /create_group, после чего бот запрашивает:

Выбор роли: Терапевт, Клиент, Наблюдатель
Доступные временные слоты — диапазоны времени в формате:
08:00–12:00, 15:00–18:00
Комментарий (необязательно)
✅ Если тройка не заполнена, бот сообщает статус (например, "Ожидаем клиента и наблюдателя").
✅ Если уже есть две заявки с пересекающимся временем, бот предлагает участнику заполнить оставшуюся роль.

3. Вход в существующую тройку
Участник отправляет команду /join_group, после чего бот:

Показывает список незакрытых троек с указанием:
Доступных ролей
Пересекающегося времени (например, "Время: 14:00–15:00")
Участник выбирает тройку, где доступны роли и время, и занимает свободную роль.
✅ Если тройка заполняется, бот уведомляет всех участников о сформированной тройке с подтверждением времени.
✅ После подтверждения тройка становится закрытой для редактирования.

4. Уведомления
После заполнения тройки бот отправляет сообщение:
"Тройка сформирована! Время: 15:00–16:00. Роли: Терапевт — Иван, Клиент — Мария, Наблюдатель — Олег."
За 15 минут до начала бот отправляет напоминание о сессии.
Если кто-то меняет условия или выходит из тройки — бот уведомляет остальных участников.
5. Изменение условий
Команда /update_conditions позволяет участнику:

Изменить роль (если тройка ещё не полная).
Изменить доступное время.
Удалиться из незакрытой тройки.
✅ При изменении бот проверяет, не нарушится ли возможность проведения встречи.
✅ Если тройка становится неполной — оставшимся участникам приходит уведомление.

6. Отказ от участия
Команда /leave_group позволяет выйти из тройки, если встреча ещё не состоялась.
Если участник выходит, тройка становится открытой для поиска нового участника.
Если это был последний участник, тройка удаляется.
7. Просмотр информации
/my_groups – отображает список текущих троек пользователя с ролями и временем.
/open_groups – показывает список неполных троек с возможностью присоединиться.

8. Проведение сессии и архивирование
По истечении времени встречи тройка автоматически переходит в архив.
Участники получают сообщение о завершении сессии.
✅ Если сессия не состоялась (например, кто-то не явился), бот предлагает пересоздать тройку или скорректировать участников.

⚙️ Пример сценария работы
Участник А создаёт тройку в роли терапевта с доступным временем: 14:00–18:00.
Участник Б видит свободную тройку, занимает роль клиента, время совпадает.
Участник В присоединяется как наблюдатель с пересекающимся временем.
Бот сообщает: "Тройка сформирована! Время: 15:00–16:00"
За 15 минут до встречи все получают напоминание.
После окончания сессии тройка переносится в архив.
🚀 Особенности реализации
✅ Отслеживание временных зон с помощью pytz или встроенных средств Telegram.
✅ Временные интервалы сверяются с учётом часовых поясов.
✅ Формирование троек только на ближайшее свободное время (следующий полный час).
✅ Уведомления через Telegram API (sendMessage) с возможностью inline-кнопок для удобства.

🎯 Дополнительно (по желанию):
Возможность добавления тегов/тем сессий (например, "психодинамическая терапия").
Рейтинг участников после сессий для обратной связи.
Уведомления о новых свободных тройках по интересам.
