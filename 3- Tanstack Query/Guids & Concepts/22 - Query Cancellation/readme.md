TanStack Query provides each query function with an AbortSignal instance. When a query becomes out-of-date or inactive, this signal will become aborted. This means that all queries are cancellable, and you can respond to the cancellation inside your query function if desired. The best part about this is that it allows you to continue to use normal async/await syntax while getting all the benefits of automatic cancellation.

### Default behavior

By default, queries that unmount or become unused before their promises are resolved are not cancelled. This means that after the promise has resolved, the resulting data will be available in the cache. This is helpful if you've started receiving a query, but then unmount the component before it finishes. If you mount the component again and the query has not been garbage collected yet, data will be available.

However, if you consume the AbortSignal, the Promise will be cancelled (e.g. aborting the fetch) and therefore, also the Query must be cancelled. Cancelling the query will result in its state being reverted to its previous state.

### Using fetch

```tsx
const query = useQuery({
  queryKey: ["todos"],
  queryFn: async ({ signal }) => {
    const todosResponse = await fetch("/todos", {
      // Pass the signal to one fetch
      signal,
    });
    const todos = await todosResponse.json();

    const todoDetails = todos.map(async ({ details }) => {
      const response = await fetch(details, {
        // Or pass it to several
        signal,
      });
      return response.json();
    });

    return Promise.all(todoDetails);
  },
});
```

### Using axios v0.22.0+

```tsx
import axios from "axios";

const query = useQuery({
  queryKey: ["todos"],
  queryFn: ({ signal }) =>
    axios.get("/todos", {
      // Pass the signal to `axios`
      signal,
    }),
});
```

### Using axios with version lower than v0.22.0

```tsx
import axios from "axios";

const query = useQuery({
  queryKey: ["todos"],
  queryFn: ({ signal }) => {
    // Create a new CancelToken source for this request
    const CancelToken = axios.CancelToken;
    const source = CancelToken.source();

    const promise = axios.get("/todos", {
      // Pass the source token to your request
      cancelToken: source.token,
    });

    // Cancel the request if TanStack Query signals to abort
    signal?.addEventListener("abort", () => {
      source.cancel("Query was cancelled by TanStack Query");
    });

    return promise;
  },
});
```

### Manual Cancellation

You might want to cancel a query manually. For example, if the request takes a long time to finish, you can allow the user to click a cancel button to stop the request. To do this, you just need to call `queryClient.cancelQueries({ queryKey })`, which will cancel the query and revert it back to its previous state. If you have consumed the signal passed to the query function, TanStack Query will additionally also cancel the Promise.

```tsx
const query = useQuery({
  queryKey: ["todos"],
  queryFn: async ({ signal }) => {
    const resp = await fetch("/todos", { signal });
    return resp.json();
  },
});

const queryClient = useQueryClient();

return (
  <button
    onClick={(e) => {
      e.preventDefault();
      queryClient.cancelQueries({ queryKey: ["todos"] });
    }}
  >
    Cancel
  </button>
);
```
