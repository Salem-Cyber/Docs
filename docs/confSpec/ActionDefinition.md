# Action Definition Specification
Action definitions contain base parameters for various contextual and reporting actions.  While you can configure your own action definitions, there are default options available to re-use.  To see current configured action definitions, type 'configure' in Salem Chat and follow the prompt.

There are three types of actions, which are defined in the 'action_type' parameter of a configuration

- chat
- email
- webhook

## chat

chat action is used by [reportConf](/docs/confSpec/ReportConf.md) and other internal processes

## email

Email action type is used by reportConf and by default one email actionDefinition will be defined, called 'Email Notify'. To enable use of this actionDefinition, add a target email server and port. Additionally see the default ReportConf configuration 'default_email_notify'

## webhook
Webhook actionDefinitions allow Salem to interact with third party systems, either as [ActionConf](/docs/confSpec/ActionConf.md) or [ReportConf](/docs/confSpec/ReportConf.md) actions.  There are several default configurations loaded into Salem.  To view type 'configure' into Salem Chat and follow the prompt

### webhook auth
To enable webhook authentication, you need to create a key vault, add a secret and then allow Salem to read that secret.