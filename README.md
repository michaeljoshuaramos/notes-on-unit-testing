## Table of Contents

**Unit Testing with Vitest and React Testing Library**

1. [Testing utility and helper functions](#)

## Testing utility and helper functions

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
  });
});
```

```
 ✓ src/utils.test.js (3)
   ✓ utils (3)
     ✓ range (2)
       ✓ returns correct result from 1-6 range
       ✓ returns correct result from 41-45 range
     ✓ sum (1)
       ✓ should add two numbers correctly

 Test Files  1 passed (1)
      Tests  3 passed (3)
   Start at  17:04:11
   Duration  101ms
```

**[⬆ back to top](#table-of-contents)**
