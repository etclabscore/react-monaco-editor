# React Monaco Editor

Monaco Editor Wrapper for integration with react + webpack. Based on [SurenAt93/monaco-react/](https://github.com/SurenAt93/monaco-react/) but does not load from a CDN. It loads monaco via `monaco-editor-webpack-plugin` and gives installation instructions for a new or existing project via `rescripts`.


## Setup in a new create-react-app project

### 1. Install deps

```
npm install @etclabscore/react-monaco-editor --save
```

```sh
npm install @rescripts/cli @rescripts/utilities --save-dev
```

```sh
npm install monaco-editor-webpack-plugin --save-dev
```

### 2. Replace `react-scripts` calls with `rescripts` calls

`package.json`

```diff
{
  "name": "built-with-rescripts",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "react": "^16.6.1",
    "react-dom": "^16.6.1",
    "react-scripts": "2.1.1"
  }
  "devDependencies": {
    "@rescripts/cli": "^0.0.11",
    "@rescripts/rescript-env": "^0.0.10"
  }
  "scripts": {
-   "start": "react-scripts start",
+   "start": "rescripts start",
-   "build": "react-scripts build",
+   "build": "rescripts build",
-   "test": "react-scripts test",
+   "test": "rescripts test",
-   "eject": "react-scripts eject"
  },
  "eslintConfig": {
    "extends": "react-app"
  },
  "browserslist": [
    ">0.2%",
    "not dead",
    "not ie <= 11",
    "not op_mini all"
  ]
}
```


### 3. Add new file called in root of your project called rescript-monaco.js

```js
const MonacoWebpackPlugin = require('monaco-editor-webpack-plugin');
const { prependWebpackPlugin } = require("@rescripts/utilities");

module.exports = function override(config, env) {
  return prependWebpackPlugin(new MonacoWebpackPlugin({
    // available options are documented at https://github.com/Microsoft/monaco-editor-webpack-plugin#options
    languages: ["json"]
  }), config);
}
```

### 4. Define a 'rescripts' field and specify the rescript-monaco.js

`package.json`

```diff
{
  "name": "built-with-rescripts",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "react": "^16.6.1",
    "react-dom": "^16.6.1",
    "react-scripts": "2.1.1"
  }
  "devDependencies": {
    "@rescripts/cli": "^0.1.0"
  }
  "scripts": {
    "start": "rescripts start",
    "build": "rescripts build",
    "test": "rescripts test"
  },
  "eslintConfig": {
    "extends": "react-app"
  },
  "browserslist": [
    ">0.2%",
    "not dead",
    "not ie <= 11",
    "not op_mini all"
  ],
+ "rescripts": [
+   "rescript-monaco"
+ ]
}
```


### 5. Use the component:

```js
import MonacoEditor from "@etclabscore/react-monaco-editor";

const MyComponent = ({value}) => {
  const handleEditorDidMount = (editor) => {

  }
  const handleChange = (ev, value) => {

  }
  return (
    <MonacoEditor
      height="100vh"
      value={value}
      editorDidMount={handleEditorDidMount}
      language="json"
      onChange={handleChange}
    />
  );
}
```

### Contributing

How to contribute, build and release are outlined in [CONTRIBUTING.md](CONTRIBUTING.md), [BUILDING.md](BUILDING.md) and [RELEASING.md](RELEASING.md) respectively. Commits in this repository follow the [CONVENTIONAL_COMMITS.md](CONVENTIONAL_COMMITS.md) specification.
