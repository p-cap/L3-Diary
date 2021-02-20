### Still need some work to learn about recursion. 
I think the best thing I got from trying to figure how recursion is returning their values in two ways:  
- Think of recursion like how stacks work
- stra with simpler problems so I can watch the returns closely

## Customizing my input html element and hopefully figure out away to props properly through creating seperate heper files.  

``` 
import "./style.css"
import { useState } from 'react';

export default function InputField() {
  const [info, setInfo] = useState("")
  return (
    <div>
    <form onSubmit={handleSubmit}>
      <input  
        className="some-class" 
        type="text" 
        id="name" 
        name="name" 
        required 
        placeholder="sample" 
        onChange={(e)=> setInfo(e.target.value)}
        />
        <h1>{info}</h1>
      </form>
    </div>
    )
}

// Still need to work on the handlesubmit function
```

CSS file 
```
.some-class {
  width: 400px;
  height: 30px;
  padding: 3px;
  font-size: 20px;
  border: 6px solid rgb(223, 215, 215);
  border-radius: 0.5rem;
  /* outline: 2px solid rgb(228, 145, 28); */
  padding-left: 10px;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  outline-color: green;
}
```
I wish I was more productive but kids wanted to play......I would say it was a great day.  
Hopefully, I can rebuid a json server via express and then render responses on the front end.  

## And one last thing, I am done with recursion....for now


