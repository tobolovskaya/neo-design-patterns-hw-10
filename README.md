## TODO CLI with Command Pattern
Цей проект — консольний TODO-застосунок, який демонструє використання патерну **Command** для управління задачами з підтримкою **undo/redo**.

### Структура проекту
```
src/
├── commands/
│   ├── Command.ts
│   ├── AbstractCommand.ts
│   ├── AddTaskCommand.ts
│   ├── RemoveTaskCommand.ts
│   ├── UpdateTaskCommand.ts
│   ├── CompleteTaskCommand.ts
│   └── CommandHistory.ts
├── models/
│   ├── Task.ts
│   └── TaskList.ts
├── services/
│   └── TaskManager.ts
└── main.ts
```

### Реалізація патерну Command
- **Command** (`Command.ts`) — інтерфейс із методами `execute()`, `undo()`, `redo()`.
- **AbstractCommand** (`AbstractCommand.ts`) — базовий клас, що реалізує `redo()` через `execute()`.
- **ConcreteCommand** (`AddTaskCommand`, `RemoveTaskCommand`, `UpdateTaskCommand`, `CompleteTaskCommand`) — кожна команда інкапсулює дію над `TaskList`:
  - `execute()` виконує дію;
  - `undo()` скасовує її, використовуючи збережений попередній стан;
  - `redo()` повторює виконання.
- **CommandHistory** (`CommandHistory.ts`) — зберігає стек виконаних команд і поточний індекс, реалізує `executeCommand()`, `undo()`, `redo()`.
- **TaskManager** (`TaskManager.ts`) — фасад, що обгортає `TaskList` та `CommandHistory`, надає методи `addTask()`, `removeTask()`, `updateTask()`, `completeTask()`, `undo()`, `redo()`.

### Як запускати проект
1. Встановити залежності:
   ```bash
   npm install
   ```
2. Запустити приклад:
   ```bash
   npx ts-node src/main.ts
   ```
3. Ви побачите послідовний виконаний сценарій з додавання, оновлення, виконання, видалення задач та їх `undo/redo`.

### Механізм undo/redo
- Кожна дія додається в `CommandHistory` через `executeCommand()`.
- **Undo**: виклик `undo()` викликає метод `undo()` останньої виконаної команди та зменшує індекс.
- **Redo**: виклик `redo()` збільшує індекс і виконує `redo()` (або `execute()`) наступної команди.
- Таким чином, можна крок за кроком відкотити або повторити серію дій над задачами.

---
© 2025 Design Patterns