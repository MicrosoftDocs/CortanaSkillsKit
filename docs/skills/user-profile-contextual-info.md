---
title: Cortana User Profile & Contextual Information Reference
description: Defines the user profile and contextual information objects.
label: Conceptual
ms.assetid: 41f911c9-b5eb-4cd3-b4d9-2dc7453e3f51
ms.date: 02/01/2019
ms.topic: article
keywords: cortana
---

# Cortana user profile and contextual information reference

Cortana sends the user's profile and contextual information as part of the message that it sends your skill. You can use this information to provide a custom experience for the user. User profile information is data that the user has provided about themselves to Cortana. User contextual information is information that Cortana has discovered about the user, such as their current location.  

For information about how you use the objects listed in this reference, see [Get the user's profile and contextual information](get-user-profile-context.md).

## User Profile Entities

These are the types of user profile data that you can request when you configure the Cortana channel.

| Entity Name | Type | Description  
|--|-|-
| User.SemanticLocation.Away | [Away](#away-object) | Indicates whether the user is away from their home or work. 
| User.SemanticLocation.Current | [Visit](#visit-object) | The user's current location. |
| User.SemanticLocation.FrequentPlaces | [Hub](#hub-object)[] | A list of places the user frequents.  
| User.Info.Name | [Name](#name-object)| The user's name. |
| User.Info.Email | string | The user's email address. |


## Away object

Defines whether the user is away from home or work.

| Property | Type | Always included | Description 
|-|-|-|-
| Away | Boolean | Yes | A Boolean value that determines whether the user is away from home or work. If **true**, the user is away from home or work. Otherwise, **false**.
| Since | DateTime | No | The date and time that the user left home or work, in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format.

**Example**

User is not away:

```json
{
    "Away": false
}
```

User is away since April 25th, ‎2017‎ ‎6:‎02‎PM UTC:

```json
{
    "Away": true,
    "Since": "2017-04-25T18:02:00+00:00"
}
```


## Hub object 


Defines a place that the user frequents.

| Property | Type | Always included | Description 
|-|-|-|-
| Id | string | Yes | An ID that uniquely identifies the hub. |
| Type | string | Yes | The type of hub. The following are the possible types:<ul><li>Home</li><li>Work</li><li>Other</li> 
| Name | string | No | A friendly name for the hub that the user typically provides. |
| Latitude | double | Yes | The hub's geographical latitude. |
| Longitude | double | Yes | The hub's geographical longitude. |
| Address | string | No | The hub's address. |

**Example**

```json
{
    "Id":"11111111-1111-1111-1111-11111111111",
    "Type": "Work",
    "Name": "My office",
    "Latitude": 47.61512,
    "Longitude": -122.1957,
    "Address": "500 108th Ave NE, Redmond, WA 98004, USA"
}
```


## Name object

Defines the user's name.

| Property | Type | Always included | Description
|-|-|-|-
| GivenName | string | No | The user's first name. 
| FamilyName | string | No | The user's last name. 

**Example**

```json
{
    "GivenName": "John",
    "FamilyName": "Smith"
}
```


## Visit object

Defines the user's current location.

| Property | Type | Always included | Description 
|-|-|-|-
| StartTime | DateTime | Yes | The date and time the user arrived at the location, in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format. 
| EndTime | DateTime | No | The date and time the user left the location, in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format. 
| Hub | [Hub](#hub-object) | Yes | The user's location. 
| VenueName | string | No | The name of the location if the location is a point of interest.
| Away | [Away](#away-object) | No | Indicates whether the user is away from home or work. |

**Example**

```json
{
    "StartTime": 2017-04-25T18:02:30+00:00,
    "EndTime": 2017-04-27T7:35:00+00:00,
    "Hub": {
        "Id":"11111111-1111-1111-1111-11111111111",
        "Type": "Work",
        "Name": "My office",
        "Latitude": 47.61512,
        "Longitude": -122.1957,
        "Address": "500 108th Ave NE, Bellevue, WA 98004, USA"
    }
    "VenueName": null,
    "Away": {
        "Away": true,
        "Since": "2017-04-25T18:02:00+00:00"
    }
}
```
