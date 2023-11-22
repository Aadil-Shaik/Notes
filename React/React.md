
# React js using next js

- By default it is Server side rendering, so to perform any client side actions, you have to explicitly mention "use client" in the code itself

### Starting

```js
    npx create-next-app
```
To run
```js
    npm run dev
```

```js
    import React from 'react'

const page = () => {
    return(
        <div>Hello</div>
    )
}

export default page
```

using variables

```js
    import React from 'react'

    const page = () => {
        const name = "Kat"
            const apple = 5
        return(
            <h1>{name} has {apple} apples</h1>
        )
    }

    export default page
```

using fragments as wrappers

```js
    import React from 'react'

    const page = () => {
        const name = "Kat"
        const apple = 5
        return(
            <>
            <h1>{name} has {apple} apples</h1>
            </>
        )
    }

    export default page
```

## Real DOM vs Virtual DOM

- Real DOM considers everything in the form of a tree. The root being window then HTML then head, body and so on

- So, when updating an element far down the line, the whole DOM tree is changed. In real time that means, the whole page needs to reload again. That also mean the existing elements loose their properties upon rerender. (loosing typing input in the input box or already changed styles)

- Virtual DOM is a copy of real DOM. This DOM updates the UI according to the requirement and then compares the changes to the real DOM then updates only the specific element in the real DOM resulting in no loss in the other states of the real DOM

- This change is made using prepend and append operaions

#### using css

```js
    import React from 'react'

    const page = () => {
        return(
            <>
            <div className= 'font-bold text-xl text-red-500'> Hello </div>
            </>
        )
    }

    export default page
```

#### using variables

```js
    "use client"
    import React, { useState } from 'react'

    const page = () => {
        const [marks, setMarks] = useState(80)
        return(
            <>
            <div className= 'font-bold text-xl '> Hello, I scored {marks} </div>
            <button onClick={()=>{
                setMarks(33)
            }}>Update</button>    
            </>
        )
    }

    export default page
```

#### passing variables as props 

```js
"use client"
import React, { useState } from 'react'
import Header from "@/Components/Header";

    const page = () => {
        const [user, setUser] = useState("Aadil")
        return(
            <>
            <Header user={user} var = {varName}/>
            </>
        )
    }

    export default page

------------------------------------------------------------------

"use client"
import React from "react";

const Header = (props) => {
    return (
        <>
        <h1 className="text">This is Header!</h1>
        The name's {props.user} //user:Aadil (object)
        </>
    )
}

export default Header
```

### Routing in react

- create a folder for the next page in the app itself

```js
"use client"
import React from 'react'
import Link from 'next/link'

    const page = () => {
        return(
            <>
            <Link href="/About">About</Link> 
            </>
        )
    }

export default page 
```

- to avoid reloading other components that don't change like Header, just put it in the layout

```js
import Header from '@/Components/Header'
import { Inter } from 'next/font/google'
import './globals.css'

export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body>
      <Header/>
        {children}</body>
    </html>
  )
}
```

## Axios

- npm i axios 

```js
"use client"
import axios from "axios";
import React, { useState } from "react";

const Pictures = () => {
    const [Images, setImages] = useState([]);
    const getImages = async () => {
        try {
            const response = await axios.get("https://picsum.photos/v2/list");
            const data = response.data;
            setImages(data);
            console.log(Images);
        } catch (error) {
            console.error("Didn't get any response yet");
        }
    }
    return (
        <>
        <button onClick={getImages} className="m-5 px-3 py-5 bg-green-800 text-white font-bold">Pictures Summon!</button>

        <div className="p-10">
            {Images.map((elem,i)=>{
                return <div className ="inline-block">
                <h1 key={i}>{elem.author}</h1>
                <img key={i}
                src = {elem.download_url}
                width={300}
                height={300}
                className = "m-10 rounded"
                />
                </div>
            }     
            )}
        </div>
        </>
    )
}

export default Pictures
```

### 2 way binding

I did not understand this yet

```js
    "use client"
import React, { useState } from 'react'

const page = () => {
  const [uname, setUname] = useState("")
  return(
    <>
    <form className='flex gap-6 items-center p-10'>
    <h1 className="text-2xl">Enter your name: </h1>
    <input type="text" className="border-purple-500 border-4 px-2 py-2 text-xl text-black rounded"
    placeholder='Enter username'
    value = {uname}
    onChange = {(e) => {
      // console.log(e.target.value)
      setUname(e.target.value)
      // console.log(uname)
    }}
    />
    </form>

    </>
  )
}

export default page
```

## App Routing/ Dynamic Routing

- Json placeholder API (axios => npm i axios)

#### useEffect

to do a task without any sideeffects like fetching data or updating DOM directly and immediately

```js
    useEffect(()=>{
    // function up here
    }, [])

```

- create a folder with the name [id]

```js
    "use client"
import axios from 'axios'
import Link from 'next/link'
import React, { useState } from 'react'

const page = () => {
  const [users,setUsers] = useState([])
  const getUsers = async () => {
      const {data} = await axios.get("https://jsonplaceholder.typicode.com/users");
      console.log(data)
      setUsers(data)
  }

  return(
    <>
    <div className='text-5xl'>Home here</div>
   
    <button onClick={getUsers} className='block p-4 bg-slate-700 rounded my-4 mx-4'>Get User Data</button>

    <div className='p-4 bg-slate-900'>
      <ul>
        {users.map((e) => {
          return <li>{e.username} {"-->"} <Link href= {`${e.id}`} > {e.username}{"'s contact"}</Link> </li>
        })}
      </ul>
    </div>
    </>
  )
}

export default page
```

in page of [id] folder

```js
    "use client"
import axios from 'axios'
import React, { useEffect, useState } from 'react'

const page = ( {params} ) => {
    const {id} = params
    const [users,setUsers] = useState([])
    const getUsers = async () => {
      const {data} = await axios.get("https://jsonplaceholder.typicode.com/users/"+id);
      setUsers(data)
      console.log(data.username)
  }

  useEffect(()=>{
    getUsers()
  }, [])

    return (
        <>
        {JSON.stringify(users)}
        </>
    )
}

export default page
```

# Contect API   !!! (pending)

- used to share information among the children componens directly

- used in a small application (about 200 components)

- in a bigger application, Redux toolkit is used which is not part of react

### Toastify

- pop up library

```js 
    npm install --save react-toastify
```

- then import

## Deploying in render

- build command you can change to `npm run build`
