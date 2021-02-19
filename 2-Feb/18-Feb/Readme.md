## Coin Change Recursion

I was busy with prepping for my move next week.  
I tried to do the recursion version for coin change but I was not successful. 
I'll update it with the source code

```
def coinChange(target, coins):
    # create initial values
    cache = []
    results = 0
    # Base case 
    if (target == 0):
        return results

    print("results: ", results)
    # recursion case
    for i in coins:   
        if (target // i > 0):
            results += target // i
            print("results:", results)
            target -= ((target // i) * i)
    return coinChange(target, coins) + coinChange(target, coins)

    
coins = [1,5,10,25]
coins.reverse()
print("denominations: ", coinChange(23, coins))
# print(coinChange(45, coins) == 3)
# print(coinChange(74, coins) == 8)

```
My problem right now returning the updated result

