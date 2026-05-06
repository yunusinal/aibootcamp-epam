# Output WITHOUT Memory Banks

## Prompt Used
```
Generate a React component for creating a new task on a Kanban board.
The task should have a title and optional description.
Tasks go into the "To Do" column.
```

## Generated Code

### TaskForm.jsx

```jsx
import React, { useState } from 'react';
import './TaskForm.css';

const TaskForm = ({ onAddTask }) => {
  const [title, setTitle] = useState('');
  const [description, setDescription] = useState('');
  const [isOpen, setIsOpen] = useState(false);

  const handleSubmit = (e) => {
    e.preventDefault();
    if (!title) return;

    const newTask = {
      id: Date.now(),
      title,
      description,
      status: 'todo',
    };

    onAddTask(newTask);
    setTitle('');
    setDescription('');
    setIsOpen(false);
  };

  if (!isOpen) {
    return (
      <button onClick={() => setIsOpen(true)}>
        + Add Task
      </button>
    );
  }

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        placeholder="Task title"
        value={title}
        onChange={(e) => setTitle(e.target.value)}
      />
      <textarea
        placeholder="Description (optional)"
        value={description}
        onChange={(e) => setDescription(e.target.value)}
      />
      <div>
        <button type="submit">Save</button>
        <button type="button" onClick={() => setIsOpen(false)}>
          Cancel
        </button>
      </div>
    </form>
  );
};

export default TaskForm;
```

### TaskForm.css

```css
form {
  display: flex;
  flex-direction: column;
  gap: 8px;
  padding: 12px;
  background: white;
  border-radius: 8px;
  box-shadow: 0 1px 3px rgba(0,0,0,0.1);
}

input, textarea {
  padding: 8px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 14px;
}

button {
  padding: 8px 16px;
  cursor: pointer;
}
```

## Issues Found

- ❌ **Used `.jsx` not `.tsx`** — project requires TypeScript, this is plain JavaScript
- ❌ **No type annotations** — no interfaces for props or task object
- ❌ **Used `Date.now()` for IDs** — project specifies `crypto.randomUUID()`
- ❌ **No input validation message** — silently returns on empty title instead of showing "Title is required"
- ❌ **No localStorage persistence** — task is only passed via callback, never saved
- ❌ **Global CSS, not CSS Modules** — uses `TaskForm.css` with global selectors that leak styles
- ❌ **No XSS sanitization** — user input rendered without trimming or sanitizing
- ❌ **No `column` field on task** — uses `status: 'todo'` instead of `column: 'todo'`
- ❌ **Missing `createdAt` and `order` fields** — story specifies these are required
- ❌ **No keyboard accessibility** — no ARIA labels, no focus management
- ❌ **No tests generated** — zero test coverage
- ❌ **Not accessible** — buttons have no ARIA attributes, no focus trap in form

## Estimated Correction Time
**25–35 minutes** to fix all issues (rewrite in TypeScript, add types, validation, localStorage, CSS Modules, accessibility, tests)
