# <font color="#000000">🟠🔵 SetUp & Configuartion</font>

## 🔶 - <span style="background:#d4b106"><font color="#ffffff">SetUp - (back-end)</font></span>


### 1️⃣ Rest Apis + ExpressJS + MongoDB 

---

#### Connection with MongoDB Atlas

`1) Configuration `
- Connexion in mongoDB Atlas
- Choose Free for deploy
- Choose name username
- put IP Adress 

--

`2) Connection to app `
-  Choose Connectio with MongoDB Drivers
- Copy the url inside folder .env
```js
EX_DATABASE_URL = mongodb+srv: <usernameFromMongo>:Apvlhke6kfvHwZXc@cluster0.xxd4h.mongodb.net/<databaseName>?retryWrites=true&w=majority&appName=Cluster0

```
- in MongoDbAtlas -> browser Collection -> create Collection -> put the same name of database in your .env

---

#### Structure Folder

- config
    - db.js
    - envVars (all variable from .env)
- middleware
    - auth.js
    - createToken.js
- router
    - userRouter
    - categoryRouter
- contollers
    - userController
    - categotyController
- models
    - userModels
    - categoryModels
- index.js
- .env

---
#### 💻 VS Code


- 🧩 **in index.js** & **npm**

```js

1️⃣ import express from 'express'

import connectDB from ''
2️⃣ import morgan from ''
import coookieParser from ''


const express = app


app.use(morgan())

3️⃣ app.use(express.json())
4️⃣ app.use(express.urlencoded({ extended : true }))
5️⃣ app.use(cookieParser())

const port = VAR.port || 5500

connectDB()

app.listen(port, ()=>console.log(`server is running on port ${port}`))
```

--

