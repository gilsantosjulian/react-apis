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

## Create Custom React Components
In this step, is needed use a reusabe elements in someway from your application, for this, is a good idea make a a custom react components. It is very helpfull in order to mantein our app performance. 

We going to make a *React.createElement* function that is useful to create our element:

```
const Message = () => <div>Hello World</div>
const element = (
    <div>
        {React.createElement(Message, {})}
    </div>
)
```

Now, wirte React.createElement funcion is more easy usin babel, just only we have to write in angular brackets <Message /> passing into the props, for instance (it happen because is the same, only change the sintax):

```
const Message = (props) => <div>{props.msg}</div>
const element = (
    <div>
        <Message {msg: 'Hello World'}/>
    </div>
)
```

And we can call it every time that we need:
```
const Message = (props) => <div>{props.msg}</div>
const element = (
    <div>
        <Message msg={'Hello World'} />
        <Message msg={'Good Bye'} />
    </div>
)
```

So we can use it like children component too:
```
const Message = (props) => <div>{props.msg}</div>
const element = (
    <div>
        <Message>
            Hello World
            <Message>
                Good Bye
            </Message>
        </Message>
    </div>
)
```

## Validate Custom React Component Props with PropTypes
In this lesson we'll learn about how you can use the prop-types module to validate a custom React component's props.

The first thing that we going to do, is create a new function that recive props:
```
function SayHello(props) {
            return(
                <div>
                    Hello {props.firstname} {props.lastName}
                </div>
            )            
        }
```

Now we have to describe our props to passed into the function, lest see:
```
SayHello.proptypes = {
            firstName(props, propName, componentName) {
                if(typeof props[propName] !== 'string') {
                    return new Error(`Hey, you should pass a string for ${propName} in componentName ${componentName} but you passed a ${typeof props[propName]}`)
                }
            }
        }
```

One best form to rewrite this is:
```
const PropTypes = {
            string(props, propName, componentName) {
                if(typeof props[propName] !== 'string') {
                    return new Error(`Hey, you should pass a string for ${propName} in componentName ${componentName} but you passed a ${typeof props[propName]}`)
                }
            }
        } 

        SayHello.propTypes = {
            firstName: PropTypes.string,
            lastName: PropTypes.string,
        }
```

However, we have to include the library on top of the our file and remove the proptypes const:
```
 <script src='https://unpkg.com/prop-types@15.6.0/prop-types.js'></script>
```

Until this step, we can check our props to passed into, but we can make them require too. First we going to pass a unknown prop, and define the others like require:
```
<div>
    Hello {props.firstname} {props.lastName || 'Unknown'} 
</div>

SayHello.propTypes = {
    firstName: PropTypes.string.isRequired,
    lastName: PropTypes.string.isRequired,
}
```


## Conditionally Render A React Component
In this step we explore JSX a little further and solidify in our minds that JSX is simply syntax sugar on top of a fairly simple React API: React.createElement

First one, we can to pass props into a function called 'Message - our component', and if exist, show a message, if not, show a 'No Message texts' using a simple conditional.
```
function Message({message}) {
    if(!message) {
        return <div>No Message</div>
    }
    return <div>{message}</div>        
}
```

We can to rewrite our code returning a div tag, using React.createElement() method, making a little more fancy let's see:
```
function Message({message}) {
    return(
        message
        ? React.createElement('div', null, message)
        : React.createElement('div', null, 'No Message')
    );        
}
```

At the final, we can to do better our code, involved whole into a div and returning new divs:
```
function Message({message}) {
    return(
        <div>
            {
                message
                ? <div>{message}</div>
                : <div>No Message</div>
                }
        </div>
    );               
}
```

## Rerender a React Application
In this step, we'll learn how we can call ReactDOM.render repeatedly with brand new React Elements and React will preserve element focus and only do the minimal required DOM operations for the re-render.

The first thing that we are going to do, is display our local time, for this only we have to use the 'toLocaleTimeString()' method:

```
const rootElement = document.getElementById('root')
const time = new Date().toLocaleTimeString()
const element = <div>It is {time}</div>
```

Now we start to impproving our code put into the code in one function and call it every second using a setInterval() method, let see:
```
function tick(){
    const rootElement = document.getElementById('root')
    const time = new Date().toLocaleTimeString()
	const element = <div>It is {time}</div>
	ReactDOM.render(element, rootElement)
}
tick()
setInterval(tick, 1000)
```

In roder to see the focus of the ReactDOM, we going to put into a text input tag our time:
```
function tick(){
    const rootElement = document.getElementById('root')
    const time = new Date().toLocaleTimeString()
	const element = 
        <div>
            It is 
            <input value={time}/>
            <input value={time}/>
        </div>
	ReactDOM.render(element, rootElement)
}
tick()
setInterval(tick, 1000)
```

Ok now we are going to see how ReactDOM help us to focus only in the div that is doing updated. If you inspect the html file in browser, you can see that the only html tag that is updated is the <input />. Only render the component that is necesary.

But is very different if we use the common javascript using the innerHTML param for include the same code, passing it into a string variable, something like this:
```
function tick(){
    const rootElement = document.getElementById('root')
    const time = new Date().toLocaleTimeString()
	const element = `
        <div>
            It is 
            <input value=${time}/>
			<input value=${time}/>
        </div>
    `
    rootElement.innerHTML = element
	//ReactDOM.render(element, rootElement)
}
tick()
setInterval(tick, 1000)
```

If you inspect again the html file in your browser, you can see that all div is updated. Thats meand all the page is rendered.

## Style React Components with className and In Line Styles
In this step, we'll learn about how you can style react components using the style prop and className prop. We will go over how these props are differant than regular html style and class properties. Style, in JSX, takes an object, camel casing the property keys like borderRadius instead of border-radius.

First we are going to include our object style (normally we add the styles in the string form), let's see:
```
const rootElement = document.getElementById('root')
const element = (
    <div>
        <div style={{ paddingLeft: '20px' }}>box</div>
        <div style={{ paddingLeft: 20 }}>box</div> you can write it in only number
    </div>)
ReactDOM.render(element, rootElement)
```

Ok, is very good for now, but we can inlcude our styles only to calling our CSS class with the key word *Clasname*. First include our style and after calling our key word:

```
<style>
    .box {
        padding-left: 20
    }
</style>
const element = (
    <div>
        <div className='box'>box</div>
    </div>
)
```

Well we are going to be more specific, let's try (Adding more style):
```
.box-small {
    width: 60px;
    height: 60px;
    border: 1px solid gray;
}
const element = (
    <div>
        <div className='box box-small'>box</div>
    </div>
)
```

Now we can to make our Box component, just into a new function, let's see passing three params (className, style and another params - rest):
```
function Box({className, style, rest}) {
    return(
        <div 
            className={`box ${className}`} //Using interpolation
            style={{paddingLeft: 20, ...style}}
        >
            {...rest}
        </div>
    );
}
```

## Use event handlers with React
In this part we are going to how React catch the events in the HTML elements and take care and delegation. 

Fist we going to create a onClick event for a button, and pass it inline arrow function that will modify the state and increment our count variable.

```
    <button onClick={() => setState({ eventCount: state.eventCount + 1 })} >Button</button>
```