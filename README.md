## Employee Directory

### Create App Boilerplate
Delete _client_ and _server_ folder. Create new _client_ folder.
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

### Create MongoDB Collections
Create _imports_ folder. Under _imports_ folder create _collections_ folder.
Under _collections_ folder, create **employee.jsx** :
```js
// Declare our collection
import { Mongo } from 'meteor/mongo';

const Employees = new Mongo.Collection('employees');

export default Employees;
```

### Generating data with Faker
Install faker and lodash :
```bash
npm install --save faker lodash
```
Create _server_ folder. Under _server_ folder create **main.jsx** :
```js
// Only executed on the server
import _ from 'lodash';
import { Meteor } from 'meteor/meteor';
import { Employees } from '../imports/collections/employee';
import { image, helpers } from 'faker';

Meteor.startup(() => {
    // Great place to generate data

    // Check to see if data exists in the collection
    // See if the collection has any records
    const numberRecords = Employees.find({}).count();
    if (!numberRecords) {
        // Generate some data...
        _.times(5000, () => {
            const { name, email, phone } = helpers.createCard();

            Employees.insert({
                name, email, phone,
                avatar: image.avatar()
            });
        });
    }
});
```