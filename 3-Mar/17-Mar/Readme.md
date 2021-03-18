# Creating a Binary through lists

Reference: Python for Data Strcuture and Algorithms wiht Jose Portillo

```
def binaryTree(r):
    return [r,[],[]]
    
r = binaryTree(3)

r = [3, [], []]
```
#### Function creates a root node, the left and right side of the binary tree

```
def. insertLeft(root, newbranch)

  t = root.pop(1)
  
  if len(t) > 1:
    root.insert(1, [newBranch, t, []])
  
  else:
    root.insert(1,[newBranch, [], []])

```
#### Insert the left side of the binary tree


```
def. insertLeft(root, newbranch)

  t = root.pop(2)
  
  if len(t) > 1:
    root.insert(2, [newBranch, t, []])
  
  else:
    root.insert(2,[newBranch, [], []])

```
#### The only difference is the ```t = pop(2)``` and where to insert the new branch

## I still need to look into why when calling the following:

- r = binaryTree(3)
- insertLeft(r, 4)
- insertLeft(r, 5)
- insertLeft(r, 6)

Output: ```[3, [6, [5, [4, [], []], []], []], []]```
- I added 4 first as a branch?????





