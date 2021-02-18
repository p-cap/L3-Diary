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
