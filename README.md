# jsonapi-datastore

JavaScript client-side [JSON API](http://jsonapi.org) data handling made easy.

Current version is v0.1.0-alpha. It is still a work in progress, but should do what it says.

## Installing

Install jsonapi-datastore by running:
```
$ bower install jsonapi-datastore
```

## Parsing data

Just call the `.sync()` method of your store.
```
var store = new JsonApiDataStore();
store.sync(data);
```
This parses the data and incorporates it in the store, taking care of already existing records (by updating them) and relationships.

## Retrieving models

Just call the `.find(type, id)` method of your store.
```
var article = store.find('article', 123);
```
All the attributes *and* relationships are accessible through the model as object properties.
```
console.log(article.author.name);
```
In case a related resource has not been fetched yet (either as a primary resource or as an included resource), the corresponding property on the model will contain only the `type` and `id` (and the `._placeHolder` property will be set to `true`). However, the models are *updated in place*, so you can fetch a related resource later, and your data will remain consistent.

## Serializing data

Just call the `.serialize()` method on the model.
```
console.log(article.serialize());
```

## Examples

TODO

## What's missing

Currently, the store does not handle `links` and `meta` attributes.

## Notes

### AngularJS

In order to use jsonapi-datastore inside an AngularJS project, simply require the plugin in your `index.html` and then make a factory:
```
angular
  .module('myApp')
  .factory('JsonApiDataStore', function() {
    return new JsonApiDataStore();
  });
```

## Contributing

All pull-requests welcome!
