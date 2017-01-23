## Create Employee Directory

### App Boilerplate
Delete _client_ and _server_ folder.
Create _client_ folder.
Under _client_ folder, create **main.html** :
```html
<head>
    <title>Employee Directory</title>
</head>

<body>
    <div class="container"></div>
</body>
```
Create **main.jsx** :
```js
import React from 'react';
import ReactDOM from 'react-dom';

const App = () => {
    return (
        <div>Hello there!</div>
    );
};

// After Meteor loads in the browser, render my app to the browser
Meteor.startup(() => {
    // React render call
    ReactDOM.render(<App />, document.querySelector('.container'));
});
```