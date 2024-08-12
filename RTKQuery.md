# RTK Query

This document demonstrates various features of RTK Query using React and TypeScript. We will cover the following topics:
1. Introduction to RTK Query
2. Loading data with RTK Query
3. Modifying data with RTK Query
4. Refreshing data with RTK Query
5. Optimistic UI with RTK Query

## 1. Introduction to RTK Query

RTK Query is a powerful data fetching and caching tool built on top of Redux Toolkit. It simplifies the process of making API requests and managing data in a Redux store.

## 2. Setting Up RTK Query

First, we need to set up RTK Query in our project. We'll create a basic API service using RTK Query.

### API Slice

Create an API slice using RTK Query.

```tsx
// src/services/api.ts
import { createApi, fetchBaseQuery } from '@reduxjs/toolkit/query/react';

export const api = createApi({
  reducerPath: 'api',
  baseQuery: fetchBaseQuery({ baseUrl: '/api' }),
  endpoints: (builder) => ({
    getItems: builder.query<Item[], void>({
      query: () => 'items',
    }),
    addItem: builder.mutation<Item, Partial<Item>>({
      query: (body) => ({
        url: 'items',
        method: 'POST',
        body,
      }),
    }),
    updateItem: builder.mutation<Item, Partial<Item>>({
      query: (body) => ({
        url: `items/${body.id}`,
        method: 'PUT',
        body,
      }),
    }),
    deleteItem: builder.mutation<{ success: boolean; id: number }, number>({
      query: (id) => ({
        url: `items/${id}`,
        method: 'DELETE',
      }),
    }),
  }),
});

export const { useGetItemsQuery, useAddItemMutation, useUpdateItemMutation, useDeleteItemMutation } = api;
```

### Setting Up the Redux Store

Configure the Redux store to include the API slice.

```tsx
// src/store.ts
import { configureStore } from '@reduxjs/toolkit';
import { api } from './services/api';

export const store = configureStore({
  reducer: {
    [api.reducerPath]: api.reducer,
  },
  middleware: (getDefaultMiddleware) =>
    getDefaultMiddleware().concat(api.middleware),
});

export type RootState = ReturnType<typeof store.getState>;
export type AppDispatch = typeof store.dispatch;
```

## 3. Creating the RTKQueryPage Component

Now, let's create the `RTKQueryPage` component to demonstrate the features.

### RTKQueryPage Component

```tsx
// src/components/RTKQueryPage.tsx
import React from 'react';
import { useGetItemsQuery, useAddItemMutation, useUpdateItemMutation, useDeleteItemMutation } from '../services/api';

export const RTKQueryPage: React.FC = () => {
  const { data: items, error, isLoading, refetch } = useGetItemsQuery();
  const [addItem] = useAddItemMutation();
  const [updateItem] = useUpdateItemMutation();
  const [deleteItem] = useDeleteItemMutation();

  if (isLoading) return <div>Loading...</div>;
  if (error) return <div>Error loading data.</div>;

  return (
    <div className="p-5">
      <h2 className="text-2xl font-bold mb-5">RTK Query Demo</h2>

      <!-- Introduction to RTK Query -->
      <div className="mb-5">
        <h3 className="text-xl font-semibold">RTK Query Introduction</h3>
        <p>RTK Query is a powerful data fetching and caching tool built on top of Redux Toolkit.</p>
      </div>

      <!-- Loading Data -->
      <div className="mb-5">
        <h3 className="text-xl font-semibold">Loading Data</h3>
        <ul>
          {items && items.map((item) => (
            <li key={item.id}>{item.name}</li>
          ))}
        </ul>
      </div>

      <!-- Modifying Data -->
      <div className="mb-5">
        <h3 className="text-xl font-semibold">Modifying Data</h3>
        <button
          className="px-4 py-2 bg-blue-500 text-white rounded"
          onClick={() => addItem({ name: 'New Item' })}
        >
          Add Item
        </button>
        {items && items[0] && (
          <button
            className="px-4 py-2 bg-green-500 text-white rounded ml-2"
            onClick={() => updateItem({ id: items[0].id, name: 'Updated Item' })}
          >
            Update First Item
          </button>
        )}
      </div>

      <!-- Refreshing Data -->
      <div className="mb-5">
        <h3 className="text-xl font-semibold">Refreshing Data</h3>
        <button
          className="px-4 py-2 bg-yellow-500 text-white rounded"
          onClick={() => refetch()}
        >
          Refresh Data
        </button>
      </div>

      <!-- Optimistic UI -->
      <div className="mb-5">
        <h3 className="text-xl font-semibold">Optimistic UI</h3>
        {items && items[0] && (
          <button
            className="px-4 py-2 bg-red-500 text-white rounded"
            onClick={() => deleteItem(items[0].id)}
          >
            Delete First Item
          </button>
        )}
      </div>
    </div>
  );
};

export default RTKQueryPage;
```

### Explanation

1. **RTK Query Introduction**: Provides a brief introduction to RTK Query.
2. **Loading Data**: Demonstrates how to load data using `useGetItemsQuery`.
3. **Modifying Data**: Shows how to add and update items using `useAddItemMutation` and `useUpdateItemMutation`.
4. **Refreshing Data**: Uses the `refetch` function to manually refresh data.
5. **Optimistic UI**: Demonstrates optimistic updates by deleting an item using `useDeleteItemMutation`.

### Final Code Structure

- **services/api.ts**: Contains the API slice and RTK Query hooks.
- **store.ts**: Configures the Redux store.
- **components/RTKQueryPage.tsx**: Demonstrates the features of RTK Query.

This setup includes a comprehensive demonstration of RTK Query features using React and TypeScript. If you have any further questions or modifications, feel free to ask!