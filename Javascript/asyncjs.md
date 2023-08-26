## Asynchronous Javascript

These send request

- setTimeout
- setInterval
- promises
- fetch 
- axios
- XMLHttpRequest - Ajax call to server to retrieve data which is to be retrieved to display on DOM

These catch the response

- then catch
- call backs
- async await

## callback function

```js
    setTimeout(function(){
        console.log(" This ran after 2 seconds ") ;
    }, 2000 ) ;  
```

- only after completion of the main stack codes, is the side stack code executed ! meaning giving 0 timeout will still make it execute last
- even loop is responsible for info transfer between main and side stack 

## fetch

fetch('url')

```js
var ans = new Promise((res,rej)=>{
    var n = Math.floor(Math.random()*10);

    if(n<5){
        return res();
    }
    else{
        return rej();
    }
})

ans.then(function(){
    console.log("below");
})
.catch(function(){
    console.log("above");
})
```
#### promise chain
```js
var promise1 = new Promise(function(res, rej){
    return res("Completed Task 1")
})

var promise2 = promise1.then(function(data){
    console.log(data);
    return new Promise(function(res, rej){      //saved in promise2 variable
        return res("Completed Task 2")
    })
})

promise2.then(function(data){
    console.log(data);
```

## async await

without async await

```js
function abcd(){
fetch('https://randomuser.me/api/')
    .then( function(raw){
        return raw.json();
    } )
    .then( function(data){
        console.log(data);
    } );
}

abcd();
```
with async await

```js
async function abcd(){
let raw = await fetch('https://randomuser.me/api/')
    let data = await raw.json();
    console.log(data);
}

abcd();
```

### concurrency
both async (side stack) and sync (mian stack) code are concurrently being executed in js
### parallelism
the ability to run different tasks on different cores of the system
### throttling 
controlling the no. of snaps of the activity

e.g. time interval between each snap of mouse scroll 20ms
