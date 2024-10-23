## Table of Contents

**Unit Testing with Vitest and React Testing Library**

1. [Testing Utility and Helper Functions](#testing-utility-and-helper-functions)
2. [Testing Components](#testing-components)

## Testing Utility and Helper Functions

```javascript
// utils.js

export const range = (start, end) => {
  return Array.from({ length: end - start }, (_, i) => start + i);
};

export function sum(a, b) {
  return a + b;
}
```

```javascript
// utils.test.js

import { describe, expect, it } from "vitest";
import { range, sum } from "./utils";

describe("utils", () => {
  describe("range", () => {
    it("returns correct result from 1-6 range", () => {
      const result = range(1, 6);
      expect(result).toEqual([1, 2, 3, 4, 5]);
    });

    it("returns correct result from 41-45 range", () => {
      const result = range(41, 45);
      expect(result).toEqual([41, 42, 43, 44]);
    });
  });

  describe("sum", () => {
    it("adds two numbers correctly", () => {
      const result = sum(2, 4);
      expect(result).toEqual(6);
    });

    it("adds floating-point numbers correctly", () => {
      const result = sum(0.1, 0.2);
      expect(result).toBeCloseTo(0.3);
    });
  });
});
```

```
 ✓ src/utils.test.js (4)
   ✓ utils (4)
     ✓ range (2)
       ✓ returns correct result from 1-6 range
       ✓ returns correct result from 41-45 range
     ✓ sum (2)
       ✓ adds two numbers correctly
       ✓ adds floating-point numbers correctly

 Test Files  1 passed (1)
      Tests  4 passed (4)
   Start at  17:52:51
   Duration  115ms
```

### Key Points

- Use `toEqual` for strict equality checks when you expect the values to match exactly, such as integers, strings, arrays, or objects.
- Use `toBeCloseTo` when comparing **floating-point numbers** to account for precision errors that occur due to how floating-point arithmetic works in JavaScript.

**[⬆ back to top](#table-of-contents)**

## Testing Components

### 2.1 Rendering and Querying Elements

```javascript
// Todo.jsx
import { useState } from "react";

const Todo = ({ addTodo }) => {
  const [text, setText] = useState("");

  const handleSubmit = (e) => {
    e.preventDefault();
    if (text.trim()) {
      addTodo(text);
      setText("");
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        placeholder="Add Todo"
        value={text}
        onChange={(e) => setText(e.target.value)}
      />
      <button type="submit">Add</button>
    </form>
  );
};

export default Todo;
```

```javascript
// Todo.test.js

describe("Todo", () => {
  it("renders Todo component", () => {
    render(<Todo />);
    expect(screen.getByText("Add Todo")).toBeInTheDocument();
  });
});
```

```javascript
// TodoItem.test.js

describe("TodoItem", () => {
  it("renders todo text", () => {
    render(<TodoItem todo={{ text: "Learn React", isCompleted: false }} />);
    expect(screen.getByText("Learn React")).toBeInTheDocument();
  });
});
```

### 2.2 Handling User Events

```javascript
it("adds a new todo on button click", async () => {
  render(<TodoList />);
  const user = userEvent.setup();
  await user.type(screen.getByRole("textbox"), "New Todo");
  await user.click(screen.getByRole("button", { name: /add/i }));
  expect(screen.getByText("New Todo")).toBeInTheDocument();
});
```

**Note:** `screen.getByRole('button', { name: /add/i })`: This finds the button element by its role (button) and text (matching the word "Add", case-insensitive due to the /i flag).

### 2.3 Testing Props

```javascript
it("renders completed todo", () => {
  const todo = { text: "Learn Testing", isCompleted: true };
  render(<TodoItem todo={todo} />);
  expect(screen.getByText("Learn Testing")).toHaveClass("completed");
});
```

### 2.4 Testing Conditional Rendering

```javascript
it("shows empty state when no todos", () => {
  render(<TodoList todos={[]} />);
  expect(screen.getByText("No todos yet")).toBeInTheDocument();
});
```

### Key Points

- **Keep tests focused:** Test one thing at a time (e.g., rendering, events, props).
- **Use** `screen` for **queries:** It aligns with user-centric testing.
- **Avoid testing implementation details:** Focus on behavior and what the user sees, not internal states.
- **Use** `toBeInTheDocument`: Ensures the element exists in the DOM.
- **Use** `userEvent` **for interactions:** Simulates how users interact with your UI (click, type, etc.).

**[⬆ back to top](#table-of-contents)**
