# Search UI: Vue.js Assignment

Vue 3 + Vite search UI which fetches data from a dummy API and allows filtering, expanding results and changing theme.

## Walkthrough

![Project walkthrough](public/walkthrough%20video%20of%20project.gif)

## Running locally

Node 20+ and npm 10+ required.

```sh
npm install
npm run dev
```

## What's in here

- `SearchBar` — Component for search bar
- `App.vue` — All the logic of code is written over here
- `ResultList` & `ResultItem` — ResultList is collection of results and item is used for particular expand/collapse feature
- `Loader` — Shows the loader when its fetching data

Data comes from `dummyjson.com/products`. Each product gets mapped to `{ title, snippet }` to match the expected shape.

## Scaling notes

These are things I'd do if I wanted to scale this:

1. Right now everything is in App.vue which is fine at this size. Once we add more pages or shared state (user preferences, auth, filters) it makes sense to move to Pinia. Keeps components dumb and easy to test.

2. If the result set got large I'd be doing list virtualization (vue-virtual-scroller).

3. If this expanded to multiple pages (search page, result detail page) I'd be adding Vue Router and split into page components.