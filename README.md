# Next.js App Router Course - Starter

## Key concepts :

### Client components VS server components :

#### Client components :

Client components are rendered in the browser after beeing sent as Javascript code. They are the basic kind of react components. Any component that needs to access brosers APIs such as localstorage or window has to be a client component

#### Server components :

Server components are rendered on the server and sent to the browser as HTML. It means that server components render static code. By default, components in Next.js 13+ are Server Components unless explicitly marked as Client Components.

### Automatic code-splitting and prefetching :

To improve the navigation experience, Next.js automatically code splits your application by route segments. This is different from a traditional React SPA, where the browser loads all your application code on initial load.

Splitting code by routes means that pages become isolated. If a certain page throws an error, the rest of the application will still work.

Furthermore, in production, whenever `<Link>` components appear in the browser's viewport, Next.js automatically prefetches the code for the linked route in the background. By the time the user clicks the link, the code for the destination page will already be loaded in the background, and this is what makes the page transition near-instant!

### Automatic redeployment :

By connecting your GitHub repository, whenever you push changes to your main branch, Vercel will automatically redeploy your application with no configuration needed.

### Requests waterfall VS Parralel data fetching :

#### _Requests waterfall_ :

A "waterfall" refers to a sequence of network requests that depend on the completion of previous requests. In the case of data fetching, each request can only begin once the previous request has returned data.

This pattern is not necessarily bad. There may be cases where you want waterfalls because you want a condition to be satisfied before you make the next request. For example, you might want to fetch a user's ID and profile information first. Once you have the ID, you might then proceed to fetch their list of friends. In this case, each request is contingent on the data returned from the previous request.

#### _Parralel data fetching_ :

A common way to avoid waterfalls is to initiate all data requests at the same time - in parallel.

In JavaScript, you can use the Promise.all() or Promise.allSettled() functions to initiate all promises at the same time.
However, there is one disadvantage of relying only on this JavaScript pattern: what happens if one data request is slower than all the others?

### Static rendering VS Dynamic rendering :

#### Static rendering :

With static rendering, data fetching and rendering happens on the server at build time. When user refreshes the page no data is refetched. It is usefull for blog articles or other contents generated during the build and that wont change

#### Dynamic rendering :

With dynamic rendering, content is rendered on the server for each user at request time. When user refreshes the page, data is refetched causing an update of the interface. It is usefull for social media's feed user informations or comment sections.

`With dynamic rendering, your application is only as fast as your slowest data fetch.`

### Components that fetches data :

Suspense is a react component allowing to display a fallback until its children have finished loading. This means that `Suspense children have to be async components`.

```ts
<Suspense fallback={<RevenueChartSkeleton />}>
  <RevenueChart /> //data is fetched down in the component
</Suspense>
```

### Search and deboucing:

searching is implemented using the URLParams. When input value change, url is updated then page is rerendered and data are refetched.

To avoid too large amount of query debouncing is implemented. Here debouncing make that the url is updated only if the user stop typing keystrokes for more than 300ms. (Game changer)
