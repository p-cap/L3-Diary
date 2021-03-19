# Binary Tree using Classes

Reference: Udemy Course entitled "Python for Data Structures and Algorithms from Jose Portillo"

### NOTE: When adding new child into the binary tree, the newer addition is closer to the root

## Binary Tree class with 3 attibutes
```
 3 class BinaryTree(object):
  4 
  5    def __init__(self, rootObject):
  6 
  7       self.key = rootObject
  8       self.leftChild = None
  9       self.rightChild = None
  ...
```

## Inserting the child nodes
```
11    def insertLeft(self, newNode):
 12 
 13       if self.leftChild == None:
 14          self.leftChild = BinaryTree(newNode)
 15 
 16       else:
 17 
 18          t = BinaryTree(newNode)
 19          t.leftChild  = self.leftChild
 20          self.leftChild = t
 21 
 22    def insertRight(self, newNode):
 23 
 24       if self.rightChild == None:
 25          self.rightChild = BinaryTree(newNode)
 26 
 27       else:
 28 
 29          t = BinaryTree(newNode)
 30          t.rightChild  = self.rightChild
 31          self.rightChild = t
```
### ELABORATE: When the else statement is used, ```t = BinaryTree(newNode)``` creates a new Binary instance with the new node.The existing left child node is added saved to ```t```. This makes sure the actual left child node value is saved into the Binary Tree instance. Then, ``` self.leftChild = t```, the gets the entire instance from t into the left child node. To me, this is critical series of code to grow the tree accordingly

## Printing the actual node value
```print(newBinaryTree.getLeftChild().getRootValue())```
### ELABORATE:  If you want the left child node value, you need to use the getRootValue() method to retrieve it

#####################################

# Next.js
- server-side rendering vs client side rendering(React)
- SEO -> when viewing source code on a page, you can actually see the html format of the page
- No need to ask for a request when switching to different routes on the page

# Started with Next.js
- installed node pkg (came with node and npm)
- npm i npx
- npx create-next-app (name)
- npm run dev => runs on localhost:3000



