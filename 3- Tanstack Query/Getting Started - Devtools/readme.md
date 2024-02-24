markdown

# React Query Devtools Recap

## What Are React Query Devtools?
- React Query Devtools are an essential companion for your React Query journey.
- They help visualize all the inner workings of React Query.
- These devtools can save you hours of debugging when you find yourself in a pinch.
- Note that they currently do not support React Native.

## Installation and Import:
- Install the devtools package:

  ```bash
  $ npm i @tanstack/react-query-devtools

    Import the devtools in your code:

    javascript

    import { ReactQueryDevtools } from '@tanstack/react-query-devtools';

Floating Mode:

    Mount the devtools as a fixed, floating element in your app.

    A toggle in the corner of the screen allows you to show and hide the devtools.

    The toggle state is stored in localStorage across reloads.

    Example usage:

    ```js

    function App() {
      return (
        <QueryClientProvider client={queryClient}>
          {/* The rest of your application */}
          <ReactQueryDevtools initialIsOpen={false} />
        </QueryClientProvider>
      );
    }
    ```

Options:

    initialIsOpen: Set this to true if you want the devtools to default to being open.
    buttonPosition: Choose from "top-left", "top-right", "bottom-left", or "bottom-right" (defaults to bottom-right).
    position: Choose from "top", "bottom", "left", or "right" (defaults to bottom).
    client: Use a custom QueryClient if needed.
    errorTypes: Predefine errors triggered on queries.
    styleNonce: Pass a nonce for inline styles (useful for CSP).

Devtools in Production:

    Devtools are excluded in production builds.
    To lazy load them in production, you can conditionally include them based on process.env.NODE_ENV.