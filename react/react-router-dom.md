# react-router-dom

[Tutorial Link](https://reactrouter.com/docs/en/v6/getting-started/tutorial)

## Tutorial
A quick start.

### Installation
```Bash
cd <wordspace>
npm install react-router-dom@6
```

### Connect the URL
`BrowserRouter` is the component for rendering the web given urls.  
Wrap your own `App` with `BrowserRouter` like this:
```Javascript
render(
  <BrowserRouter>
    <App />
  </BrowserRouter>,
  rootElement
);
```

### Link
`Link` is a component for a html `<a>` like element.  
A simple navigation bar:
```Javascript
<nav>
    <Link to="/invoices">Invoices</Link> |{" "}
    <Link to="/expenses">Expenses</Link>
</nav>
```

### Routes
If there is only one `App` in `BrowserRouter`, the router can only manage the `/` url. Add `Routes` to manage all urls.
```Javascript
<BrowserRouter>
    <Routes>
        <Route path="/" element={<App />} />
        <Route path="expenses" element={<Expenses />} />
        <Route path="invoices" element={<Invoices />} />
    </Routes>
</BrowserRouter>
```
The `element` prop of `Route` accepts an element.

### Nested Routes
UI is a series of nested layouts, e.g.,
```Html
<body>
    <nav>
    </nav>
    <div id="content">
        <div id="element_1">
        </div>
    </div>
</body>
```
We hope different urls navigates to different contents, e.g., annotation interface and data browser.

The `Route` can be nested:
```Javascript
 <BrowserRouter>
    <Routes>
      <Route path="/" element={<App />}>
        <Route path="expenses" element={<Expenses />} />
        <Route path="invoices" element={<Invoices />} />
      </Route>
    </Routes>
</BrowserRouter>
```
- The path of child `Route` is relative to the path of parent.
- The element of child `Route` will render the `<Outlet />` element in the parent `Route`'s element.
Comment: `<Outlet />` is like a placeholder to populate.

### "No Match" Route
```Javascript
<Route
      path="*"
      element={
        <main style={{ padding: "1rem" }}>
          <p>There's nothing here!</p>
        </main>
      }
/>
```
This is also a route, which behaves in a nested manner. If there are two "No Match" Route at different Route layers, the url will match the closest one.

### Reading URL Params
A "URL param" is part of the path, which can be matched by:
```Javascript
<Route path=":invoiceId" element={<Invoice />} />
```
The param can be accessed by the function `useParams` provided by `react-router-dom`:
```Javascript
params = useParams();
return <h2>Invoice: {params.invoiceId}</h2>;
```

### Index Routes
- Index routes render in the parent routes outlet at the parent route's path.
- Index routes match when a parent route matches but none of the other children match.
- Index routes are the **default child route** for a parent route.
```Javascript
<Route index element={<p>Please select</p>}/>
```

### Active Links
Each Link is bound to a path. If the link (path) is active, that is, the current url matches the path, we hope the Link is aware of such status.
Use `NavLink`
```JavaScript
<NavLink
    style={({ isActive }) => {
        return {
        display: "block",
        margin: "1rem 0",
        color: isActive ? "red" : "",
        };
    }}
    to={`/invoices/${invoice.number}`}
    key={invoice.number}
    >
    {invoice.name}
</NavLink>
```
the `style` props is a function, which accept one argument isActive and return an style object.
Can also change the style by className on NavLink:
```JavaScript
<NavLink className={({ isActive }) => isActive ? "red" : "blue"} />
```

### Search params
search params are parameters after `?` in urls.
use the interface `searchParams` and `setSearchParams` returned by  `useSearchParams` of react-router-dom to access and set them.

注：一般而言，react的同级元素之间的通信要依靠父元素，这种设计思路叫做状态提升。然而，实现同级元素通信也可以有很多其他的办法，比如可以把通信内容放到searchParams里面，另外一个元素可以通过获取这个参数来实现通讯。当searchParams发生改变的时候，元素会自动渲染。这种机制就好像自己本元素的state发生改变一样。

Achieve the **dual binding** between input and searchParams:
```JavaScript
<input
    value={searchParams.get("filter") || ""}
    onChange={(event) => {
    let filter = event.target.value;
    if (filter) {
        setSearchParams({ filter });
    } else {
        setSearchParams({});
    }
    }}
/>
```

### Custom Behavior
#### retain search params
```JavaScript
function QueryNavLink({ to, ...props }) {
  let location = useLocation();
  return <NavLink to={to + location.search} {...props} />;
}
```
`useLocation` returns the information about the URL.



### Navigating Programmatically

