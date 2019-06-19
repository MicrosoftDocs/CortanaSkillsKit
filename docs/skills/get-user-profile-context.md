---
title: Get the user's profile and contextual information
description: Shows how to get the user's profile and contextual information.

ms.assetid: CE72258E-7934-4B5B-9CE7-15BE3905096C
ms.date: 09/25/2018
ms.topic: article

keywords: cortana
---


# Get the user's profile and contextual information

> [!NOTE]
> This document provides details about obtaining user information for skills built using the Microsoft Bot Framework.
> 


Cortana can send the user's profile and contextual information as part of the message that it sends your skill. You can use this information to provide a custom experience for the user.

User profile information is data that the user provided to Cortana that's stored in Cortana's Notebook. Cortana passes this information to your skill if it's available, and if the user has provided explicit consent to share this information with your skill. _Your skill must have a valid reason to use profile information in order to pass certification._ See [the review guidelines](https://docs.microsoft.com/cortana/skills/skill-review-guidelines) for more details.

User contextual information is information that Cortana has about the user, such as their location.

To receive this information, you must specify the type of user data that you want when you configure your Cortana channel (see [Request user profile data](https://docs.microsoft.com/azure/bot-service/bot-service-channel-connect-cortana?view=azure-bot-service-4.0)).

The following C# code shows how to access the `User.Info.Email` and `User.SemanticLocation.Current` entities. The example assumes that `UserName` and `CurrentLocation` were used as the property (friendly) names during the channel configuration.

```csharp
    var userInfo = turnContext.Activity.Entities?.FirstOrDefault(entity => entity.Type.Equals("UserInfo", StringComparison.Ordinal));
    if(userInfo != null)
    {
        var email = userInfo.Properties.Value<string>("UserEmail");

        if (!string.IsNullOrEmpty(email))
        {
            //Do something with the user's email address.
        }

        var currentLocation = userInfo.Properties["CurrentLocation"];

        if (currentLocation != null)
        {
            var hub = currentLocation["Hub"];

            //Access the latitude and longitude values of the user's location.
            var lat = hub.Value<double>("Latitude");
            var lon = hub.Value<double>("Longitude");

            //Do something with the user's location information.
        }
    }
```

The following example shows the same implementation using JavaScript.

```javascript
    if ( turnContext.activity.entities ) {
       let authEntity = turnContext.activity.entities.find((e) => {
       return e.type === 'UserInfo';
       });
    if (userInfo) {
        let email = userInfo['UserEmail']);

        if(email && email !== ''){
            //Do something with the user's email address.
        }

        let currentLocation = userInfo['CurrentLocation'];
        if (currentLocation && currentLocation.Hub)
        {
            //Access the latitude and longitude values of the user's location.
            var lat = currentLocation.Hub.Latitude;
            var lon = currentLocation.Hub.Longitude;
            //Do something with the user's location information.
        }
    }
}
```
