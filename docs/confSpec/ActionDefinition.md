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

To Add credentials to an action definition, update the "credentials" object of the ActionDefinition.
* `user` is the user name used to authentication Salem to a third party system
* `secret_name` is the name of a secret in a key vault that contains the credential used to access a third party system
* `vault_url` is the FQDN (ex: `https://vaultName.vault.azure.net`) of the key vault where the secret is stored
    * Configure a key vault for Salem to access [here](../guides/configureSecrets.md)