# Requirements for search MEs (user sent cards) to support Universal Actions
1. Specify a bot in the manifest and use the same bot for your ME as well. Specify `"team"` and `"groupchat"` depending on scenarios you plan to support.

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
2. If you need automatic refresh. You have two options -
    1. You can specify user ids in the `userIds` section of the manifest.
    ```json
        {
            "type": "AdaptiveCard",
            
        }
    ```
    2. 
