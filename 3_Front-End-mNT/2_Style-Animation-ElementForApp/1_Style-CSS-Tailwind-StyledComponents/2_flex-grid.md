# <font color="#00b0f0">🔵 Flexbox & Grid</font> 

## 🟠 -  <font color="#f79646">Grid</font>

### 🔶 - <span style="background:#d4b106"><font color="#ffffff">Subgrid</font></span>

#### <font color="#ffc000">What's it ?</font>

---

#### <font color="#e36c09">👨🏾‍💻 - Let's Practice</font>


##### Task

`task 1)`

- Solve the alignement issue within the card in the Cartier website

- ![subgridCartier1](https://github.com/user-attachments/assets/d9a306a4-0300-4aa9-82db-bfa779ae3313)


----

`2)`

- Build this

----


##### <font color="#0070c0">CSS</font>

`📔 Ressource`

- 📖 [Ressource](Link)
- 🎥 [Ressource](Link)

---

`1)`

🧩 `html`
```html

```

🧩 `css`
```css

```

---

`2)`

---

##### <font color="#d99694">SCSS</font>

`📔 Ressource`

- 📖 [Ressource](Link)
- 🎥 [Ressource](Link)

---

##### <font color="#4bacc6">Tailwind</font>

`📔 Ressource`

- 📖 [Ressource](Link)
- 🎥 [Ressource](Link)

--



`task 1) with flexbox ❌`

🧩 **home.jsx** 

```jsx


<div className='bg-purple-500 w-full h-[100vh] p-8 flex gap-8 justify-center items-center'>

 

  <div className='bg-yellow-500 w-[40vw] h-[70vh] flex flex-col justify-center items-center gap-8'>

    <img src={subgridCartier2} className='h-[30vh] w-[90%] object-cover' />

    <h2 className='font-bold text-purple-950 text-[2.5rem]'>Panthère Double
    </h2>

    <p className='mx-auto text-center'>
    Un sac à main de caractère dont Cartier sophistique la anse par deux têtes de panthère sculpturales.​
    </p>

    <button className='border-black border-b-2'>Découvrir</button>


  </div>


  <div className='bg-red-500 w-[40vw] h-[70vh] flex flex-col justify-center items-center gap-8'>

<img src={subgridCartier3} className='h-[30vh] w-[90%] object-cover' />

<h2 className='font-bold text-purple-950 text-[2.5rem] text-center'>Un parfum, une panthère
</h2>

<p className='mx-auto text-center'>
Un grand classique de la parfumerie qui ose revisiter le mythique chypre avec un accord floral fauve inédit.

</p>

<button className='border-black border-b-2'>Découvrir</button>


</div>


 </div>


```

👀 view in the browser

![Flex Subgrid-1](https://github.com/user-attachments/assets/7db1e601-c766-4b66-851a-2b59a8ece9ba)

**Problem** 

- As we can see using flexbox if inside the card the longer of the title, text is different between the cards all will not align , image, text
- bad experience users
--

`task 1) with flexbox adjust the gap ❌`

🧩`home.jsx` file

```jsx


<div className='bg-purple-500 w-full h-[100vh] p-8 flex gap-8 justify-center items-center'>

 

 <div className='bg-yellow-500 w-[40vw] h-[70vh] flex flex-col justify-center items-center   👀 gap-[3.2rem] 👀'>

   // Code don't change


  </div>


  <div className='bg-red-500 w-[40vw] h-[70vh] flex flex-col justify-center items-center 👀 gap-[1.8rem] 👀'>

// Code don't change


</div>


 </div>


```

👀 view in the browser

![Flex Subgrid-2](https://github.com/user-attachments/assets/ac403fa3-4785-43b7-a268-1641e7fbb465)

**Problem** 

- As we can see using flexbox even if we play with the gap for get the card align there are still an alignement 
--

--

`task 1 - with grid ✅`

- thanks to the new feature subgrid we can solve this alignement issue

🧩`tailwind.config` file

- The properties for the columns and the subgrid don't works in the same way to classic CSS, so we configure this property in tailwind.config
- I use auto-fit in the grid-column for handle the responsive

```jsx

export default {

  content: ['./src/**/*.{js,jsx,ts,tsx}'],

  theme: {

    gridTemplateColumns : {

      gridAutoFit : 'repeat(auto-fit , minmax(350px,1fr))',
    },

    gridTemplateRows : {

      'sub' : 'subgrid',
 
    },
   
  }
}

```

--

🧩`home.jsx` file

```jsx

<div className='bg-green-500 h-[200vh] w-[100vw] p-4'>

1️⃣ <div className='h-[80vh] bg-blue-700 grid grid-cols-gridAutoFit gap-2'>

  2️⃣  <div className='bg-yellow-500 w-[40vw] items-center grid grid-rows-sub row-[span_5]  mx-auto text-center'>

      <img src={subgridCartier2} className='h-[30vh] w-[90%] object-cover mx-auto' />

      <h2 className='font-bold text-purple-950 text-[2.5rem]'>Panthère Double
      </h2>

      <p className='mx-auto text-center'>
      Un sac à main de caractère dont Cartier sophistique la anse par deux têtes de panthère sculpturales.​
      Un sac à main de caractère dont Cartier sophistique la anse par deux têtes de panthère sculpturales.​   
      </p>

      <button className='border-black border-b-[1px] w-[75px] mx-auto'>Découvrir</button>


    </div>


2️⃣  <div className='bg-orange-500 w-[40vw] h-[100%] items-center  grid grid-rows-sub row-[span_5]  mx-auto text-center'>

<img src={subgridCartier3} className='h-[30vh] w-[90%] object-cover mx-auto' />

<h2 className='font-bold text-purple-950 text-[2.5rem] text-center'>Un parfum, une panthère
</h2>

<p className='mx-auto text-center'>
Un grand classique de la parfumerie qui ose revisiter le mythique chypre avec un accord floral fauve inédit.

</p>

<button className='border-black border-b-[1px] w-[75px] mx-auto'>Découvrir</button>


</div>

</div>


</div>

```

1️⃣
- We wrap all the card in a div and inside this div we put
    - the grid-column property from tailwind config

--

2️⃣
- Within each card we define the new feature subgrid
    - and for example in there are 4 elements within the card, we put row-[span_5], after subgrid,
    - if there are 6 elements inside the card, we put row-[span_7] after subgrid


👀 view in the browser

![Flex Subgrid-3](https://github.com/user-attachments/assets/4be758b6-1125-4625-be5c-72e99a4afad0)

**Solution ✅** 

- As we can see using grid and the new feature subgrid we solve the alignement issue, even if the text is more longer , all the elements within the items remain aligned

👀 view in the browser

![Flex Subgrid-4](https://github.com/user-attachments/assets/329384b4-ef3a-4e2c-8633-ff984b53b3ea)

---

##### <font color="#8064a2">Styled-Components</font>

`📔 Ressource`

- 📖 [Ressource](Link)
- 🎥 [Ressource](Link)


---
