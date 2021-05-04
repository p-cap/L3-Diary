# YARA 101 

## yara my_first_rule my_first_rule 
- yara 4.1.0 the pattern matching swiss army knife
- my_first_rule
  ```
  rule dummy { 
          condition: true 
     }
  ```
- ```Usage: yara [OPTION]... [NAMESPACE:]RULES_FILE... FILE | DIR | PID```
- OUTPUT: ```dummy my_first_rule```

## using strings
```
text_rule

rule TextExample
{
	strings:
	  $text_string = "test"

	condition:
	  $text_string
}
```
- this rule looks for string "test" inside a file

```
test file

I'm the test inside
```
- ```yara text_rule test```
- OUTPUT: ```TextExample test```
- OUTPUT FORMAT: ```Rule_matched FIle_matched```

## first yara-python
```
first-yara.py

# first yara-python
import yara

# compile the rule first
rules = yara.compile(filepath='./sample_rule')

# opens the file
with open('./sample_file', 'rb') as f:
  matches = rules.match(data=f.read())

# prints out the matches in an array
print(matches)
```

```
sample_rule

rule Sample {
	
  strings:
    $sample_string = "sup"

  condition:
    $sample_string   
}
```
```
sample_file

Wassup????
```
- ```python3 first-yara.py```
- OUTPUT: [Sample]
- OUTPUT ANALYSIS: The output shows an array of triggered rules

## Using callbacks => callback functions should expect a single parameter of dictionary type
```
import yara

## callback function that prints the data in json format
def mycallback(data):
  print(data)
  return yara.CALLBACK_CONTINUE
 
## don't forget.....compile the rule first...not the directory that stores the rulesrules = yara.compile('./myrules/filename_rule')
rules = yara.compile('./callback_rule')

## use match against the file of interest
## setting "which_callbacks" will determine when the callback is called, in this case, when CALLBACK_MATCHES
## Your callback function should expect a single parameter of dictionary type
# utilize the store rule 
matches = rules.match('./callback_file', callback=mycallback, which_callbacks=yara.CALLBACK_MATCHES)
```
```
callback_rule

rule Callback_Rule {
  strings: 
    $callback_string = "findme"

  condition:
    $callback_string

}
```

```
callback_file

cooadnsonaIOCN
CAKNSDKNACSL
XAmksakfindmekaxCXXMamp
```
- OUTPUT: {'matches': True, 'rule': 'Callback_Rule', 'namespace': 'default', 'tags': [], 'meta': {}, 'strings': [(35, '$callback_string', b'findme')]}
- OUTPUT ANALYSIS: This data is great for data analysis
