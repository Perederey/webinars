# GophKeeper: Менеджер паролей в Terminal UI
## Проектная документация

### Слайд 1: Введение - "Почему это крутой проект?"
- 🔐 Собственный менеджер паролей в терминале
- 🚀 Реальный проект для портфолио
- 💡 Практика Go в промышленной разработке
- 🎯 Решение реальной проблемы безопасности

### Слайд 2: User Stories
"Как пользователь, я хочу..."
1. "Быстро получить доступ к паролям через терминал, не открывая браузер"
2. "Синхронизировать пароли между рабочим и домашним компьютером"
3. "Хранить не только пароли, но и заметки и файлы"
4. "Иметь возможность работать с паролями даже без интернета"
5. "Быстро копировать пароль в буфер обмена одной командой"

### Слайд 3: Архитектура TUI
```
┌─ Application Layer ─────┐
│ ┌─ Views ──────────┐   │
│ │- LoginView       │   │
│ │- PasswordListView│   │
│ │- EditView       │   │
│ └─────────────────┘   │
│ ┌─ Controllers ────┐   │
│ │- UserController  │   │
│ │- DataController  │   │
│ └─────────────────┘   │
└─────────────────────────┘
```

### Слайд 4: Библиотеки для TUI
- bubbletea - фреймворк для TUI
- lipgloss - стилизация
- bubbles - готовые компоненты
- charm - utilities для терминала

### Слайд 5: Подводные камни проекта
1. Синхронизация:
   - Конфликты при офлайн изменениях
   - Race conditions при многопользовательском доступе
   - Версионирование данных

2. Безопасность:
   - Хранение мастер-пароля
   - Безопасная очистка памяти
   - Защита от перехвата данных в терминале

3. UX в Terminal UI:
   - Обработка разных размеров терминала
   - Поддержка разных кодировок
   - Работа с буфером обмена

### Слайд 6: Структура TUI приложения
```go
type App struct {
    tui       *tea.Program
    state     *AppState
    sync      *SyncManager
    crypto    *CryptoManager
    views     map[string]View
}

type View interface {
    Init() tea.Cmd
    Update(msg tea.Msg) (tea.Model, tea.Cmd)
    View() string
}
```

### Слайд 7: Паттерны проектирования
1. MVC для TUI:
   - Model: структуры данных
   - View: TUI компоненты
   - Controller: бизнес-логика

2. Repository Pattern:
   - Абстракция хранилища
   - Легкое переключение между хранилищами
   - Тестируемость

3. Service Layer:
   - Синхронизация
   - Шифрование
   - Аутентификация

### Слайд 8: Советы по реализации
1. Начните с прототипа без синхронизации
2. Используйте SQLite для локального хранения
3. Примените простой REST API для синхронизации
4. Добавьте шифрование на последнем этапе
5. Тестируйте TUI в разных терминалах

### Слайд 9: Пример интерфейса
```
┌─ GophKeeper ──────────────────┐
│ [1] Passwords   [2] Notes     │
│ [3] Files       [4] Cards     │
├────────────────────────────────┤
│ > example.com                  │
│   login: user@example.com      │
│   pass: ************          │
│                               │
│ + Add New Entry               │
└────────────────────────────────┘
```

### Слайд 10: План разработки
1. Неделя 1-2: Базовый TUI интерфейс
2. Неделя 3-4: Локальное хранение
3. Неделя 5-6: Серверная часть
4. Неделя 7-8: Синхронизация
5. Неделя 9-10: Безопасность и тесты