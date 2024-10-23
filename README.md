## Table of Contents

**Unit Testing with Vitest and React Testing Library**

1. [Testing Utility and Helper Functions](#)

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