1️⃣ `import express`
-  📔 Ressource
    - 📖 [Official Documentation Express](https://redux-toolkit.js.org/rtk-query/usage/cache-behavior)
- package.json add { type : module }

--

2️⃣ - `morgan`
    
-  📔 Ressource
    - 📖 [Dev.io](https://dev.to/devland/how-to-use-morgan-in-your-nodejs-project-21im#:~:text=Morgan%20is%20a%20logging%20tool,and%20more%20to%20the%20console.)
-  allows flexibility when logging HTTP requests and updates precise status and response time in custom format strings.
    For log HTTP requests and errors, and don't want to write extra configuration codes, Morgan is the best option.

--

3️⃣ - `app.use(express.json())`


```js

import express from "express";
const app = express();

 app.use(express.json());

const port = process.env.PORT || 5500;

app.post("/login", (req, res)=>{

    // Without `express.json()`, `req.body` is undefined.
    console.log(req.body);
})


app.listen(port, ()=>console.log(`server is running on port ${port}`))
```

--

4️⃣ `app.use(express.urlencoded({ extend : true }))`

- 📔 Ressource
    - 🎥 [Great Indian Education - 13min - Ytb](https://www.youtube.com/watch?v=5dZNWL4sEGo)

- Whenever we are sending for example an information from a form the data from the client to the server it will send in the form of URL encoded format through that request
- But server can't understand that uRL encoded format by default
- So we use this now it will create an object and it will send it to the server , so if the server want understand this format we should pass that URL encoded format right into a json format

<font color="#9bbb59">example before</font>

```js
import express from "express";
const app = express();


connectDB();

dotenv.config();
const port = process.env.PORT || 5500;

app.get("/login", (req, res)=>{

    res.send("<form action='/login' method='POST'><input type='text' name='username'><input type='password' name='password'><input type='submit'></form>")
})

app.post("/login", (req, res)=>{

    res.send("Yes this is an user")
    console.log(req.body);
})


app.listen(port, ()=>console.log(`server is running on port ${port}`))

```

- In my browser when I enter username "Moli" , password "1234" the information and submit
- My browser display "Yes this is an user"
- In console/reséau/login/en-tête/ content-type : application/x-www-form-urlencoded


🧩`terminal` file
```terminal
undefined
```

 <font color="#9bbb59">example after</font>

```js
import express from "express";
const app = express();

👀 app.use(express.urlencoded({extends : true})); 👀

connectDB();

dotenv.config();
const port = process.env.PORT || 5500;

app.get("/login", (req, res)=>{

    res.send("<form action='/login' method='POST'><input type='text' name='username'><input type='password' name='password'><input type='submit'></form>")
})

app.post("/login", (req, res)=>{

    res.send("Yes this is an user")
    console.log(req.body);
})


app.listen(port, ()=>console.log(`server is running on port ${port}`))

```

- In my browser when I enter username "Moli" , password "1234" the information and submit
- My browser display "Yes this is an user"

🧩`terminal` file
```terminal
{ username: 'MOLI', password: '1234' }
```

--

5️⃣ - `app.use(cookieParser())`
    
    - cookie-parser middleware is used to parse cookies in Node.js applications.

--


6️⃣ `npm asyncHandler`


- asyncHandler is likely a middleware that wraps your route handler to catch any errors thrown inside it
- It relies on the asyncHandler to catch any errors thrown within the function.
- Instead of using return statements with res.status().json(), it sets the status code separately and then throws an error.
- The asyncHandler is expected to catch these errors and send appropriate responses.
- It still performs all the necessary checks and operations as the previous version.
- It adds a check to ensure the user was actually created before sending a success response.


- This approach can make the code more linear and easier to follow in some cases, as it doesn't have the nested structure of a try-catch block. However, it does require that the asyncHandler is properly set up to handle errors and send appropriate responses.

`difference vs res.status(400).json({ error.message : "ppapa"})`

- With throw new Error(), you're relying on the asyncHandler to send the response.
- With res.status().json(), you're sending the response directly.
- The throw approach can be more consistent if you're using asyncHandler throughout your application.

6️⃣ `npm bcrypt`

- for hash the password

7️⃣ `npm dotenv`


- express `process.env.NODE_ENV
    - this varibale is an convention it will either 'developpmenent' when we create the app or 'production' when the app is deployed

- `.env`
    - this is a convetion folder the store all the sensible variable in our project
- `dotenv.config()`
    - grap all the environnement variable and place into 'process.env' , without dotenv.config() server cannot access to the varibale in the folder .env

9️⃣ `npm nodemon`

- for the server run automatically without you need to always run the command 'node/sever.js'

8️⃣ `npm concurrently`

- for run at the same time the server and the client folder

🔟 `npm express-formidable`

- For hanlde the request from the form in the front-end

--



---




## 🔷 - <span style="background:#40a9ff"><font color="#ffffff">Set-Up (front-end )</font></span>


---

### 1️⃣ RTQ Query

#### Configuration

🧩 `terminal`

[Documentation](https://tailwindcss.com/docs/guides/vite)


- npm i create latest@vite
- installtion react + tailwind CSS 

🧩 `in vite.config`

```js

export default defineConfig({


server : {


        proxy : {

            '/api' : 'http:localhost:5500'
        }
    },

resolve: {
  alias: {
    '@': '/src',
  },
}

})

```


--

##### package

##### 💻 VS Code

- **Structure folder**

    - src
        - redux
            - Features.jsx
                - authSlice.jsx
                - favoriteSlice.jsx
            - Api.jsx
                - apiSlice.jsx
                - apiSliceUser.jsx
                - apiSliceCategory.jsx
                - apiSliceProduct.jsx
            - Store.jsx
            - Constant.jsx

--



`🧩 in constant`

```js

// Folder for store the url that we using in the app

// we store the base Url directly in the vite.config
export const BASE_URL = ''

export const USER_URL = `/api/user`
export const CATEGORY_URL = `/api/categories`

```



--

`🧩 in apiSlice.jsx`

```js

import { createApi , fetchBaseQuery} from '@reduxjs/toolkit/query/react'
import { BASE_URL } from '../constants'


// We use the method fetchBaseQuery by redux toolkit query for 
const baseQuery = fetchBaseQuery({ baseUrl : "" })


// create Api for configuration and create APi for the app
export const apiSlice = createApi({


    // base query is already create we use ES6 syntax
    baseQuery,

    // For cahing and invalidate data for the future
    tagTypes : ['Product', 'User', 'Category'],
    
    // For cahing and invalidate data for the future
    endpoints : ()=>({})

})

```

-- 

`🧩 in store.jsx`

```jsx


import { apiSlice } from ''
import { configureStore } from 'redux'


const store = store.configureStore({

    // The reducers here is for all features that I will create and automatically integrate in my store by seting into reducers
    reducers : {

        // I add apiSlice.reducers for integrate RTQ Queryn store management to my store
       1️⃣ api : apiSlice.reducers
    },


    // we add the middleware to apiSlice because without we cannot use caching, fetching, invalidateTag, provideTags
    middleware : getDefaultMiddleware().concat(apiSlice.middleware),

    devTools : true,


    // Provide the data up to date 
    setupListeners(store.dispatch)


})

```


1️⃣

- apiSlice.reducer is automatically generated by Redux Toolkit's createApi function, which you used to create your apiSlice. Its purpose is to:
Manage the state for all API requests made through RTK Query.
Handle caching of API responses.
Track loading states for requests.
Store any errors that occur during API calls.
By including apiSlice.reducer in your root reducer, you're integrating RTK Query's state management into your Redux store. This allows RTK Query to:
Automatically update your store with API response data.
Provide hooks (like useQuery and useMutation) that you can use in your components to easily interact with your API and access the stored data.

e.g

```jsx

import { useGetUsersQuery } from './apiSlice'

function UserList() {
  const { data: users, isLoading, isError } = useGetUsersQuery()

  if (isLoading) return <div>Loading...</div>
  if (isError) return <div>Error fetching users</div>

  return (
    <ul>
      {users.map(user => <li key={user.id}>{user.name}</li>)}
    </ul>
  )
}

```

- In this example, useGetUsersQuery is a hook automatically generated by RTK Query. It will:

    Trigger the API call when the component mounts.
Update the Redux store with the response data.
Provide loading and error states.
Automatically re-render the component when the data changes.

    All of this is possible because you included apiSlice.reducer in your store configuration.

--


`🧩 in main.jsx`


```jsx


import { store } from ''
import { Provider } from


<Provider store={store}>

<RouterProvider router={router}>

</Provider>

```

- We are using the react-routerv6 



---
##### <font color="#ffc000">❗️ - Remark & Interview Question</font>

------------------------------ **`Related SetUp Configuration  `** ----------------------------------

**Question 1** 

- Why set the Base Url from the server in the proxy and set a empty string into the constant ?


`good answers` ✅

- The proxy configuration in vite.config.js serves a different purpose than the BASE_URL in your constants file. Here's why:

- Development vs. Production: The proxy in vite.config.js is primarily used during development. It allows your frontend to make requests to your backend server without running into CORS issues when they're on different ports or domains.
- Simplifying API calls: By setting up the proxy, you can make API calls to "/api" in your frontend code, and Vite will automatically forward these requests to your backend server (in this case, http://localhost:5500).
- Environment independence: Keeping the BASE_URL empty in your constants file allows your app to work in different environments (development, staging, production) without changing the code. The actual base URL is determined by where your app is deployed.



--

**Question 2** 

- What's the advantage and cons to write this in the createApi ?

```js

import { BASE_URL } from '../constants'

// 1️⃣ this 
const baseQuery = fetchBaseQuery({ baseUrl: '' })

// 2️⃣ instead this
const baseQuery = fetchBaseQuery({ baseUrl: BASE_URL })

```

`good answers` ✅

- the 2 syntax are correct

1️⃣ 

-  BASE_URL is an empty string ("") and you're using a proxy in development, your API calls will work correctly in both development and production environments:

- In development: The empty BASE_URL combined with the Vite proxy will route requests to your local backend.
In production: You would typically set BASE_URL to your actual API URL before building the app for production.

- This setup provides flexibility and ease of configuration across different environments.

2️⃣

- By using BASE_URL, you ensure consistency across your application. If you need to change the base URL in the future, you only need to update it in one place (the constants file)


----------------------------- **`Related Redux Store `** ---------------------------------

**Question 1** 

- Why add the redux toolkit query middleware in the store ?


`good answers` ✅

What's Middleware in Redux ?
- Middleware in Redux provides a third-party extension point between dispatching an action and the moment it reaches the reducer. It allows you to add custom functionality to Redux.

--

`Advantage to add the middleware` ?

2️⃣ Automatic Refetching

2️⃣ Polling

3️⃣ Cache invalidation (ProvideTags, InvalidateTags)

- Without middleware the tags woyld be define but not functionnal
- Cache invalidation wouldn't occurs automatically
- Refetching based on tag invalidtion wouldn't happen

4️⃣ Response Lifecycle Management


`What the middleware does in RTQ Query ?`

- It intercepts actions dispatched by RTK Query.
- When a mutation with invalidatesTags is successful, the middleware triggers refetching of any queries that provide the invalidated tags.
- It manages the cache lifecycle, deciding when to refetch data based on tag invalidations.



--

**Question 2** 

- Blabla ?

```js

// Code

```

`good answers` ✅

1️⃣ `extract`
- blablabla


---

##### <font color="#c00000">❎ - Handle Error || Fix bug</font>

------------------------------ **`Related to Configuration`** ---------------------------------


**bug /error 1** : <u>[plugin:vite:import-analysis] failed to resolve import "../../redux/api/productApiSlice" from "src/components/Home.jsx". Does the file exist ? </u>


- `Scenario`
    - Sometimes I write the good import and path in react but I still have this warning


🧩 **in  compoenent**

```js

// Code Before
import { useAllProductsQuery } from 'src/redux/api/productApiSlice';

```

--

- `Problem 🤔`
    - In this line there is an error

--

- `Solution ✅` ?



🧩 **in vite.config**

```js

resolve: {
  alias: {
    '@': '/src',
  },
}

```

🧩 **in component**

```js

import { useAllProductsQuery } from '@/redux/api/productApiSlice';
```
