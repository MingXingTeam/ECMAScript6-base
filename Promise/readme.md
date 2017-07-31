# Promise

Promise is a async program solution, it is a contructor.It has three status: Pending, Resolved, Rejected.

### base demo 1

```javascript

var _promise = new Promise(function(resolve, reject) {
    if(/* finish async operation */) {
        resolve(value);//The params will be passed to callback func
    } else {
        reject(error);
    }
});

_promise.then(function(value) {
    //success
}, function(err) {//This error func is option
    //failure
});



```

### base demo 2

The param of resolve func can be a Promise object. 


```javascript

var p1 = new Promise(function (resolve, reject) {
  setTimeout(() => reject(new Error('fail')), 3000)
});

var p2 = new Promise(function (resolve, reject) {
  setTimeout(() => resolve(p1), 1000)
});

p2.then(result => console.log(result))
  .catch(error => console.log(error))
  
//output=> Error: fail

```

p1's status will passed to p2. 

### base demo 3

invoking resolve and reject func will not end Promise's param func to run continue program lines.

for example:
```javascript
new Promise((resolve, reject) => {
  resolve(1);
  console.log(2);
}).then(r => {
  console.log(r);
});

//output: 
//2
//1
```

**better write**

```javascript
new Promise((resolve,reject) => {
    return resolve(1);//return directly
});
```

### advanced demo 1

then func's return is a Promise object. so we can use chain invoke.

```javascript
getJSON("/posts.json").then(function(json) {
  return json.post;//result will passed to next then func
}).then(function(post) {
  // ...
});
```

###  advanced demo 2

catch func will be invoked when error happend.

```javascript
getJSON('/posts.json').then(function(posts) {
  // ...
}).catch(function(error) {
  console.log('error happend！', error);
});
```

**better write**

using catch func, not error callback way.

```javascript
// bad
promise
  .then(function(data) {
    // success
  }, function(err) {
    // error
  });

// good
promise
  .then(function(data) { //cb
    // success
  })
  .catch(function(err) {
    // error
  });
```

