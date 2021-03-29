# Struggled with one of the kickstart problems I learned quite a bit in ```PYTHON```

## input file
```
2
2
Oksana Baiul
Michelle Kwan
3
Elvis Stojko
Evgeni Plushenko
Kristi Yamaguchi
```


## Reading from files
- content becomes an array
```
with open(filename) as f:
    content = f.read().splitlines()
```

## Used try....except block
- Basically, when I was iterating through the array with ```isinstance(int(j), int)``` and it would hit a string, I would get a ```ValueError: invalid literal for int() with base 10:``` because when I was casting the str into int(), it was not an int.
```
for i in range(1, t + 1):
    for j in content:
        // the code below would cause the error
        if isinstance(int(j), int): 
            continue
        else:
            arr.append(i)
            if len(arr) > 1:
                if arr != sorted(arr):
                    charge += 1
                    arr.sort()
    break
```

## Below is the closest I can get
- this would account for all of the string but combine them all together even though there are two cases
```
for i in range(1, t + 1):
    for j in content:
        try:
            j = int(j)
            continue
        except ValueError:
            arr.append(j)
            if len(arr) > 1:
                if arr != sorted(arr):
                    charge += 1
                    arr.sort()
    break
```



