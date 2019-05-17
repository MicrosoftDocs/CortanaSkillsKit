---
title: Building hybrid user interfaces
description: Describes the process for approving or rejecting third-party Cortana devs.
label: Conceptual

ms.date: 05/17/2019
ms.topic: article
ms.author: v-daturc@microsoft.com

keywords: cortana
---

# Building hybrid user interfaces

A hybrid user interface is one where two or more modes of communication are used to accomplish a task. In the 90s, this term was used to describe how to blend a Graphic User Interface with a Command Line Interface. Today it describes how to blend a Voice Interface with either a Graphical Interface or Textual Interface or both.

Chat bots use a textual interface. You can supplement the conversations with rich cards – adding graphical elements. These elements can extend beyond simple display elements, including input controls. You may ask, "What is best way to implement a hybrid voice, graphical, and text experience?" The answer lies in identifying what the primary experience is and what its goals are.

## Cortana as the Primary Experience

If you are designing for voice first, you should read the [Principles of Cortana skills design](https://docs.microsoft.com/en-us/cortana/skills/design-principles) page.

To summarize the goals, you pick a voice experience when

- It's more natural to interact with voice.
- The user’s hands are busy, and/or you want to support multitasking.
- The voice experience is more effective and/or efficient.

Your interactions should be efficient, relevant, clear, and trustworthy. Keep your questions simple and concise. When presenting options to the user, ask in a way that makes it clear to the user that it is an either/or question. Limit the list of options to three entries and state all options clearly.

When possible, use directed prompts and let the user pick from a short list of options. Try to break down a conversation into a series of steps with a few succinct actions. Or, if there are too many choices (more than three), use an open prompt. Say what you want to do, and discern the users intent.

Keep in mind that voice-driven interfaces are also inclusive interfaces. It may be helpful to review the [Designing inclusive software for Windows 10](https://docs.microsoft.com/en-us/windows/uwp/design/accessibility/designing-inclusive-software) guidelines.

*Use case: Where do you want to go?*
*A user would like to fly from A to B. Instead of presenting the user with long lists of potential sources and destinations, just ask: "Where are you coming from?" and "Where do you want to go?".*

## The design process

Building a great Cortana skill that meets the voice design goals means having a clear picture of how the problem you are trying to solve fits with the voice-enabled solution. We’ve borrowed some concepts from Process Re-engineering: Identify. Review. Design. Test.

1. Define the existing process or problem you want to simplify or optimize with Cortana
1. Design the conversation / Design the improvement plan that is fit-for-purpose
1. Define the success or performance metrics
1. Supplement the conversation with supporting visuals where they make sense
1. Perform a Usability study / Test and Experiment
1. Refine the experience based on feedback

When designing conversations, apply "role play" or "script" writing to your user stories and use cases (scenarios). For example, if you're familiar with user stories, keep this one in mind: *As a first-time skill user, I can invoke the skill and get help easily, without having to leave the conversation*.

A sample conversation might go like this:

>**First time user:** Open MySkill.  
>**MySkill:** Hello! It looks like this is your first time using MySkill. Try saying "Perform action one" or "Perform action two." You can get more help at any time by saying "Help me."

As a suggestion for designing successful conversations, think about these questions. Is the conversation:

- Efficient?
- Relevant?
- Clear?
- Trustworthy?

Does the dialog allow the user to correct or cancel an activity gracefully? Can the user get contextual help easily? Can they get feedback, or a summary of where you are in the conversation?

## When to use rich cards

Visual elements should be used to support your skill. Ideally, conversations should stand alone. See the design tips in the [Design your skill's visual elements](https://docs.microsoft.com/en-us/cortana/skills/design-principles#card-design-tips) section of the [Principles of Cortana skills design](https://docs.microsoft.com/en-us/cortana/skills/design-principles) page.

The card should, in general, not provide any new information to the conversation.

The skill should support a voice interaction even when a rich card is displayed (remember: not all Cortana devices have screens, and the goal it to design interactions that are hands-free).

If you find yourself presenting the end-user with a form that has multiple input controls, you may want to ask yourself why you're building this interface for a Cortana skill. Cortana supports deep linking to apps and web pages that may be better suited to form input, and the minimal screen real-estate provided by Cortana provides very little room. Use the goals above to stay focused on your hybrid design.

### Example: Form auto-population

The end user wants to create a pre-populated form. The form itself has tens of fields and options. So, the end user asks the Cortana skill to create a form that is populated from a template, or clone their most recent form entered, or to create a form based on the most recent or frequent inputs. Cortana creates the form, and presents the end user with a deep link into the system to view the form, and/or notifies the user via email with a deep link into the system to view the form.

## Being a bot – support short conversations

A good conversation should work similarly on text and by voice (as the voice component is transcribed into text). Although these docs are not directly related to Cortana, some of the Azure Bot Service documentation might be helpful:

- [Principles of bot design](https://docs.microsoft.com/en-us/azure/bot-service/bot-service-design-principles?view=azure-bot-service-4.0)
- [Design and control conversation flow](https://docs.microsoft.com/en-us/azure/bot-service/bot-service-design-conversation-flow?view=azure-bot-service-4.0)
- [Design the user experience](https://docs.microsoft.com/en-us/azure/bot-service/bot-service-design-user-experience?view=azure-bot-service-4.0)

Using a bot to automate tasks or answer questions should make the task easier, not more complicated.

Where procedural conversation flow is required (directed prompts), make it as simple as possible.

A well-designed bot will have a conversation flow that feels natural. The bot should be able to handle the core conversation seamlessly and handle interruptions gracefully (for example, if the user switches to a new topic).

## Using buttons, choices, and links

Displaying buttons from rich cards should follow the general guidance on buttons:

- [Command Buttons](https://docs.microsoft.com/en-us/windows/desktop/uxguide/ctrl-command-buttons)

Buttons should be used to confirm actions.

Options should be spoken, and recognized as voice input on a conversation, to keep a consistent voice experience.

If you decide to give your users the option of responding in a screen, would a combination of radio buttons and generic command buttons be a better choice? Often radio buttons are used in conjunction with generic command buttons (`OK`, `Cancel`) in place of a set of specific command buttons when any of the following are true:

- There are five or more possible actions.
- Users need to view additional information before making a decision.
- Users need to interact with the choices (perhaps to see additional information) before making a decision.
- Users view the choices as options instead of different commands.

As our applications are also responsive (and mobile first), you might also consider reviewing Universal Windows Platform (UWP) control patterns.

[UI basics for Universal Windows Platform (UWP) apps](https://msdn.microsoft.com/en-us/library/windows/apps/dn958432.aspx?f=255&MSPPError=-2147217396)

Guidance specific to buttons:

[Buttons](https://docs.microsoft.com/en-us/windows/uwp/design/controls-and-patterns/buttons)

The summary:

- Use a button to let the user initiate an immediate action, such as submitting a form.
- Don't use a button when the action is to navigate to another page. Use a HyperlinkButton instead. See [Hyperlinks](https://docs.microsoft.com/en-us/windows/uwp/design/controls-and-patterns/hyperlinks) for more info.  

    Adaptive Cards do not support HyperlinkButtons, but you can use link markup in the text block. Or, simply use link markup in the message (activity) text. This lets the user know that they are leaving the conversation and the client application.

    Visit [Adaptive Cards Overview](https://docs.microsoft.com/en-us/adaptive-cards/) for more details.

## From bot to assistant – follow up

When a user gets a response (for example, a link) that takes them away from the conversation, consider saving the state of conversation such that if the user returns in a short amount of time that they can pull up their previous state without having to navigate to it again.

Maintaining state across conversations allows the end user to change devices or try something out without blocking on the conversation.

You also have the opportunity to gather performance metrics on the previous results.

### Example: Support ticket follow-up

The user created a support ticket from a template using Cortana. The skill queries for a state change on the ticket, such that the user does not need to remember the ticket number, and notifies the user the next time they invoke the skill.

*Use case: Search follow-up*
*The user searched a knowledge base for help. He/she followed the links and followed the procedure, but it was not applicable. He/she invokes the skill again shortly after, and is asked if the previous results answered the question. A negative response continues the search, or allows the user to escalate to live help or filing a support ticket.*

>**Returning user:** Open MySkill.  
>**MySkill:** Welcome back. Did that link help you with your question?  
>**Returning user:** No.  
>**MySkill:** Would you like to ‘search again’, ‘chat with a live agent’, or ‘open a support ticket’?

## Dealing with large amounts of data

Bots and voice skills are not designed to relay a lot of information. If the user needs to scroll to see all of the information you're trying to display, you’ve presented too much data.

However, for some applications, you can't avoid presenting a lot of information. Consider refactoring your conversation to so that it returns the information differently.

- **Refine the search results:** Return less data.
- **Return the top N results:** For voice, we recommend N <= 3.
- **Paginate results:** Use Carousel layouts where supported, or procedural steps to navigate N results at a time.
- **Delegate viewing of results elsewhere:** For example, ask if the user wants all the results emailed to them, or provide a link to a service that can render all the results.

Refining the search result is usually the best way to optimize the user’s time.

*Use case: A user wants to know what international holidays might affect a product launch.*
*On the desktop, you might forward the user to a web page that displays a table of holidays. For Cortana, it's better if you focus on the answer, as shown below.*

>**User:** What holidays are within 30 days of July 15?  
>**MySkill:** There are 12 international holidays within 30 days of July 15. Would you like me to list them all, review them by country, or review by type of holiday?  
>**User:** What are the US holidays?  
>**MySkill:** July 4 is Independence Day in the United States. It is a statutory national holiday.