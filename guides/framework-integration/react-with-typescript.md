---
description: 'How to create an Electron app with React, TypeScript, and Electron Forge'
---

# React with TypeScript

Adding React support to the TypeScript + Webpack template is fairly straightforward and doesn't require a complicated boilerplate to get started.

{% hint style="info" %}
The following guide has been tested with React 17, TypeScript 4.3, and Webpack 5.
{% endhint %}

### Create the app and setup the TypeScript config

Create the app with the [TypeScript + Webpack template](../../templates/typescript-+-webpack-template.md), then edit the newly created `tsconfig.json` to add the key-value entry [`"jsx": "react"`](https://www.typescriptlang.org/tsconfig#jsx) to the `"compilerOptions"` section.

### Add the React dependencies

Add the basic React packages to your `dependencies` and the corresponding types to your `devDependencies`:

{% tabs %}
{% tab title="Yarn" %}
```bash
yarn add react react-dom
yarn add --dev @types/react @types/react-dom
```
{% endtab %}

{% tab title="NPM" %}
```bash
npm install --save react react-dom
npm install --save-dev @types/react @types/react-dom
```
{% endtab %}
{% endtabs %}

### Integrate React code

You should now be able to start writing and using React components in your Electron app. The following is a very minimal example of how to start to add React code:

{% tabs %}
{% tab title="src/app.tsx" %}
```tsx
import React, { useState } from 'react';

export const App: React.FC = () => {
  const [clicks, setClicks] = useState(0);

  return (
    <>
      <h1>Hello from React!</h1>
      <button onClick={() => setClicks((clicks) => clicks + 1)}>Click me! {clicks}</button>
    </>
  );
};

```
{% endtab %}

{% tab title="src/renderer.tsx" %}
```typescript
// *** Change the extension to .tsx for JSX to work ***

import React from 'react';
import ReactDOM from 'react-dom';
import { App } from './App';

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.querySelector('#root'),
);

```
{% endtab %}

{% tab title="src/index.html" %}
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Hello World!</title>
  </head>
  <body>
    <div id="root"></div>
  </body>
</html>
```
{% endtab %}

{% tab title="package.json" %}
```js
// Just make this small change, don't delete everything
{
  "config": {
    "forge": {
      "plugins": [
        [
          {
            "renderer": {
              "entryPoints": [
                {
                  "js": "./src/renderer.tsx", // Change this to .tsx for JSX to work
                }
              ]
            }
          }
        ]
      ]
    }
  },
}
```
{% endtab %}
{% endtabs %}

For more about React, see [their documentation](https://reactjs.org/docs/hello-world.html).

