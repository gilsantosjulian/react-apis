# The Begginer's guide to Reavt JS
Sometimes we forget how works some basic thing regarding javascript and HTML elements. For instance how we can add a element into the DOM, or how the browser interprets the components we made in React js. The idea of this repositorie is show the begginer devs the basic idea that react are working.

## Write Hello World with raw React APIs
In this step we are going to create a simple HTML element using the basic funcions of javascript, and add them into the DOM. For this, we use the 'getElemetById(), createElement() and appendChild()' methods.
```
// 01-js.html
<div className='root'></div>
<script type='text/javascript'>
    const root = getElementById('root')
    const element = createElement('div')
    element.textConten = 'Hello World'
    element.className = 'Container'
    root.appenChild(element)
</script>
```
After we going to import the React an React-dom libraries.
```
// 01-js.html
<script src='https://unpkg.com/react@16.2.0/umd/react.development.js'></script>
<script src='https://unpkg.com/react-dom@16.2.0/umd/react-dom.development.js'></script>
<div className='root'></div>
<script type='text/javascript'>
    //React.createElement have two params:
    //const element = React.createElement('name', props <object>)
    const element = React.createElement(
            'div',
            {
                className: 'container',
                children: 'Hello World'
            }
        )
        console.log('element')
        console.log(element)

        ReactDOM.render(element, rootElement)
</script>
```
Finally we can test it in our browser.

## Using JSX with React
Until now, we are using one sintax that isn't good. In order to make more economic our code, we use JSX. The first thing to do is import it in the top of our file. For this we create a new file called *02-js.html* which will have the same code but with a different way to write it using JSX and change the type of script Let's see:
```
<script src='https://unpkg.com/babel-standalone@6.26.0/babel.js'></script>
<script type='text/babel'>
```

And create our new element, look at this:
```
const element = <div className='container'>Hello World</div>
```

One the good things that come with JSX is that we can pass variables trough interpolation and arrow functions (this make possible to do some another operations before to render the content), let's see with a little example:
```
const content = 'Hello World'
// 1. Interoplation
const element = <div className='container'>{content}</div>
// 2. Arrow functions
const element = <div className='container'>{() => content}</div>
```

Now we are going to see how we can pass props inside. Just we have to create a object with different props and put them in brackets using the spread operator.
```
const props = {
    className: 'container',
    children: 'Hello World'
}
const element = <div {...props} />
```

The idea to JSX is to specify what HTML element to rendered and whic props to pass it. It is a more comfortable way to use.