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
with open('./test', 'rb') as f:
  matches = rules.match(data=f.read())

# prints out the matches in an array
print(matches)
```
- ```python3 first-yara.py```
- OUTPUT: [Sample]
- OUTPUT ANALYSIS: The output shows an array of triggered rules


