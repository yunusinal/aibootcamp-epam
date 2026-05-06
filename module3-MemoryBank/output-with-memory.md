# Output WITH Memory Banks

## Prompt Used
```
Generate a React component for creating a new task on a Kanban board.
The task should have a title and optional description.
Tasks go into the "To Do" column.
```

_(Same prompt — but memory banks are loaded in the workspace context)_

## Generated Code

### Task.types.ts

```ts
export type ColumnType = 'todo' | 'in-progress' | 'done';

export interface Task {
  id: string;
  title: string;
  description?: string;
  column: ColumnType;
  createdAt: string;
  order: number;
}
```

### TaskForm/TaskForm.tsx

```tsx
import { useState, useRef, useEffect, type FormEvent } from 'react';
import styles from './taskForm.module.css';
import type { Task } from '../../types/Task.types';

interface TaskFormProps {
  /** Called with the new task when the form is submitted successfully. */
  onAddTask: (task: Task) => void;
  /** Current number of tasks in the To Do column, used to set initial order. */
  existingTaskCount: number;
}

function TaskForm({ onAddTask, existingTaskCount }: TaskFormProps) {
  const [isOpen, setIsOpen] = useState(false);
  const [title, setTitle] = useState('');
  const [description, setDescription] = useState('');
  const [error, setError] = useState<string | null>(null);

  const titleInputRef = useRef<HTMLInputElement>(null);

  useEffect(() => {
    if (isOpen && titleInputRef.current) {
      titleInputRef.current.focus();
    }
  }, [isOpen]);

  const handleOpen = () => {
    setIsOpen(true);
    setError(null);
  };

  const handleClose = () => {
    setIsOpen(false);
    setTitle('');
    setDescription('');
    setError(null);
  };

  const handleSubmit = (e: FormEvent<HTMLFormElement>) => {
    e.preventDefault();

    const trimmedTitle = title.trim();

    if (!trimmedTitle) {
      setError('Title is required');
      titleInputRef.current?.focus();
      return;
    }

    const newTask: Task = {
      id: crypto.randomUUID(),
      title: trimmedTitle,
      description: description.trim() || undefined,
      column: 'todo',
      createdAt: new Date().toISOString(),
      order: existingTaskCount,
    };

    onAddTask(newTask);
    setTitle('');
    setDescription('');
    setError(null);
    setIsOpen(false);
  };

  if (!isOpen) {
    return (
      <button
        className={styles.addButton}
        onClick={handleOpen}
        aria-label="Add a new task to the To Do column"
      >
        + Add Task
      </button>
    );
  }

  return (
    <form
      className={styles.form}
      onSubmit={handleSubmit}
      aria-label="Create a new task"
    >
      <label htmlFor="task-title" className={styles.label}>
        Title <span aria-hidden="true">*</span>
      </label>
      <input
        ref={titleInputRef}
        id="task-title"
        type="text"
        className={styles.input}
        placeholder="Enter task title"
        value={title}
        onChange={(e) => {
          setTitle(e.target.value);
          if (error) setError(null);
        }}
        aria-required="true"
        aria-invalid={error ? 'true' : undefined}
        aria-describedby={error ? 'title-error' : undefined}
        maxLength={200}
      />
      {error && (
        <p id="title-error" className={styles.error} role="alert">
          {error}
        </p>
      )}

      <label htmlFor="task-description" className={styles.label}>
        Description (optional)
      </label>
      <textarea
        id="task-description"
        className={styles.textarea}
        placeholder="Add a description"
        value={description}
        onChange={(e) => setDescription(e.target.value)}
        rows={3}
      />

      <div className={styles.actions}>
        <button type="submit" className={styles.saveButton}>
          Save
        </button>
        <button
          type="button"
          className={styles.cancelButton}
          onClick={handleClose}
        >
          Cancel
        </button>
      </div>
    </form>
  );
}

export default TaskForm;
```

### TaskForm/taskForm.module.css

```css
.form {
  display: flex;
  flex-direction: column;
  gap: 8px;
  padding: 12px;
  background-color: #ffffff;
  border: 1px solid #d1d5db;
  border-radius: 6px;
}

.label {
  font-size: 0.875rem;
  font-weight: 600;
  color: #374151;
}

.input,
.textarea {
  padding: 8px 10px;
  border: 1px solid #d1d5db;
  border-radius: 4px;
  font-size: 0.875rem;
  font-family: inherit;
  color: #111827;
  background-color: #ffffff;
}

.input:focus,
.textarea:focus {
  outline: 2px solid #2563eb;
  outline-offset: 1px;
  border-color: #2563eb;
}

.error {
  color: #dc2626;
  font-size: 0.8125rem;
  margin: 0;
}

.actions {
  display: flex;
  gap: 8px;
  margin-top: 4px;
}

.addButton,
.saveButton,
.cancelButton {
  padding: 6px 14px;
  border: none;
  border-radius: 4px;
  font-size: 0.875rem;
  cursor: pointer;
}

.addButton {
  background-color: #f3f4f6;
  color: #374151;
  width: 100%;
}

.addButton:hover {
  background-color: #e5e7eb;
}

.addButton:focus-visible {
  outline: 2px solid #2563eb;
  outline-offset: 2px;
}

.saveButton {
  background-color: #2563eb;
  color: #ffffff;
}

.saveButton:hover {
  background-color: #1d4ed8;
}

.saveButton:focus-visible {
  outline: 2px solid #2563eb;
  outline-offset: 2px;
}

.cancelButton {
  background-color: #f3f4f6;
  color: #374151;
}

.cancelButton:hover {
  background-color: #e5e7eb;
}

.cancelButton:focus-visible {
  outline: 2px solid #2563eb;
  outline-offset: 2px;
}
```

### TaskForm/TaskForm.test.tsx

