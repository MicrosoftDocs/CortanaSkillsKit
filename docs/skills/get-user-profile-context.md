---
title: Get the user's profile and contextual information
description: Shows how to get the user's profile and contextual information.

ms.assetid: CE72258E-7934-4B5B-9CE7-15BE3905096C
ms.date: 06/27/2019
ms.topic: article

keywords: cortana
---

# Get the user's profile and contextual information

> [!NOTE]
> This document provides details about obtaining user information for skills built using the Microsoft Bot Framework.

Cortana can provide the user's profile and contextual information as part of the data that it makes available to your skill. You can use this information to build a custom experience for the user.

User profile information is data that the user provided to Cortana that's stored in Cortana's Notebook. Cortana passes this information to your skill if it's available, and if the user has provided explicit consent to share this information with your skill. _Your skill must have a valid reason to use profile information in order to pass certification._ See the [Skill review guidelines](https://docs.microsoft.com/cortana/skills/skill-review-guidelines) for more details.

User contextual information is information that Cortana has about the user, such as their location.

To receive this information, you must specify the type of user data that you want when you configure your Cortana channel (see the *Request user profile data* section in the [Connect a bot to Cortana](https://docs.microsoft.com/azure/bot-service/bot-service-channel-connect-cortana?view=azure-bot-service-4.0)) page.

The sample code shows how to access `userInfo.Properties` in order to retrieve the user's email address (which is profile info) and location (which is contextual info). The examples assume that `UserEmail` and `CurrentLocation` were used as the property's friendly names during the channel configuration.

# [C#](#tab/cs)

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

# [JavaScript](#tab/js)

```javascript
<<<<<<< HEAD
    var userInfo;
    if ( turnContext.activity.entities ) {
       userInfo = turnContext.activity.entities.find((e) => {
=======
    if ( turnContext.activity.entities ) {
       let authEntity = turnContext.activity.entities.find((e) => {
>>>>>>> 8b936453edc7eb9db220cef1a6779f6533b0df8f
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

---