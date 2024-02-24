1. **Lagged Query Data** - React Query provides a way to continue to see an existing query's data while the next query loads (similar to the same UX that suspense will soon provide natively). This is extremely important when writing pagination UIs or infinite loading UIs where you do not want to show a hard loading state whenever a new query is requested. Other libraries do not have this capability and render a hard loading state for the new query (unless it has been prefetched), while the new query loads.

2. **Render Optimization** - React Query has excellent rendering performance. By default, it will automatically track which fields are accessed and only re-render if one of them changes. If you would like to opt-out of this optimization, setting `notifyOnChangeProps` to `'all'` will re-render your components whenever the query is updated. For example because it has new data, or to indicate it is fetching. React Query also batches updates together to make sure your application only re-renders once when multiple components are using the same query. If you are only interested in the `data` or `error` properties, you can reduce the number of renders even more by setting `notifyOnChangeProps` to `['data', 'error']`.

3. **Partial query matching** - Because React Query uses deterministic query key serialization, this allows you to manipulate variable groups of queries without having to know each individual query-key that you want to match, e.g., you can refetch every query that starts with `todos` in its key, regardless of variables, or you can target specific queries with (or without) variables or nested properties, and even use a filter function to only match queries that pass your specific conditions.

4. **Pre-usage Query Configuration** - This is simply a fancy name for being able to configure how queries and mutations will behave before they are used. For instance, a query can be fully configured with defaults beforehand and when the time comes to use it, only `useQuery({ queryKey })` is necessary, instead of being required to pass the fetcher and/or options with every usage. SWR does have a partial form of this feature by allowing you to pre-configure a default fetcher, but only as a global fetcher, not on a per-query basis and definitely not for mutations.

5. **Automatic Refetch after Mutation** - For truly automatic refetching to happen after a mutation occurs, a schema is necessary (like the one GraphQL provides) along with heuristics that help the library know how to identify individual entities and entity types in that schema.

6. **Normalized Caching** - React Query, SWR, and RTK-Query do not currently support automatic-normalized caching which describes storing entities in a flat architecture to avoid some high-level data duplication.

7. **SWR's Immutable Mode** - SWR ships with an "immutable" mode that does allow you to only fetch a query once for the life of the cache, but it still does not have the concept of stale-time or conditional auto-revalidation.

8. **React Router Cache Persistence** - React Router does not cache data beyond the currently matched routes. If a route is left, its data is lost.



Tanstack Query Official Doc for Comparison :  https://tanstack.com/query/latest/docs/framework/react/comparison