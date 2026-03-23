# CCS Grammar (EBNF)
## Version 0.1.1

This document defines the minimal grammar for the Cognitive Component Specification (CCS) format.

```
ccs          = header, core, governance, layers, agents ;

header       = "system_id", ":", string,
               "version", ":", string ;

core         = "core", ":", indent,
                 "purpose", ":", string,
               dedent ;

governance   = "governance", ":", indent,
                 "policies", ":", indent,
                   policy, { policy },
                 dedent,
               dedent ;

policy       = identifier, ":", ( number | string ) ;

layers       = "layers", ":", indent,
                 layer, { layer },
               dedent ;

layer        = "-", indent,
                 "id", ":", string,
                 "name", ":", string,
                 "description", ":", string,
               dedent ;

agents       = "agents", ":", indent,
                 agent, { agent },
               dedent ;

agent        = "-", indent,
                 "id", ":", string,
                 "role", ":", string,
                 "capabilities", ":", indent,
                   string, { string },
                 dedent,
                 "limits", ":", indent,
                   limit, { limit },
                 dedent,
               dedent ;

limit        = identifier, ":", ( number | boolean ) ;

string       = quoted text ;
number       = integer or float ;
boolean      = "true" | "false" ;
identifier   = alphanumeric token ;
indent       = increase indentation ;
dedent       = decrease indentation ;
```
