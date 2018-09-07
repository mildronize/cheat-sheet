# React & JavaScript ES6



## Next.JS

### Basic

```javascript
export default () => (
    <p>Technology + สารานุกรม = Techนุกรม</p>
)
```

### Basic SSR

```jsx
const Index = (props) => (
  <p>Data: {props.data}</p>
)
Index.getInitialProps = function () {
  return {data: 1}
}
export default Index
```

method ของ Nextjs for SSR

```javascript
getInitialProps(context) {
    var id = context.query.id === undefined ? 0 : context.query.id;
    // do something
}

// In server.js of express
server.get('/:id', (req, res) => {
    const actualPage = '/'
    const queryParams = { id: req.params.id }
    app.render(req, res, actualPage, queryParams)
})
```

### Sass setup

1. `yarn add next-sass node-sass`
2. แก้ไฟล์ `./next.config.js`

   ```jsx
   // ./next.config.js
   const withSass = require('@zeit/next-sass')
   module.exports = withSass({
       exportPathMap : () => { '/': { page: '/' } }
       sassLoaderOptions: {
         includePaths: ["./node_modules", "./styles"],  // don't use relative path
         outputStyle: 'compressed'  // minify CSS
       }
     });
   ```

3. สร้างไฟล์ `./styles/index.scss`
4. เพิ่ม `import '../styles/index.scss'` ใน `./pages/_app.js`

   ```jsx
   // ./pages/_app.js
   import App, {Container} from 'next/app'
   import React from 'react'
   // Add this line
   import '../styles/index.scss'

   export default class MyApp extends App {
     static async getInitialProps ({ Component, router, ctx }) {
       let pageProps = {}

       if (Component.getInitialProps) {
         pageProps = await Component.getInitialProps(ctx)
       }

       return {pageProps}
     }

     render () {
       const {Component, pageProps} = this.props
       return <Container>
         <Component {...pageProps} />
       </Container>
     }
   }
   ```

5. แก้ `./pages/_document.js`

   ```jsx
   // ./pages/_document.js
   import Document, { Head, Main, NextScript } from 'next/document'

   export default class MyDocument extends Document {
     static async getInitialProps(ctx) {
       const initialProps = await Document.getInitialProps(ctx)
       return { ...initialProps }
     }

     render() {
       return (
         <html>
           <Head>
             <style>{`body { margin: 0 } /* custom! */`}</style>
             {/* Add this line */}
             <link rel="stylesheet" type='text/css' href="/_next/static/style.css" />
           </Head>
           <body className="custom_class">
             <Main />
             <NextScript />
           </body>
         </html>
       )
     }
   }
   ```

## React

### Introduction

