# usePagination

### Hook:
```jsx
import { useState, useMemo } from "react";

const usePagination = ({ items, pageSize, currentPage }) => {
  const [page, setPage] = useState(currentPage);

  const totalPages = useMemo(() => {
    return Math.ceil(items.length / pageSize);
  }, [items.length, pageSize]);

  const startIndex = (page - 1) * pageSize;
  const endIndex = startIndex + pageSize;
  const itemsToShow = useMemo(() => {
    return items.slice(startIndex, endIndex);
  }, [items, startIndex, endIndex]);

  const goToPage = (pageNumber) => {
    if (pageNumber < 1 || pageNumber > totalPages) {
      return;
    }
    setPage(pageNumber);
  };

  return { itemsToShow, totalPages, goToPage };
};

export default usePagination;

```

### How to use:
```jsx
import React, { useState } from "react";
import usePagination from "./usePagination";

const items = Array.from({ length: 50 }, (_, i) => `Item ${i + 1}`);

const Example = () => {
  const [page, setPage] = useState(1);
  const { itemsToShow, totalPages, goToPage } = usePagination({
    items,
    pageSize: 10,
    currentPage: page,
  });

  return (
    <div>
      <ul>
        {itemsToShow.map((item) => (
          <li key={item}>{item}</li>
        ))}
      </ul>
      <p>
        Showing page {page} of {totalPages}
      </p>
      <button onClick={() => goToPage(page - 1)}>Prev</button>
      <button onClick={() => goToPage(page + 1)}>Next</button>
    </div>
  );
};

export default Example;
```
