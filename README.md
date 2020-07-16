# Microsoft Teams Steps

These steps allow you to Create a Meeting, Delete a Channel, Invite a user to a channel, and Get Messages from a Channel.


---------

<kbd>
<a href="https://support.xmatters.com/hc/en-us/community/topics">
   <img src="https://github.com/xmatters/xMatters-Labs/raw/master/media/disclaimer.png">
</a>
</kbd>

---------

# Files

* [MicrosoftTeamsSteps.zip](MicrosoftTeamsSteps.zip) - Workflow zip file with the step and example flow

# How it works
These steps use the [Microsoft Graph API](https://docs.microsoft.com/en-us/graph/overview?view=graph-rest-1.0) in order to perform different operations.

The `MS Teams - Invite to Channel` and `MS Teams - Get Channel Messages` steps use the beta version of the API.

# Installation

## Microsoft Teams Setup
None. This requires access to Microsoft Teams in order to be useful, so you'll need a Microsoft account.

## xMatters Setup
1. Download the [MicrosoftTeamsSteps.zip](MicrosoftTeamsSteps.zip) file onto your local computer
2. Navigate to the Workflows tab of your xMatters instance
3. Click Import, and select the zip file you just downloaded
4. Create a new endpoint of type **Microsoft Graph API** and connect your Microsoft account.


## Usage
There are many steps included with this workflow. The **Get Channel Messages** and **Beautify Chat** steps are meant to be used in conjunction in order to make the text usable in an xMatters event.

This workflow contains the following steps:
- MS Teams - Create Conference Bridge
- MS Teams - Delete Channel
- MS Teams - Invite to Channel
- MS Teams - Get Channel Messages
- MS Teams - Beautify Chat

---
## MS Teams - Create Conference Bridge

### Inputs
| Name  | Required? | Min | Max | Help Text | Default Value | Multiline |
| ----- | ----------| --- | --- | --------- | ------------- | --------- |
| Subject | No | 0 | 2000 | Subject of meeting. | | No |
| Start of Meeting | No | 0 | 2000 | Start time for the meeting. If left empty, the meeting will start immediately. Represented like (2020-07-20T13:46:29-04:00 or 2020-07-20T17:46:29Z). You can join a meeting before it has started, so this value doesn't appear to have much purpose. | | No |
| Length of Meeting | No | 0 | 2000 | Length of meeting in minutes. If left empty it will default to 60 minutes. The meeting does not seem to terminate when over, so this value shouldn't matter. | | No |


### Outputs

| Name | Description |
| ---- | ----------  |
| creationDateTime | Time the meeting was created |
| startDateTime | Time the meeting is set to start at |
| endDateTime | Time the meeting is set to end at |
| joinUrl | The join URL for the meeting |
| joinWebUrl | Not exactly sure what this is. Seems to be the same as **joinUrl** |

---
## MS Teams - Delete Channel

### Inputs
| Name  | Required? | Min | Max | Help Text | Default Value | Multiline |
| ----- | ----------| --- | --- | --------- | ------------- | --------- |
| Team | Yes | 0 | 260 | Name or ID of the Team the channel is to be deleted inside. | | No |
| Channel Name | Yes | 0 | 50 | The name of the channel to be deleted. | | No |


### Outputs

| Name | Description |
| ---- | ----------  |
| ok | if the step succeeded |
| message | message about any issues |

---
## MS Teams - Invite to Channel

### Inputs
| Name  | Required? | Min | Max | Help Text | Default Value | Multiline |
| ----- | ----------| --- | --- | --------- | ------------- | --------- |
| Team | Yes | 0 | 260 | Name or ID of the Team the channel is in. | | No |
| Channel Name | Yes | 0 | 50 | The name of the private channel to add the user(s) to. | | No |
| Users | Yes | 0 | 2000 | A comma-separated list of users to add to the channel. Can be their display names, emails, or ids. | | No |

---
## MS Teams - Get Channel Messages

### Inputs
| Name  | Required? | Min | Max | Help Text | Default Value | Multiline |
| ----- | ----------| --- | --- | --------- | ------------- | --------- |
| Team | Yes | 0 | 260 | Name or ID of the Team the channel is in. | | No |
| Channel Name | Yes | 0 | 50 | The name of the channel to get the messages from. | | No |
| Get Apps | Yes | 4 | 5 | Whether to include (true) or exclude (false) any apps or bots. | true | No |
| Include Replies | Yes | 4 | 5 | This will include replies to messages. Preferably this is not used, as for large quantities of messages, it will take a long time. | false | No |
| Blacklist | No | 0 | 2000 | A comma-separated list of users or bots to ignore messages from. Can be either ids or display names. | | No |
| Max Messages | No | 0 | 2000 | The max number of messages to get. By default this is 100. The output for messages can only support 20,000 characters, so larger values may not work as expected. | 100 | No |


### Outputs

| Name | Description |
| ---- | ----------  |
| messages | A List of messages sorted in chronological order |
| replies | A map of message ids to all their replies |

---
## MS Teams - Beautify Chat

### Inputs
| Name  | Required? | Min | Max | Help Text | Default Value | Multiline |
| ----- | ----------| --- | --- | --------- | ------------- | --------- |
| Messages | Yes | 0 | 20000 | Messages from the "MS Teams - Get Channel Messages" step. | | No |
| Replies | No | 0 | 20000 | Replies from the "MS Teams - Get Channel Messages" step. | | No |


### Outputs

| Name | Description |
| ---- | ----------  |
| html | HTML output for use in an xMatters event. |


## Example
This is an image of the flow included with this repository.

<kbd>
	<img src="/media/ExampleFlow.png">
</kbd>

