[Furtune.js](https://github.com/daliwali/fortune) Example
---------------------------------------------------------

### Resources 
* ```Person```
* ```Pet```

### Relationships
* A ```Person``` can have 0 or more ```Pet```

Code
----

```js
var fortune = require('fortune')
  , app = fortune({
    db: 'petstore'
  })
  .resource('person', {
    name: String,
    age: Number,
    pets: ['pet'] // "has many" relationship to pets
  })
  .resource('pet', {
    name: String,
    age: Number,
    owner: 'person' // "belongs to" relationship to a person
  })
  .listen(1337);
```

Starting the server
-------------------

```
node app.js
```

API
---

### ```Person```

---

NOTE : ```Person``` becomes ```people``` in its plural form. [Fortune.js does it on it's own](https://github.com/daliwali/fortune/blob/master/lib/route.js#L38). If we had a resource called ```Child```, collection would have been refered as ```children```.

#### GET
**Request** - getting them all.
```
curl -X GET http://localhost:1337/people
```

**Reply**
```
{
  "people": [
    {
      "id": "SILtWkM4MQK1n32R",
      "name": "Ram"
    }
  ]
}
```
**Request** - getting an individual person by its id.
```
curl -X GET http://localhost:1337/people/SILtWkM4MQK1n32R
```
**Reply**
```
{
  "people": [
    {
      "id": "SILtWkM4MQK1n32R",
      "name": "Ram"
    }
  ]
}
```
**Request** - getting specific set of individuals by thier ids.
```
curl -X GET 'http://localhost:1337/people?ids=hXuwSO3Q9qTzerjp,qjeSCuNLhdEM7RXZ'
```
**Reply**
```
{
  "people": [
    {
      "id": "hXuwSO3Q9qTzerjp",
      "name": "Laxman"
    },
    {
      "id": "qjeSCuNLhdEM7RXZ",
      "name": "Raju",
      "links": {
        "pets": [
          "T0ozuiz15oGmtD90"
        ]
      }
    }
  ]
}
```
**Request** - getting all pets of an individual person by its id.
```
curl -X GET http://localhost:1337/people/qjeSCuNLhdEM7RXZ/pets
```

**Reply**
```
{
  "pets": [
    {
      "id": "T0ozuiz15oGmtD90",
      "name": "Sherdil",
      "links": {
        "owner": "qjeSCuNLhdEM7RXZ"
      }
    }
  ]
}
```
#### POST
**Request**
```
curl -X POST -H "Content-Type:application/vnd.api+json" -d '{"people":[{"name":"Ram"}]}' http://localhost:1337/people
```

**Reply**

```
{
  "people": [
    {
      "id": "SILtWkM4MQK1n32R",
      "name": "Ram"
    }
  ]
}
```

Some other request you can try.

```
curl -X POST -H "Content-Type:application/vnd.api+json" -d '{"people":[{"name":"Raju","Age":20}]}' http://localhost:1337/people
```

```
curl -X POST -H "Content-Type:application/vnd.api+json" -d '{"people":[{"name":"Raju","Age":20,"pets":["T0ozuiz15oGmtD90"]}]}' http://localhost:1337/people
```


#### PUT

**Request**
```
curl -X PUT -H "Content-Type:application/vnd.api+json" -d '{"people":[{"name":"Ramanujan"}]}' http://localhost:1337/people/SILtWkM4MQK1n32R
```
**Reply**
```
{
  "people": [
    {
      "id": "SILtWkM4MQK1n32R",
      "name": "Ramanujan"
    }
  ]
}
```

##### [PATCH](http://tools.ietf.org/html/rfc6902) 

###### add

**Request**
```

```

**Reply**
```

```

###### remove
 
**Request**
```

```

**Reply**
```

``` 
###### replace
**Request**
```

```

**Reply**
```

``` 
 
###### move
**Request**
```

```

**Reply**
```

``` 
 
###### copy
**Request**
```

```

**Reply**
```

``` 

###### test
**Request**
```

```

**Reply**
```

``` 

##### DELETE
**Request**
```
curl -I -X DELETE http://localhost:1337/people/SILtWkM4MQK1n32R
```

**Reply**
```
HTTP/1.1 204 No Content
Date: Fri, 13 Dec 2013 14:50:23 GMT
Connection: keep-alive
```

### ```Pet```

---

#### GET
**Request** - getting them all.
```
curl -X GET http://localhost:1337/pets
```

**Reply**
```
{
  "pets": [
    {
      "id": "T0ozuiz15oGmtD90",
      "name": "Sherdil"
    }
  ]
}
```

**Request** - getting an individual pet by its id.
```
curl -X GET http://localhost:1337/pets/T0ozuiz15oGmtD90
```

**Reply**
```
{
  "pets": [
    {
      "id": "T0ozuiz15oGmtD90",
      "name": "Sherdil"
    }
  ]
}
```

#### POST
**Request**
```
curl -X POST -H "Content-Type:application/vnd.api+json" -d '{"pets":[{"name":"Sheru"}]}' http://localhost:1337/pets
```

**Reply**

```
{
  "pets": [
    {
      "id": "T0ozuiz15oGmtD90",
      "name": "Sheru"
    }
  ]
}
```

#### PUT

**Request**
```
curl -X PUT -H "Content-Type:application/vnd.api+json" -d '{"pets":[{"name":"Sherdil"}]}' http://localhost:1337/pets/T0ozuiz15oGmtD90
```
**Reply**
```
{
  "pets": [
    {
      "id": "T0ozuiz15oGmtD90",
      "name": "Sherdil"
    }
  ]
}
```

##### [PATCH](http://tools.ietf.org/html/rfc6902) 

###### add

**Request**
```

```

**Reply**
```

```

###### remove
 
**Request**
```

```

**Reply**
```

``` 
###### replace
**Request**
```

```

**Reply**
```

``` 
 
###### move
**Request**
```

```

**Reply**
```

``` 
 
###### copy
**Request**
```

```

**Reply**
```

``` 

###### test
**Request**
```

```

**Reply**
```

``` 

##### DELETE
**Request**
```
curl -I -X DELETE http://localhost:1337/people/SILtWkM4MQK1n32R
```

**Reply**
```
HTTP/1.1 204 No Content
Date: Fri, 13 Dec 2013 14:50:23 GMT
Connection: keep-alive
```