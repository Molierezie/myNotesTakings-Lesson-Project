# <font color="#000000">⚫️ UserFlow RTK Query</font>

## 🔶 - <span style="background:#d4b106"><font color="#ffffff">Register / Login / Logout</font></span>

### 1️⃣ RTK Query

#### 💻 VS Code

##### Register

🧩 **Feature/auth**

```jsx

import { createSlice } from ''

// we intialatState take an object key value pairs
// He we set an conditional for the value and we parse the result because after we will use 
// the userInfo inside the app

const initialState = { userInfo : localStorage('user', userInfo) ? JSON.parse(localStorage('user', UserInfo) ) : null }

const authSlice = createSlice({

    // the name of the slice it's the same name set in the store
    name : 'auth',

    initialState : initialState,

     // this function take two arguments state and action
            // the state is the actual state in initialState
            // the action is an object which take type and payload
            // payload is the value set when we dispatch the action in the component
            // Imagine an user login so now the information of the user will be the payload 
            // when we set an code javascript to Localstprage we need to stringify the payload
    reducer :  {


        setCredential : ( state, action)=>{

            state.userInfo : action.payload
            localStorage('userInfo', JSON.stringify(action.payload))

            const date = new Date()*30*30
            localStorage('dateExpire' , date)
        },
        

        // When the user logout we set the initialState to "null" and we remove the info from localStorage
        logout : (state)=>{

            state.userInfo = null
            localStorage.clear()
        }
    }


})

// These function are exported in the components
export const ( setCredential, logout) = authSlice.actions

// we export the slice and we set the reducer in the store as a value and the key will be the name of the slice here 'auth'
export default authSlice.reducers



```

--

🧩 **Store**


```jsx

import { authSlice } from

const store = configureStore({


    reducer : {

        api : apiSlice.Reducers,
        auth : authSlice.reducers
    },

    middleware : (getDefualtMiddleware)=>
})


```

--

🧩 **apiSliceUser**

```js

import { BASE_URL } from ''
import { apiSlice } from ''


const apiUserSlice = injectEndpoints({


    
        endpoints : (builder)=>({


            register : builder.mutation =>(

                query : (dataRegister)=>({

                        url : `${BASE_URL}/register`,
                        Method : 'POST',
                        body : dataRegister

                })
            )

        })




})


export const { useRegisterMutation} = apiUserSlice

```

--

🧩 **Register.jsx**


```jsx


import { useState, useEffect} from react
import { useDispatch, useSelector} from ''
import { useRegisterMutation } from ''
import { navigate } from ''
import { toast} from ''



const Register = ()=>{

        // Here with useState for the info that we need in our back-end for the login user
        const [ username, setUsername] = useState('')

        const [ email, setUsername] = useState('')

        const [ password, setPassword] = useState('')

        // We add confirmPassword for more security
        const [ confirmPassword, setConfirmPassword] = useState('')


         // Thanks to the new object provide by the RTQ query powerful we create a function which trigger the API call for the register
        // We use also an object if there is a loading
        const [ Register ] = useRegisterMutation()

        const navigate = useNavigate()


         // We take the infos form the form and set in the trigger API Call 'login'
        // After thanks to the dispath we send the payload in the store => reducer => localStorage
        const handleSubmit = async (e)=>{


            e.preventDefault()


            if(confirmPassword !== password){
                
                const res = console.log('password is different to confirmPassword')
                return res
            }

                try{
        
                    // We use the syntax ES6 
                    // const res = { data : username (back-end) : username (front-end)}

                    const res = await Register({ dataRegister : username, email , password }).unwrap()

                    if(res){

                        dispatch({setCredential(res)})
    
                        navigate('/home')
    
                        toast.success(`Welcome${username}`)


                    }else{

                        toast.error(error.message)
                    }



                }catch(err){

                    toast.error(err.message)
                }


        }



    return(



            <form  onSubmit={handleSubmit}>

                <input
                type='text'
                name='username'
                value={username}
                onChange={ (e)=>setUsername(e.target.value)}
                required
                />

                <input
                type='email'
                name='email'
                value={email}
                onChange={ (e)=>setEmail(e.target.value)}
                required
                
                />

                <input
                type='password'
                name='password'
                value={password}
                onChange={ (e)=>setPassword(e.target.value)}
                required
                />

                <input
                type='password'
                name='ConfirmPassword'
                value={ConfirmPassword}
                onChange={ (e)=>setConfirmPassword(e.target.value)}
                required
                />

                <button type='submit'> Créer un compte </button>
            </form>



    )
}
```
---

##### Login

🧩 **apiUserSlice.jsx**


```jsx


import { BASE_URL } from ''

const apiUserSlice = injectEndpoints({


    endpoints : (builder)=>(


        login : builder.mutation({

            query : (dataLogin)=>({

                url : `${BASE_URL}/login-user`,
                method : 'POST',
                data : dataLogin
            })
        })
    )
})


export const { useLoginMutation} = apiUserSlice


```

--

🧩 **Login.jsx**



```jsx


import { useLoginMutation} from ''
import { useDispatch} from ''
import { useState, useEffect} from ''
import { useNavigate, useParams} from ''


const Login = ()=>{


        // Here with useState for the info that we need in our back-end for the login user
        const [ password, setPassword] = useState('')
        const [ email, setEmail] = useState('')


        const naviagte = useNavigate()
        

            // Thanks to the new object provide by the RTQ query powerful we create a function which trigger the API call for the login
            // We use also an object if there is a loading or error
        const [ Login, { isLoading : isLoadingLogin , error : errorLogin}] = useLoginMutation()


          // We take the infos form the form and set in the trigger API Call 'login'
         // After thanks to the dispath we send the payload in the store => reducer => localStorage
        const handleSubmit = async (e)=>{


            e.preventDefault()

            try{

                    const res = await Login({ dataLogin : email, password}).unwrap()

                    if(res){

                        dispatch({ setCredential(res)})
                        toast.success(`Welcome back ${res?.username}`)
                        navigate('/home')
                    }else{

                        toast.error(res?.error.message)
                    }

            }catch(err){

                    toast.err(err)
            }
        }



    return(



            <form onSubmit={HandleSubmit}>


                    <input
                    type='email'
                    value={email}
                    onChange={(e)=>setEmail(e.target.value)}
                    >

                      <input
                    type='password'
                    value={password}
                    onChange={(e)=>setPassword(e.target.value)}
                    
                    >


            <button type='submit'> </button>
            </form>



    )
}


```


---

##### Logout
