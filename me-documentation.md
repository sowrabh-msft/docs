# Requirements for search based MEs to support Universal Actions

In addition to requirements for supporting Universal Actions ==(TODO: insert link here)==, you need to provide the below in your bot.

Specify a bot in the manifest and use the same bot for your ME as well. Specify `"team"` and `"groupchat"` depending on scenarios you plan to support.

    ```json
    {
        "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
        "manifestVersion": "1.11",
        "version": "1.0.0",
        "id": "%MICROSOFT-APP-ID%",
        "packageName": "com.example.myapp",
        "bots": [
            {
                "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
                "scopes": [
                        "team",
                        "personal",
                        "groupchat"
                    ]
            }
        ],
        "composeExtensions": [
            {
                "canUpdateConfiguration": true,
                "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%", // Use the same bot as what is specified in the bots section above
            }
        ]
    }
    ```

Also see **Automatic Refresh for Adaptive Cards in search based MEs** section below.

# Just In Time Install 
In order to support Universal Actions in search based Message extensions, your bot will be added to the conversation where the card is sent by the user. The following will be the flow for a user sending card:

==**TODO: below screenshots need to be updated to show a non-Dynamics scenario**==

![](Media\Slide2.jpg)

![](Media\Slide3.jpg)

![](Media\Slide4.jpg)


# Automatic Refresh for Adaptive Cards in search based MEs        
If you need automatic refresh. You have two options -
    1. You can specify user ids in `userIds` property in `refresh` section of the card. User Ids need to be provided in either `29:<ID>` or `8:orgid:<AAD ID>` format for automatic refresh.

        ```json
        {
            "type": "AdaptiveCard",
            "refresh": {
                "userIds": [
                    "<8:orgId:<AADID>>",
                    "29:<id>"
                ],
                "action": {
                    "type": "Action.Execute",
                    "data": {}
                }
            },
            "body": [
                {
                    "type": "TextBlock",
                    "text": "Hello World!",
                    "wrap": true
                }
            ],
            "actions": [
                {
                    "type": "Action.Execute",
                    "data": {},
                    "title": "Hello"
                }
            ]
        }
        ```  

    2. Skipping userIds would enable refresh for everyone in the group chat/channel with size <= 60. For conversations (group chat/channel) of size more than 60, automatic refresh would not be enabled and users will be provided with an option to refresh manually from the message options menu.
     
        ```json
        {
            "type": "AdaptiveCard",
            "refresh": {
                "action": {
                    "type": "Action.Execute",
                    "data": {}
                }
            },
            "body": [
                {
                    "type": "TextBlock",
                    "text": "Hello World!",
                    "wrap": true
                }
            ],
            "actions": [
                {
                    "type": "Action.Execute",
                    "data": {},
                    "title": "Hello"
                }
            ]
        }
        ```