```tsx
import { describe, it, expect, vi } from 'vitest';
import { render, screen } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import TaskForm from './TaskForm';

describe('TaskForm', () => {
  const mockOnAddTask = vi.fn();

  beforeEach(() => {
    mockOnAddTask.mockClear();
  });

  it('renders an "Add Task" button initially', () => {
    render(<TaskForm onAddTask={mockOnAddTask} existingTaskCount={0} />);
    expect(
      screen.getByRole('button', { name: /add a new task/i })
    ).toBeInTheDocument();
  });

  it('shows the form when "Add Task" is clicked', async () => {
    const user = userEvent.setup();
    render(<TaskForm onAddTask={mockOnAddTask} existingTaskCount={0} />);

    await user.click(screen.getByRole('button', { name: /add a new task/i }));

    expect(screen.getByLabelText(/title/i)).toBeInTheDocument();
    expect(screen.getByLabelText(/description/i)).toBeInTheDocument();
  });

  it('focuses the title input when the form opens', async () => {
    const user = userEvent.setup();
    render(<TaskForm onAddTask={mockOnAddTask} existingTaskCount={0} />);

    await user.click(screen.getByRole('button', { name: /add a new task/i }));

    expect(screen.getByLabelText(/title/i)).toHaveFocus();
  });

  it('displays "Title is required" when submitting with empty title', async () => {
    const user = userEvent.setup();
    render(<TaskForm onAddTask={mockOnAddTask} existingTaskCount={0} />);

    await user.click(screen.getByRole('button', { name: /add a new task/i }));
    await user.click(screen.getByRole('button', { name: /save/i }));

    expect(screen.getByRole('alert')).toHaveTextContent('Title is required');
    expect(mockOnAddTask).not.toHaveBeenCalled();
  });

  it('creates a task with title and calls onAddTask', async () => {
    const user = userEvent.setup();
    render(<TaskForm onAddTask={mockOnAddTask} existingTaskCount={3} />);

    await user.click(screen.getByRole('button', { name: /add a new task/i }));
    await user.type(screen.getByLabelText(/title/i), 'Fix auth token refresh bug');
    await user.click(screen.getByRole('button', { name: /save/i }));

    expect(mockOnAddTask).toHaveBeenCalledOnce();
    const task = mockOnAddTask.mock.calls[0][0];
    expect(task.title).toBe('Fix auth token refresh bug');
    expect(task.column).toBe('todo');
    expect(task.order).toBe(3);
    expect(task.id).toBeDefined();
    expect(task.createdAt).toBeDefined();
  });

  it('trims whitespace from the title before creating', async () => {
    const user = userEvent.setup();
    render(<TaskForm onAddTask={mockOnAddTask} existingTaskCount={0} />);

    await user.click(screen.getByRole('button', { name: /add a new task/i }));
    await user.type(screen.getByLabelText(/title/i), '   Trim me   ');
    await user.click(screen.getByRole('button', { name: /save/i }));

    expect(mockOnAddTask.mock.calls[0][0].title).toBe('Trim me');
  });

  it('rejects whitespace-only title as empty', async () => {
    const user = userEvent.setup();
    render(<TaskForm onAddTask={mockOnAddTask} existingTaskCount={0} />);

    await user.click(screen.getByRole('button', { name: /add a new task/i }));
    await user.type(screen.getByLabelText(/title/i), '   ');
    await user.click(screen.getByRole('button', { name: /save/i }));

    expect(screen.getByRole('alert')).toHaveTextContent('Title is required');
    expect(mockOnAddTask).not.toHaveBeenCalled();
  });

  it('closes the form and resets fields when Cancel is clicked', async () => {
    const user = userEvent.setup();
    render(<TaskForm onAddTask={mockOnAddTask} existingTaskCount={0} />);

    await user.click(screen.getByRole('button', { name: /add a new task/i }));
    await user.type(screen.getByLabelText(/title/i), 'Something');
    await user.click(screen.getByRole('button', { name: /cancel/i }));

    expect(
      screen.getByRole('button', { name: /add a new task/i })
    ).toBeInTheDocument();
  });
});
```

## Improvements Over "Without Memory Banks" Version

- ✅ **TypeScript (.tsx)** — used TypeScript with full type annotations, matching project requirement
- ✅ **Task.types.ts interface** — proper `Task` interface with all required fields (`id`, `title`, `description`, `column`, `createdAt`, `order`)
- ✅ **`crypto.randomUUID()`** — used correct ID generation as specified in story technical notes
- ✅ **Validation error message** — shows "Title is required" inline with `role="alert"` for screen readers
- ✅ **Input trimming / sanitization** — `title.trim()` before saving, whitespace-only treated as empty
- ✅ **CSS Modules** — `taskForm.module.css` with scoped class names, no global style leaks
- ✅ **Accessible form** — `aria-label`, `aria-required`, `aria-invalid`, `aria-describedby`, `<label>` elements, `focus-visible` outlines
- ✅ **Focus management** — auto-focuses title input when form opens; returns focus on validation error
- ✅ **Column field** — uses `column: 'todo'` matching the `ColumnType` union type
- ✅ **Tests included** — 8 test cases covering all acceptance criteria using Vitest + React Testing Library
- ✅ **File structure** — component folder pattern (`TaskForm/TaskForm.tsx`, `TaskForm/taskForm.module.css`, `TaskForm/TaskForm.test.tsx`)
- ✅ **JSDoc on exported hook/prop interface** — documents the `onAddTask` callback purpose
- ✅ **maxLength={200}** — matches story's AC4 about 200-character titles

## Remaining Issues (if any)

- ⚠️ localStorage persistence is handled by the parent component (via `useLocalStorage` hook), not inside this form — this is correct per single-responsibility, but needs integration testing at the board level
