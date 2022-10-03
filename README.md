# movie-search

This template should help get you started developing with Vue 3 in Vite.

## Project Setup

```sh
npm install
```

Create src/env.js file and add your API_KEY
```js
export default {
  API_URL: "https://www.omdbapi.com/?",
  API_KEY: "",
};
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```

### Run Unit Tests with [Vitest](https://vitest.dev/)

```sh
npm run test:unit
```

### Run End-to-End Tests with [Cypress](https://www.cypress.io/)

```sh
npm run build
npm run test:e2e # or `npm run test:e2e:ci` for headless testing
```

### Lint with [ESLint](https://eslint.org/)

```sh
npm run lint
```
