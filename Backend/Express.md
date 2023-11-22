
// one-liner-joke in npm is awesome

# Backend

![image](https://github.com/Aadil-Shaik/Notes/assets/126098463/6b707232-230c-4537-a7bd-8a85187c0ff1)

router, ip, mac, isp

- Load balancing is the method of distributing network traffic equally across a pool of resources that support an application

- http **s** - encrypts all data

- ports are the server end points which are used for communication

#### Nodejs is a runtime environment developed from chrome's v8 engine and a wrapper for js (from c++ in v8)

### import export

```js  
    var a = 123;
    //  This is script2.js
    module.exports = a; 
```

```js
    var num = require('./script2.')
    //  This is script1.js
```

#### To run

```js
    node .\script1.js   //in the terminal
```

### Server

Full fledged example

```js
    npm init -y // to install package.json in a file

    // index.js
    const express = require('express')
    const app = express()
    const port = 3000

    app.get('/', (req, res) => {
    res.send('Hello World!!!')
})

    function calculateSum( target ){
    var sum = 0;
    for( var i = 0 ; i < target ; i++) {
        sum += i;
    }
    return sum;
}

    function handleFirstRequest(req, res){
    var counter = req.query.counter; 
    var calculatedSum = calculateSum(counter);

    var answer = "The Sum is " + calculatedSum;
    res.send(answer);
}

app.get('/handleSum', handleFirstRequest)

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
})

// then in the route give the => url http://localhost:3000/handleSum?counter=100
```

- There are 3 ways to send params. 

1. Query params means parameters in url itself ?param=value&param=value
ideally that means you could do everything with GET handler""  itself but you shouldn't. Also anything sent by GET is stored in browser history

2. in Header ```req.header.counter```

3. in body ; express doesn't give you body parser ```npm install body-parser```

```js 
    var bodyParser = require('body-parser')
    app.use(bodyParser.json()   // This is the middleware

    req.body
```

### Express

- used for routing

- by defaul you are on / route meaning no name route

- uses http available in node behind the scene

- there's a default /all route

#### GET route

- shows the route address in url

#### POST route

- doesn't show the route address in url

#### To run an express server

```js
    const express = require('express')
    const app = express()

    app.get('/', function (req, res) {
      res.send('Hello World')
    })

    app.get('/Profile', function (req, res) {
      res.send('Yo yo Hellow user!')
    })

    app.listen(3000)
    // npm .\script.js
```

To avoid restarting server everytime use nodemon

```npm i nodemon -g``` // to install globally

```nodemon .\script.js``` // to run the server

if doesn't run then ```npx nodemon .\script.js```

### Middleware

- runs before everything else. even the requests sent to the server pass through the middleware first

```js
    app.use( function(req, res, next){
        console.log("This is middleware");
        next();     // once the node is in middleware, it needs next() to push it to next instruction
    } )
```
- you can make any number of middleware

- you can respond only once meaning ```res.send()``` once used in middleware, won't work again even after ```next()```

- can add route specific middlewares

### Route Parameters

```js
    const express = require('express')
    const app = express()

    app.get('/', function (req, res) {
      res.send('Hello World')
    })

    app.get('/Profile/:username', function (req, res) {
      res.send('Yo yo Hellow ${ req.params.username }!')
    })

    //  :username here is wildcard

    app.listen(3000)
    // npm .\script.js
```

### Template engines -> ejs

- ejs is backend html with superpowers

- ejs install => ```npm i ejs```

- configure ejs => ```app.set("view engine", ejs);  //paste in js before any route```

- make a views folder with index.ejs

- instead of .send, write .render & write the name of file inside views folder without .ejs 

```js
    app.get("/", funciton (req, res){
        res.render("index", {age:12} );
    } );    

    // to use the value of age in index.ejs

    <html>
        <h1> age is : <%= age %> </h1>
    </html>
```

### Static files

- images, stylesheets, front-end js

- create a folder named public

- create three folders inside it images, stylesheets, javascripts

- configure the express ```app.use( express.static('./public') )```

move the css into stylesheets/style.css and in index.ejs link it ```link href= "../stylesheets/style.css" //no need to write public folder as its already written in express static```

### Error handling

google it 
