---
title: hooks
description: ""
position: 7
category: Guide
---

## rules of hooks

\- Only call Hooks at the top level

\- Only call Hooks from React function components

## use state

```jsx
import React, { useState } from 'react'

export default function Counter() {
    const [count, setCount] = useState(0);
    return (
        <div>
            <button onClick={() => {
                setCount((count) => {
                    return count + 1;
                });
            }}>
                count { count }
            </button>
        </div>
    )
}
```

exemple 2: handling form with use state

**NB:** the object and array act like a reference in javascript

```jsx
export default function Form() {
    const [formData, setFormData] = useState({ name: '', age: 0 });
    return (
            <div>
            <h1>name: {formData.name}, age: { formData.age }</h1>
                <form action="">
                <input type="text" value={formData.name} onChange= { 
                    (e) => {
                        setFormData((formData) => {
                            return {...formData, name: e.target.value}
                        })
                    }
                 } />
                <input type="number" value={formData.age} onChange={
                    (e) => {
                        setFormData((formData) => {
                            return { ...formData, age: e.target.value };
                        })
                    }
                    } />
                    <button type="submit">submit</button>
                </form>
            </div>
        )
}
```

## useEffect

a function excecuted every component render

exemple: change the title on every sigle render

```jsx
export default function Effect() {
    const [count, setCount] = useState(0);

    useEffect(() => {
        document.title = count;
    });
    
    return (
        <div>
            <p>clicked { count } time</p>
            <button onClick={(e) => {
                setCount((count) => {
                    return count + 1;
                })
            }}>increment</button>
        </div>
    )
}
```

### ignore some state

for optimization reason, we need sometime to ingnore some state modification

add the state to be considered as a second parameter if this is the case

exemple: run the useEffect fuction only if the count state was changed

```jsx
export default function Effect() {
    const [count, setCount] = useState(0);
    const [name, setName] = useState('san')

    useEffect(() => {
        document.title = count;
        console.log("here")
    }, [count]);

    return (
        <div>
            <p>name: {name} </p>
            <input type="text" value={name} onChange={(e) => {
                setName((name) => {
                    return e.target.value;
                })
            }} />
            <p>clicked { count } time</p>
            <button onClick={(e) => {
                setCount((count) => {
                    return count + 1;
                })
            }}>increment</button>
        </div>
    )
}
```

**to ignore all state use an empty array to the second parameter**

exemple

```jsx
export default function MouseTracker() {
    const [x, setX] = useState(0);
    const [y, setY] = useState(0);

    useEffect(() => {
        console.log("useEffect excecuted");
    }, []);
    return (
        <div className={styles.wide} onMouseMove={(e) => {
            setX(e.clientX);
            setY(e.clientY);
        }}>
            positon: x = {x} y= {y}
        </div>
    )
}
```

### clean up after unmounting

like component did unmount in class component.

just return an fuction inside the useEffect function

exemple: 

```jsx
export default function Timer() {
    const [second, setSecond] = useState(0);
    useEffect(() => {
        const interval = setInterval(() => {
            setSecond((second) => {
                return second + 1;
            })
        }, 1000)
        return () => {
            clearInterval(interval)
        }
    }, [])
    return (
        <div>
            {second}
        </div>
    )
}
```

## multile useEffect hook in a component

yes you can call useEffect as many time you like in a component