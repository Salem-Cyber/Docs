| [Docs Home](../../index.md) | [Admin Guide](../adminGuide.md) |

# ParsingConf Specification

ParsingConf controls how data is extracted from raw alerts and stored as parsed alert data.  Parsing Configurations come in three types:

| Type | id | source | Description |
| -- | -- | -- | --| 
| Default | default | default | The default configuration is the configuration that comes out of the box with Salem |
| Source | \<source\> | \<source\> | A parsing configuration specific to an alert source.  Source configuration items override default configurations items of the same name |
| Alert | \<alert_name\> |\<source\> | A parsing configuration specific to an alert name and source. These configurations take president over other configuration items of the same name defined at the source and default level |

### parsing: auto | kv | json
Defines how raw alerts are going to be extracted.  The default is 'auto' which will try to detect if the raw event is in json format or KV format

### kv_regex: \<str\>
Defines a regex string used to extract key value pairs in a raw alert text.  This value is ignored if parsing is set to 'json'

### time_regex: \<list\>
Defines a list of regex strings used to extract a time stamp from raw event data.  Salem will keep testing each regex string against the alert text until either a match is found or no match is found.

## Field Transformations
There are 3 types of field transformations and they are processed in the following order:
* alias
* evals
* lookups

### alias: \<dict\>
A dictionary were a key represent a field extracted from the alert data and value represent a new field name to set as an alias for the existing field name

```
# Alias Example
"alias": {
    "s": "src",
    "source": "src"
}
```
In the above example there are several fields that alias to 'src'.  These alias are processed from top down, meaning if 's' and 'source' both exist in the alert data, the value of 'src' will be set to the value of 'source'

### evals: \<dict\>
A dictionary of eval dictionaries.  Each eval key value is a name and the value is a dictionary containing two keys: field and eval.  Field should be set to the field name that will be set with the output of the eval statement.  The eval statement should contain an eval string that returns a value to be set.

```
"evals": {
    "file_path": {
        "field":"file_path",
        "eval": "if_then(match('regex',r'[\\\\]',file),join(split(file,'\\\\')[0:-1],'/') + '/',if_then(match('regex',r'[/]',file),join(split(file,'/')[0:-1],'/') + '/',None))"
    },
    "file": {
        "field":"file",
        "eval": "if_then(match('regex',r'[\\\\]',file),split(file,'\\\\')[-1],if_then(match('regex',r'[/]',file),split(file,'/')[-1],file))"
    }
}
```

#### eval actions
#### bool(exp)
Evaluates to true or False

#### len(obj)
Returns the length of the object provided

#### round(num,pos)
Returns a num rounded to pos digits

#### coalesce(*args)
Returns the first non null value

#### if_then(bool,true,false)
If the bool statement evaluates to true, the value of the true case is returned, otherwise the value of the false case is returned

#### join(list,str)
Returns a string comprised of the list values concatenated by the value of str

#### match(type,match_exp,match_field)
Returns True or False based on the evaluation of the match expression.  

Match types:
* in
* beginsWith
* endsWith
* contains
* regex
* bool

```
match('endsWith','.com',src)
```

#### now(seconds)
Returns a date object that is the current utc time offset by the value of seconds

#### rex(exp,str)
returns a match value based on the regex exp evaluated over str

#### split(str,exp)
returns a list of str components split by the value of exp

```
split('10.0.0.1','.')
# returns: [10,0,0,1]
```

#### strftime(time,format)
Accepts a datetime object and a time format string.  Returns a str representing time in the format provided 

#### strptime(str,format)
Accepts a time str and format, and returns a datetime object

#### to_dict(json_str)
Accepts a json formatted string and returns an object

#### to_json(obj)
Accepts and object and returns a json formatted string

#### to_str(obj)
Accepts an object and returns a str formatted version of that object

#### url_decode(url_string)
Accepts a url quoted string and returns a unquoted version

#### url_encode(str)
Accepts a string and returns a url quoted version of that string

### lookups
A dictionary of dictionaries. Each lookup item has a name key and a dictionary value with keys:
* table
* key
* type
* return

Typically table should be set to 'defaultParsingLookup', and type set to 'parsed'.  Key is the field being looked up and return is the value returned if available in the lookup table.

```
"lookups": {
    "dest_ip": {
        "table": "defaultParsingLookup",
        "key": "dest",
        "type": "parsed",
        "return": "dest_ip"
    }
}
```