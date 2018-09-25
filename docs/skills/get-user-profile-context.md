---
title: Get the user's profile and contextual information
description: Shows how to get the user's profile and contextual information.
ms.assetid: CE72258E-7934-4B5B-9CE7-15BE3905096C
ms.date: 05/03/2018
ms.topic: article
keywords: cortana
---


# Get the user's profile and contextual information

> [!NOTE]
> This documentation provides details around obtaining user information for skills built using the Microsoft Bot Framework.
> 


Cortana can send the user's profile and contextual information as part of the message that it sends your skill. You can use this information to provide a custom experience for the user. User profile information is data that the user provided to Cortana and is found in Cortana's Notebook. This is information is fairly stable and is editable by the user. Cortana passes this information to your skill if it's available, and the user has provided explicit consent to share this information with your skill. 

User contextual information is information that Cortana has discovered about the user and changes more frequently such as their location. The Notebook also contains this information, but the user typically can't edit it.

To receive this information, you must specify the type of user data that you want when you configure your Cortana channel (see [Request user profile data](https://docs.microsoft.com/bot-framework/channel-connect-cortana#request-user-profile-data)).

For each piece of user data that you request, you specify a friendly name that identifies that piece of data. Cortana uses the friendly name as the property name in the `UserData` object. For information about the types of profile and contextual information that's available, see [User Profile Reference](user-profile-contextual-info.md).

<!-- This doesn't seem right. The name is entities which is plural so you'd think it's an array of entities, one of which might be UserData. Confirm. -->

Each message contains an `entities` field, which is an array of objects. One of the objects is a `UserData` object with the following properties:


| Name | Type | Description 
|-|-|-
| friendlyName1..n | object | The user profile or contextual information that you requested. The `friendlyName1..n` name is a placeholder for the names you used when you configured the Cortana channel. For information about the objects associated with the data you requested, see [User Profile Reference](user-profile-contextual-info.md).
| type | string | The object's type, which is set to UserInfo. 


The following shows an example of the `UserInfo` object.

```json
{                   
    "type": "UserInfo",  
    "FriendlyName1": {}  
    "FriendlyName2": {}  
}
```

If you request profile or contextual data that's not available for the user, the property's value is an empty string or null. 

The following example shows accessing the `User.Info.Email` and `User.SemanticLocation.Current` entities using C#. The example assumes "UserName" and "CurrentLocation" were used as the property (friendly) names during the channel configuration.

```csharp
if (activity.Entities != null)
{
    var userInfo = activity.Entities.FirstOrDefault(e => e.Type.Equals("UserInfo"));
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
}
```

The following example shows the same implementation using Node.js.

```javascript
if(session.message && session.message.entities){
    var userInfo = session.message.entities.find((e) => {
        return e.type === 'UserInfo';
    });

    if (userInfo) {
        var email = userInfo['UserEmail']);

        if(email && email !== ''){
            //Do something with the user's email address.
        }

         var currentLocation = userInfo['CurrentLocation'];

        if (currentLocation)
        {
            //Access the latitude and longitude values of the user's location.
            var lat = currentLocation.Hub.Latitude;
            var lon = currentLocation.Hub.Longitude;

            //Do something with the user's location information.
        }
    }
}
```


