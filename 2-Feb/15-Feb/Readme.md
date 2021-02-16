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



# Day 1 of SQL Injection Login Page website
<p> Today was a very fruitful day because I was able to finish most of my project </p>
<p> First, I worked on the Spring application to serve as the endpoint for my fullstack project </p>

<p> Here were the steps adn struggles I had when creating Spring Endpoint Application</p>  

    - Spring initializr with Spring Web and PostgreSQL Driver as it's depdencies
    - Followed the tutorial from zetcode https://zetcode.com/springboot/postgresql/
    - NOTE: I already created an existing table and database so I just needed to integrate my spring boot application
    - I tried to run the application but I was having issues with ```@Autowired``` annotation which was declared with 
      my CRUD Repository
    - After an hour of trying to figure out my problem, I ended up downloading an new Spring Initializr zip file but this 
      time I added Spring Data JPA and.......it worked
 
<p align="center">
  <img src="Spring Initialzr correct package.JPG" title="Spring Boot Initializr Config">
</p>
    
    