* [Learn React - React Crash Course 2018 - React Tutorial with Examples](https://www.youtube.com/watch?v=Ke90Tje7VS0) Best video react tutorial ever!!!
* เริ่มต้นที่นี้ [https://github.com/facebook/create-react-app](https://github.com/facebook/create-react-app)
* [Nextjs Learn](https://nextjs.org/learn/)
* [https://hackr.io/hack-n-learn](https://hackr.io/hack-n-learn) สร้าง app shopping pokemon ด้วย react มีทั้ง asset และ code ให้ 

#### Best Practice

* [Writing Scalable React Apps with the Component Folder Pattern](https://medium.com/styled-components/component-folder-pattern-ee42df37ec68) การออกแบบ react component และ directory , `component folder pattern`

  > A **component** should **do one thing**, and do it well

* Read later
  * [Function as Child Components Are an Anti-Pattern](https://americanexpress.io/faccs-are-an-antipattern)

### Getting started react in html

```markup
<div id="root"></div>
<script crossorigin src="https://unpkg.com/react@16/umd/react.development.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/babel-standalone/6.26.0/babel.min.js"></script>
<script type="text/babel">
class HelloWorld extends React.Component {
    render() {
        return (<h1>Hello world</h1>);
    }
}
ReactDOM.render(
    <HelloWorld />,
    document.getElementById('root')
);
</script>
```

### React JS template, from beginner in JS & react

```javascript
import React from 'react';

export default class Index extends React.Component {

  constructor(props) {
    super(props)
    this.state = { data: 0 };
  }

  componentDidMount() {
    this.setState({ data: 1 })
  }

  render() {
    return (
      <div>
        Data: {this.state.data}
      </div>
    )
  }
}
```

### React onclick

[http://www.hackingwithreact.com/read/1/9/handling-events-with-jsx-onclick](http://www.hackingwithreact.com/read/1/9/handling-events-with-jsx-onclick) Don't

```javascript
loadMore() {
  // do something
}
render return <a onClick={this.loadMore.bind(this)}>Load more</a>;
```

Do [https://codeburst.io/6-simple-ways-to-speed-up-your-react-native-app-d5b775ab3f16](https://codeburst.io/6-simple-ways-to-speed-up-your-react-native-app-d5b775ab3f16)

```javascript
constructor(props) {
    super(props);
    this.doSomething= this.doSomething.bind(this);
}

doSomething() {
  // do something
}
render return <a onClick={this.doSomething}>Load more</a>;
```

### Loading Button

```javascript
render <a class={`button is-primary ${this.state.isLoading ? "is-loading" : ""}`}>Load More</a>
```

## Javascript

### Functional Programming

ใน JS สามารถเขียน แบบ Functional Programming  เป็น declarative paradigm 

### เปรียบเทียบ imperative และ declarative paradigm 

**imperative** คือคิดจาก หน้าไปหลัง , ล่างขึ้นบน คล้ายๆ กับภาษา C เช่น เราจะออกไปวิ่งรอบสนาม 10 รอบ เราก็ต้องคิดว่า เราจะเริ่มทำอะไรก่อน หลังจากนั้นจะทำอะไร เราสามารถลำดับเป็นขั้นตอนดังนี้

* ใส่รองเท้า
* เดินไปสนามวิ่ง
* เริ่มวิ่ง แล้ว จำว่า ตอนนี้อยู่รอบที่เท่าไหร่แล้ว
* วิ่งจนครบ 10 รอบ

หรือสามารถ เขียนเป็นโปรแกรมได้ดังนี้นะ

```javascript
prepare_something();
for( var i = 0; i < 10; i++ ){
    run();
}
```

**declarative** คือ คิดบนลงล่าง เช่น วิ่งรอบสนาม 10 รอบ แต่เราสิ่งที่เราเห็นคือ เราเห็นแค่ ว่าเราทำอะไร แต่เราไม่จำเป็นต้องรู้ว่า ข้างในนั้นเราทำอะไรบ้าง

```javascript
rounds.map( round => {
    run();
});
```

### String

```jsx
const hello = "hello";
const str = `${hello} world`;
```

### Import

```jsx
// relative path
import PostItem from '../components/PostItem';
// from npm
import Document from 'next/document';

// Import default module
import Document from 'next/document';
// Import modules
import { Head, Main, NextScript } from 'next/document';
// Import default module & modules
import { Head, Main, NextScript } from 'next/document';
```

### Export

```jsx
// # Anonymous Export

// Export default function
export default () => { 
    // do something
}
// Export function
export () => {
  // do something
}
// Export object
module.exports = {}

// # Export
const config = {};
const confit.doSomething = () => { } // alternative
export config; // or export default config;
```

### Promises

A promise is an object which can be returned synchronously from an asynchronous function \([ref](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-promise-27fc71e77261#3cd0)\).

```javascript
const fetchingPosts = new Promise((res, rej) => {
  $.get("/posts")
    .done(posts => res(posts))
    .fail(err => rej(err));
});

fetchingPosts
  .then(posts => console.log(posts))
  .catch(err => console.log(err));
```

```jsx
const xFetcherPromise = new Promise( // สร้าง promise โดยใช้คีย์เวิร์ด "new" และเก็บลงตัวแปร
  function(resolve, reject) { // constructor ของ promise รับ parameter เป็นฟังก์ชั่นที่มี parameter ชื่อ resolve และ reject ด้วยตัวมันเอง
    $.get("X") // ส่ง Ajax request
      .done(function(X) { // เมื่อ request เสร็จแล้ว ...
        resolve(X); // ... resolve promise ด้วยค่า X กลับไปเป็น parameter
      })
      .fail(function(error) { // ถ้า request เกิดผิดพลาด...
        reject(error); // ... reject promise แล้วส่ง error กลับไปเป็น parameter
      });
  }
)
```

```javascript
xFetcherPromise
  .then(function(X) {
    console.log(X);
  })
  .catch(function(err) {
    console.log(err)
  })
```

#### ส่งค่าข้าม promise.then ซ้อน promise \(firestore\)

```javascript
const handleQuery(query){
  return new Promise((resolve, reject) => {
    ref.get().then((documentSnapshots) => {

      let i = 0;
      var tmp_data = []
      documentSnapshots.forEach((doc) => {
        tmp_data.push(doc.data())
      });

      // Build a reference for next page
      const lastVisible = documentSnapshots.docs[documentSnapshots.size - 1];
      if (!lastVisible) return;

      resolve({
        data: tmp_data,
        refNext: ref.startAfter(lastVisible)
      });

    })
  })
}

const getData = async (query) => {
    const responsePromise = handleQuery(query);
    return responsePromise;
}

export default async () => {
    const data = await getData()
}
```

### Spread operator "..."

สั้นๆ คือ กระจายตัวออกให้หมด

```jsx
const arr1 = ["a", "b", "c"];
const arr2 = [...arr1, "d", "e", "f"]; // ["a", "b", "c", "d", "e", "f"]
```

### **Higher-order Function \(HoF\)**

ใน JS function เป็น _first-class objects,_ สามารถที่กำหนดให้เป็น parameter ของ function อื่นได้ หรือ assign ให้ตัวแปรได้ด้วย

[Higher-order Function ](https://www.safaribooksonline.com/library/view/react-design-patterns/9781786464538/ch02s03.html)คือ function ที่เอา function เป็น parameter และ return ออกเป็น function เช่นเดียวกัน โดยเราสามารถเพิ่มความสามารถอะไรบางอย่างให้กับ function นั้นได้ เช่น เราสามารถ log parameter ของ function add ได้ผ่านเทคนิค HoF

```javascript
const add = (x, y) => x + y 
 
const log = func => (...args) => { 
  console.log(...args) 
  return func(...args) 
} 
 
const logAdd = log(add) 
```

เทคนิคจะใช้มากใน React ก็คือ Higher-order Components \(HoC\)

## Ref:

* [Modern JS Cheat sheet](https://github.com/mbeaudru/modern-js-cheatsheet)  one-stop cheat sheet for JS developer

