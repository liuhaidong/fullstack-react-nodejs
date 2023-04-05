# Page 1

In this section, we will walk you through the process of creating the basic structure for the Personal Assistant App using the technologies and concepts introduced earlier in the book. This includes setting up the project, creating a basic file structure, and implementing routing, components, and state management.

1. Initializing the Project

To start, let's create a new React project using Create React App with TypeScript:

```bash
bashCopy codenpx create-react-app personal-assistant-app --template typescript
```

Next, navigate to the newly created directory:

```bash
bashCopy codecd personal-assistant-app
```

2. Installing Dependencies

Install the necessary dependencies for the project:

```bash
bashCopy codenpm install react-router-dom @mui/material @emotion/react @emotion/styled
```

3. Creating the File Structure

Organize the project files into a clear structure by creating folders for pages, components, and other necessary files:

```css
cssCopy codepersonal-assistant-app/
  ├── src/
  │   ├── components/
  │   ├── pages/
  │   │   ├── Home/
  │   │   ├── TaskManager/
  │   │   ├── Calendar/
  │   │   ├── Notes/
  │   │   └── Chatbot/
  │   ├── App.tsx
  │   ├── index.tsx
  │   └── ...
  └── ...
```

4. Implementing Routing

Set up the basic routing for the application using React Router in `src/App.tsx`:

```tsx
tsxCopy codeimport React from 'react';
import { BrowserRouter, Route, Switch, Link } from 'react-router-dom';

import Home from './pages/Home/Home';
import TaskManager from './pages/TaskManager/TaskManager';
import Calendar from './pages/Calendar/Calendar';
import Notes from './pages/Notes/Notes';
import Chatbot from './pages/Chatbot/Chatbot';

function App() {
  return (
    <BrowserRouter>
      <nav>
        <Link to="/">Home</Link>
        <Link to="/task-manager">Task Manager</Link>
        <Link to="/calendar">Calendar</Link>
        <Link to="/notes">Notes</Link>
        <Link to="/chatbot">Chatbot</Link>
      </nav>
      <Switch>
        <Route exact path="/" component={Home} />
        <Route path="/task-manager" component={TaskManager} />
        <Route path="/calendar" component={Calendar} />
        <Route path="/notes" component={Notes} />
        <Route path="/chatbot" component={Chatbot} />
      </Switch>
    </BrowserRouter>
  );
}

export default App;
```

5. Creating Basic Components

Create the basic components for each page:

* Home: A welcome page that introduces the Personal Assistant App.
* TaskManager: A page to manage tasks and to-do lists.
* Calendar: A page to display and manage calendar events.
* Notes: A page to create and organize notes.
* Chatbot: A page to interact with the ChatGPT API.

For each page, create an appropriate TypeScript file (e.g., `Home.tsx`) in the corresponding folder.

6. Implementing State Management

Set up the basic state management for the application using React context and hooks. Create a context provider to store the global state and a custom hook to access and update the state.

Example: Creating a `TaskContext` and a custom `useTasks` hook.

`src/contexts/TaskContext.tsx`:

```tsx
import React, { createContext, useContext, useState } from 'react';

interface Task {
  id: string;
  title: string;
  completed: boolean;
}

interface TaskContextData {
  tasks: Task[];
  addTask: (task: Task) => void;
  removeTask: (taskId: string) => void;
  toggleTaskCompletion: (taskId: string) => void;
}

const TaskContext = createContext<TaskContextData>({} as TaskContextData);

export const TaskProvider: React.FC = ({ children }) => {
  const [tasks, setTasks] = useState<Task[]>([]);

  const addTask = (task: Task) => {
    setTasks([...tasks, task]);
  };

  const removeTask = (taskId: string) => {
    setTasks(tasks.filter((task) => task.id !== taskId));
  };

  const toggleTaskCompletion = (taskId: string) => {
    setTasks(
      tasks.map((task) =>
        task.id === taskId ? { ...task, completed: !task.completed } : task
      )
    );
  };

  return (
    <TaskContext.Provider
      value={{ tasks, addTask, removeTask, toggleTaskCompletion }}
    >
      {children}
    </TaskContext.Provider>
  );
};

export const useTasks = (): TaskContextData => {
  return useContext(TaskContext);
};
```

7. Integrating State Management with Components

Integrate the state management into the `TaskManager` component by using the custom `useTasks` hook:

`src/pages/TaskManager/TaskManager.tsx`:

```tsx
import React from 'react';
import { useTasks } from '../../contexts/TaskContext';

const TaskManager: React.FC = () => {
  const { tasks, addTask, removeTask, toggleTaskCompletion } = useTasks();

  // Render tasks and implement task management logic

  return (
    <div>
      {/* Task management UI */}
    </div>
  );
};

export default TaskManager;
```
