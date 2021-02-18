# A wonderful Algorithmic but no so good Front End day
I have to say I pretty proud of my kinda iterative approach to the coin change problem  

```
# I consider my first algorithmic victory

# The function below will return the MINIMUM number of denominations 
# based on the target parameter
def coinChange(target, coins):

    # Caches the count per denomination
    cache = []
    # result variable adds the total number of denominations
    result = 0

    # rearrange the array from highest to lowest
    coins.reverse()

    # divide each denomination to the target 
    for i in coins:
        # the if statement is filter the valid denominations 
        if (target // i > 0):
            cache.append(target // i)
            target = target - ((target // i) * i)

    # getting the total number of denominations from the list                       
    for j in cache:
        result += j
    
    # resets the coins denomination list to its original form
    coins.reverse()
    return int(result)

# test cases
coins = [1,5,10,25]
print(coinChange(23, coins) == 5)
print(coinChange(45, coins) == 3)
print(coinChange(74, coins) == 8)
```
The comments provide what my thought process was  

## Hmmmmmm....struggled with parent to child component props and creating a helper file for my HttpService 
Right now, the only improvement I have with my code is the fact that my HttpService file is now a seperate file   
```
import DisplayResponse from './DisplayResponse'

var validatedUsername
var validatedPassword
var responseData
const axios = require('axios')

export default function HttpService(props) {
    axios.post('http://localhost:8080/inject', {
        username: props.data.username,
        password: props.data.password
      })
        .then(response => { 
            responseData = response.data
        })
    return responseData
    }
```
This code is really messy. Wait till you see my App.js file......hidious!  
I did not make much progress with my full stack project but I definitely have a gameplan!  

##Must DOs
- Look into trying to apply recursion to my coin change code
- Create a playground so I can practice props from one component to the other
- Work on promises especially axios promises
- Dealing with react returns especially when a typeError occurs with what I am returning. Try to return an object perhaps


# STILL A GREAT DAY....it is late right now! Good night








