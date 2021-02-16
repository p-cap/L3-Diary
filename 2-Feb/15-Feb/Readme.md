## Finding the nth number in the Fibonnacci series utilizing Resursion

I was trying to understand the recursion functions were being called sequentially  
So, I came up the code below of creating dependent functions but within those functions  
were the recursion calls

```
def sample_recursion(i):    

    # base case 
    if i == 0 or i == 1:
        # print("IF :" + str(i))
        return i

    else:
        # instead of return sample_recursion(i - 1) + sample_recursion(i - 2)
        return f1(i - 1) + f2(i - 2)

def f1(j):
      return sample_recursion(j)

def f2(k):
    return sample_recursion(k)

print("Result:" + str(sample_recursion(4)))

```
Instead of ```return sample_recursion(i - 1) + sample_recursion(i - 2)```, I put two indepdent functions  
to see if I can figure out how recursive cases / functions are being called.  
I think that the functions from the left finishes all their returns then comes the next funciton in  
recursion case
