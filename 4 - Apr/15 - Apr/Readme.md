### Gets the SHA256 hash of a file and compares it with the file that is downloaded from the site


```
  1 import subprocess
  2 import sys, getopt
  3 
  4 file = ''
  5 hashfile = ''
  6 
  7 opts, args = getopt.getopt(sys.argv[1:], "hf:t:")
  8 
  9 if (sys.argv[1:] == []):
 10    print("Usage: verify-sha256.py -f <filename> -t <hashfile>")
 11 
 12 for opt, arg in opts:
 13    
 14    if opt == "-h" or arg == " ":
 15       print("Usage: verify-sha256.py -f <filename> -t <hashfile>")   
 16       sys.exit()
 17    
 18    elif opt == "-f":
 19       file = arg
 20 
 21    elif opt == "-t":
 22       hashfile = arg
 23 
 24 shasum_output = subprocess.run(["shasum", file, "-a",  "256", "-c", hashfile], c    apture_output=True, text=True)
 25 
 26 arr = shasum_output.stdout.split("\n")
 27 
 28 for i in arr:
 29    if i.find("OK") > 0:
 30       print(i) 
```
