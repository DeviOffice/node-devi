# node-devi
A node.js wrapper for the Devi API

Credit to Daniel Leinich (gomfunkel) which this API is based on
Daniel has no affiliation with Devi nor any of the changes Devi has made to their original code
https://github.com/gomfunkel/node-mailchimp

Further information on the Devi API can be found at http://apidocs.devi.io/

## Table of Contents

 * [Installation](#installation)
 * [Usage](#usage)
   * [Devi API](#devi-api)
 * [License](#license)

## Installation

    cd ~/.node_libraries
    git clone git://github.com/devioffice/node-devi.git devi

Please note that parts of _node-devi_ depend on [request](http://github.com/mikeal/request) by [Mikeal Rogers](http://github.com/mikeal). This library needs to be installed for the API and Export API to work. If you are using npm all dependencies should be automagically resolved for you.

## Usage

Information on how to use the Devi APIs can be found below. Further information on the API methods available can be found at [http://apidocs.devi.io](http://apidocs.devi.io). You can also find further information on how to obtain an API key.

### Devi API

_DeviAPI_ takes three arguments. The first argument is your sub domain, second is your API key, which you can find in your Devi Account. The third argument is an options object which can contain the following options:

 * `version` The Devi API version to use, currently only 1.0 is available and supported. Defaults to 1.0.
 * `secure` Whether or not to use secure connections over HTTPS (true/false). Defaults to false.
 * `userAgent` Custom User-Agent description to use in the request header.

All of the API categories and actions described in the Devi API Documentation ([http://apidocs.devi.io](http://apidocs.devi.io)) are available in this wrapper. To use the the method `call` is used which takes four parameters:

 * `category` The category of the API method to call (e.g. 'employees').
 * `action` The action to call in the given category.
 * `params` Parameters to pass to the API action.
 * `callback` Callback function for returned data or errors with two parameters. The first one being an error object which is null when no error occured, the second one an object with all information retrieved as long as no error occured.

```javascript
var DeviAPI = require('devi').DeviAPI;

var subDomain = 'Your Devi API Key';
var apiKey = 'Your Devi API Key';

try {
    var devi = new DeviAPI(subDomain, apiKey, { version : '1.0', secure: false });
} catch (error) {
    console.log(error.message);
}

devi.call('employees', 'list', {  }, function (error, data) {
    if (error)
        console.log(error.message);
    else
        console.log(JSON.stringify(data)); // Do something with your data!
});
```