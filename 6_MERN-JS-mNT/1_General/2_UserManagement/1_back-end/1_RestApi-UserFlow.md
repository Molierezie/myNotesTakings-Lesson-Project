

# <font color="#000000">⚫️ UserFlow REST API</font>

## 🔶 - <span style="background:#d4b106"><font color="#ffffff">Register / Login / Logout</font></span>



### 1️⃣ NodeJS - ExpressJS - MongoDB

#### 💻 VS Code

🧩 **in models.js**

```js

import mongoose from ''


// we use the destructuring for more readabale code
const { schema } = mongoose

const userSchema = new schema({

    username : { type : String, required : true},
    email : { type : String, required : true},
    password : { type : String, minLength : 4, maxLength : 20,  required : true},
},

// timestamps for have the date of creation and uopdate for each documents
{ timestamps : true }
)

  // with this method we create a new collection
const User = mongoose.model('Users', userSchema)

export default User

```


--


🧩 **in userRouter**

```js


import { registerUser, loginUser, logoutUser } from '...controller.js'

// We use the method post because we

router.post('register', registerUser)
router.post('login', loginUser)
router.post('logout', logoutUser )

```

--


🧩 **in controller.js**


```js

import express from express
import User from 'userModel..'
import bcrypt from 'bcrypt'
import { createToken } from ''


// ------------------------------------------------------------------ //
// ---------------------------- REGISTER ---------------------------- //
// ------------------------------------------------------------------ //

export const Register = asyncHanlder(

        async(req,res)=>{
            

        try{

        // We extract the data in the front with req.body 
        const { username, email, password } = req.body


        // We verify if the user enter in the input his email and password
        if(!username || !email ){

            res.status(400)
            throw new Error('A username and email is required')
        }



        const user = await User.findOne({ email })

        // We check if the email already exist in the database or not
        if(user){

            res.status(400)
            throw new Error('This email is already taken please choice another')

        }

         // If the email doesn't exist we hash the password with bcrypt method
        const hashPassword = await bcrypt.hashSync(password, 10)
        

        // as we using destructuring we don't need to write to this way
        //  const newUser = new User({
        //  username (in db) :  username,
        // })
        // we use the method from mongoose for create a new document
        const newUser = new User({

            username,
            email,
            hashPassword
        })


         // we register the new user in the database with the method .save()
        newUser.save()


        // We add the new user in the token
        createToken(res, newUser._id)


         // we create a new variable espacially for using the data in the front-end for the user UI with the method .select
         // another way
         // const displayFront = await User.find(newUser, 'username')

        const displayFront = await User.find(newUser).select('username')

        // we send a status code '200' and the message for the user
        res.status(200).json(`Welcome ${displayFront}`)


    
        }catch(error){


            // the object throw new Error catch all the error and display here
            res.statut(400)
            throw new Error(`An error occurs : ${error.message}`)
        }

     
    }
)


// ------------------------------------------------------------------ //
// ------------------------------- LOGIN ---------------------------- //
// ------------------------------------------------------------------ //

export const LoginUser = asyncHandler(


    async(req, res)=>{


        try{
            
            // we retrieves the data from the front-end using destructuring
            const { email, password } = req.body
    
            // we check if the user enter well his email and password
            if(!email || !password){
    
                res.status(400)
                throw new Error('An email and password is required')
            }
    
            const user = await User.findOne({ email })
    
            if(!user){
                res.status(400)
                throw new Error('Email not existing is wrong try again')
            }
    
    
            const passwordCompare = bcrypt.compare(user.password, password)
    
            if(!passwordCompare){
                res.status(400)
                throw new Error('Password is wrong try again')
            }
    
            res.status(200).json(`Welcome ${user.username}`)
    
            createToken(res, user._id)



        }catch(err){

            res.status(400)
            throw new Error(`An errors occurs : ${error}`)
        }


    }
)


// ------------------------------------------------------------------ //
// ------------------------------- LOGOUT ---------------------------- //
// ------------------------------------------------------------------ //



export const logoutUser = asyncHandler(

    async(req, res)=>{


        try{
        
        // we check if there are a cookie store in the header
        if(res.Cookies.jwt){

            // method for delete the cookie in the localStorage
            res.clearCookie()
            res.status(200).json('Deconnexion')

        }else{

            res.status(400)
            throw new Error()
        }

        }catch(error){

            res.status(400)
            throw new Error('')
        }
    }
)


```


--

- 🧩 **in file**

#### Diagram - Analogy

[👀 Link - Diagram User Flow 👀 ](https://drive.google.com/file/d/1uAHjB1g-SPyq7ly40vTXwl_V5MLpe269/view?usp=sharing)



#### <font color="#ffc000">❗️ - Remark & Interview Question</font>

---------------------------------- **`Related To Register`** -----------------------------------

**Question 1** 

- Why the most blabla ?

```js

// Code


1️⃣ testArr.add(1)

```

`good answers` ✅

1️⃣ `extract`
- blablabla

--

---

#### <font color="#c00000">❎ - Handle Error || Fix bug</font>

------------------------------ **`Related To Topic 1`** ---------------------------------


**bug /error 1** : blablabla

- `Scenario`
    - ex : Imagine you want to building an interface etc...

```js

// Code

```

--

- `Problem 🤔`
    - In this line there is an error

--

- `Solution ✅` ?


```js

// Code


```

