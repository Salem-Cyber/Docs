# Configuration Home
Salem configures files control how Salem will process and analyze alerts.  Configuration include instruction for alert parsing, context extraction, incident reporting and other key Salem functions.

## Action Conf
Action Conf controls how Salem interprets and collects alert context

## Action Definitions
Action Definitions are high level action classes that are referenced by Action and Reporting actions.  These Definitions describe how Salem connections to third party systems for context and reporting actions.

## Parsing Conf
Parsing Conf defines how Salem will process and extract information from new alerts.  Parsing can be defined on default (all alerts), source and alert scopes allowing fine control over parsing of alerts using different data structures

## Report Conf
Report Conf controls how Salem sends notifications regarding alert analysis.  Salem is pre-configured to send incident notifications to chat.  Notifications can also be sent to third party systems.