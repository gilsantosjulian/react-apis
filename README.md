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