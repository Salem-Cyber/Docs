| [Docs Home](../../index.md) | [Admin Guide](../adminGuide.md) |

# ReportConf Specification

ReportConf controls how Salem investigations are reported to users and third party systems.  Each configuration is associated with an [ActionDefinition](/docs/confSpec/ActionDefinition.md).

### ID
A name for the configuration

### disabled (0 | 1 | None)
The configuration is disabled when set to 1.  The Configuration is enabled with this value is 0 or not present

### condition list[dict]
Conditions are cases that evaluate if and investigation or incident should be reported.  Each condition is evaluated independently.  Condition objects contain to keys:
* type: "bool" | "regex"
* value:  "bool or regex str"

### ignore_if \<list\>
Accepted list values:
* "duplicate"
* "similar"
* "related"

```
"ignore_if": [
    "duplicate",
    "similar"
]
```

when ignore_if is set to any combination of these values, Salem will not report incidents that are similar or duplicates of other recently reported incidents

### block_threshold \<int\>
The value of block_threshold blocks reporting of new  investigations and incidents when the total number reported in a 24hr period reaches the block_threshold value.  By setting this value to 0, there is no limit on reporting

### params \<dict\>
The params object defines ActionDefinition specific parameters.  Each ReportConf configuration will have a params parameter of 'definition' which associates the ReportConf configuration to an ActionDefinition

#### Webhook report action params
For webhook ActionDefinition's the ReportConf Params will be:
* definition: \<str\>
* inputs \<dict\>
    * values based on the input keys of the ActionDefinition

#### Email report action params
Email report action params
* definition: \<str\>
* send_as: \<str\>
* recipients: \<list\>
* subject: \<str\>
* message: \<str\>

#### Chat report action params
* definition: \<str\>
* role: \<list\>
    * a list of salem roles to receive the report, such as ["salem.analyst"]
* is_group: true | false
    * when true, Salem will try to only report to groups that are set to receive incident notifications and if none are found fall back to reporting to individuals with the identified role(s)