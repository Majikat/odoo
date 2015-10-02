# Odoo

Node.js client library for Odoo

## Installation

```bash
$ npm install Odoo
```

## Usage

```js
var Odoo = require('Odoo');

var odoo = new Odoo({
  host: 'localhost',
  port: 8069,
  database: 'demo',
  username: 'admin',
  password: 'admin'
});

// Connect to Odoo
odoo.connect(function (err) {
  if (err) { return console.log(err); }
});

// Get a partner
// https://www.odoo.com/documentation/8.0/api_integration.html#read-records
// https://www.odoo.com/documentation/8.0/reference/orm.html#openerp.models.Model.read
var params = {
  ids: [1,2,3,4,5],
  fields: [ 'name' ],
}; //params
odoo.get('res.partner', params, function (err, partners) {
  if (err) { return console.log(err); }

  console.log(partners);
});


// Search & Get products in one RPC call
// https://www.odoo.com/documentation/8.0/api_integration.html#search-and-read
// https://www.odoo.com/documentation/8.0/reference/orm.html#openerp.models.Model.search
// https://www.odoo.com/documentation/8.0/reference/orm.html#openerp.models.Model.read
var params = {
  ids: [1,2,3,4,5],
  domain: [ [ 'list_price', '>', '50' ], [ 'list_price', '<', '65' ] ],
  fields: [ 'name', 'list_price', 'items' ],
  order: 'list_price',
  limit: 5,
  offset: 0,  
}; //params
odoo.get('product.product', params, function (err, products) {
  if (err) { return console.log(err); }

  console.log(products);
});
```

## Methods

* odoo.connect(callback)
* odoo.get(model, id, callback)
* odoo.search(model, params, callback)
* odoo.search_read(model, params, callback)
* odoo.create(model, params, callback)
* odoo.update(model, id, params, callback)
* odoo.delete(model, id, callback)

##Node version
Works better with NodeJS v11.16 and further

## Reference

* [Odoo Technical Documentation](https://www.odoo.com/documentation/8.0)
* [Odoo Web Service API](https://www.odoo.com/documentation/8.0/api_integration.html)

## License

The MIT License (MIT)

Copyright (c) 2015 Marco Godínez, 4yopping and all the related trademarks

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
