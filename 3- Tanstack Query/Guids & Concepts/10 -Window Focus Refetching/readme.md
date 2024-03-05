If a user leaves your application and returns and the query data is stale, TanStack Query automatically requests fresh data for you in the background. You can disable this globally or per-query using the `refetchOnWindowFocus` option:

## Disabling Globally

```tsx
const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      refetchOnWindowFocus: false, // default: true
    },
  },
});

function App() {
  return <QueryClientProvider client={queryClient}>...</QueryClientProvider>;
}
```

## Disabling Per-Query

```tsx
useQuery({
  queryKey: ["todos"],
  queryFn: fetchTodos,
  refetchOnWindowFocus: false,
});
```

### Custom Window Focus Event

In rare circumstances, you may want to manage your own window focus events that trigger TanStack Query to revalidate. To do this, TanStack Query provides a `focusManager.setEventListener` function that supplies you the callback that should be fired when the window is focused and allows you to set up your own events. When calling `focusManager.setEventListener`, the previously set handler is removed (which in most cases will be the default handler) and your new handler is used instead. For example, this is the default handler:

```tsx
focusManager.setEventListener((handleFocus) => {
  // Listen to visibilitychange
  if (typeof window !== "undefined" && window.addEventListener) {
    window.addEventListener("visibilitychange", () => handleFocus(), false);
    return () => {
      // Be sure to unsubscribe if a new handler is set
      window.removeEventListener("visibilitychange", () => handleFocus());
    };
  }
});
```

## Managing focus state

```tsx
import { focusManager } from "@tanstack/react-query";

// Override the default focus state
focusManager.setFocused(true);

// Fallback to the default focus check
focusManager.setFocused(undefined);
```
