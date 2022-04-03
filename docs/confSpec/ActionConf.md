# ActionConf Specification
ActonConf controls the Salem actions that add contextual information to alert.

To view current action configurations type 'configure' into Salem Chat

### id \<str\>
A descriptive name

### cost \<int\>
Valid values : 0 | 1 | 2
Cost controls when a action is run.  When an action cost is set to zero it will run if the alert contains the required fields.  When set to 1 or 2, the action is only run when salem specifically wants to know the context that is returned by that action.  Typically cost 2 is used for webhook actions.

### requires list[dict]
Defines the alert fields and context required for this action to run.  One or more requirements can be added, and each will be evaluated independently

```
"requires": [
    {
        "fields": [
            "file"
        ],
        "context": {
            "contains": ["data.malicious"],
            "excludes": []
        }
    }
]
```

### returns \<list\>
A list of alert context tags to add to the alert if the action evaluates to true.  In many cases it's best to provide the full context string, such as 'action.blocked', however if the requires field is 'account','src_account','src','dest','program' or 'parent_program', you can provide a return context string with only the trailing tag portion, such as: 'windows'.  Assuming the requires field is 'dest', the returned context would be 'dest.windows'

Custom context tags can be applied, but may not contribute directly to the threat score.

### params \<dict\>
A dictionary of parameters specific to the action type.  See action types for overview of params values

### action_type \<str\>
supported values:
* match
* webhook

#### match
match actions evaluate to true or false.  When true, the return context is applied to the alert.  The match action is evaluated against the fields listed in required fields object

##### match params
For match actions valid params object should include one of the following key values pairs:
* beginsWith: \<str\>
* bool: \<str\>
* contains: \<str\>
* endsWith: \<str\>
* in: \<list\>
* regex: \<str\>

```
"params": {
    "endsWith": "_svc"
}

"params": {
    "in": [200,201,202]
}

"params": {
    "bool": "src and dest"
}
```

#### webhook
Webhook actions call an external http endpoint and evaluate the response.  

##### webhook params
##### definition \<str\>
The [ActionDefinition](/docs/confSpec/ActionDefinition.md) configuration to use for this webhook action

##### input \<dict\>
The inputs values are defined in the ActionDefinition input_keys parameter

##### outputs list[dict]
Output objects control how the results of the webhook are evaluated.  Each object contains:
```
"outputs": [
    {
        "condition": {
            "type": "bool" | "regex",
            "value": "bool or regex str"
        },
        "outcome": {
            "type": "context" | "field",
            "value": [
                "context tag or field value"
            ]
        }
    }
]
```