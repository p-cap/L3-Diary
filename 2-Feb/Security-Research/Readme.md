As I was downloading ``` npm install @material-ui/core ```, npm mentioned a critical vulnerability

```
>>> npm audit
                                                                                
                       === npm audit security report ===                        
                                                                                
┌──────────────────────────────────────────────────────────────────────────────┐
│                                Manual Review                                 │
│            Some vulnerabilities require your attention to resolve            │
│                                                                              │
│         Visit https://go.npm.me/audit-guide for additional guidance          │
└──────────────────────────────────────────────────────────────────────────────┘
┌───────────────┬──────────────────────────────────────────────────────────────┐
│ High          │ Prototype Pollution                                          │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Package       │ immer                                                        │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Patched in    │ >=8.0.1                                                      │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Dependency of │ react-scripts                                                │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Path          │ react-scripts > react-dev-utils > immer                      │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ More info     │ https://npmjs.com/advisories/1603                            │
└───────────────┴──────────────────────────────────────────────────────────────┘
found 1 high severity vulnerability in 1897 scanned packages
  1 vulnerability requires manual review. See the full report for details.

```

I will try to reproduce the critical vulnerability so I can understand why.

Link below shows the POC of the vulnerability.  
https://www.npmjs.com/advisories/1603.  
Next week, I concentrate on this vulnerability



