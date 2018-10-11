---
title: Create Your Bot from Template | Cortana Skills Kit for Enterprise
description: Build your bot using a template. 

ms.date: 10/09/2018
ms.topic: article
ms.prod: cortana

keywords: cortana
---

# Create Your Bot from Template  

Create Cortana Skills using C\# or Node.js. There are two versions of the bot building SDK available, V3 and V4, and many templates exist using V3.  

>[!NOTE]
> The number of templates are growing as Cortana migrates to Bot Framework V4.  

At the timing of writing, you may create bots using Bot Framework SDK V3 or V4.  

The differences between the versions.  
1.  V4 supports java and python.  
2.  Closer parity between all language platforms.  
3.  Middleware is refactored to create plugins accessible by multiple bots.  
4.  OAuth has changed from entities to events.  

However, Cortana Skills are currently supported in C\# and Node.js with templates and examples in those languages.  

The following templates exist for V3 and great to get you building quickly.  
1.  A basic echo bot  
2.  A question and Answer bot  
    *   Use the [QNA Maker](https://www.qnamaker.ai) tool that allows easy import of common text formats.  
1.  A LUIS (language understanding) bot  
    *   Build natural language models easily with the [Language Understanding (LUIS)](https://www.luis.ai) tool.  
        Integrate your models with your bot to get intents, entities, and rankings.  
1.  A form bot  
    *   Use form flow and the form builder class.  
        
        >[!NOTE]
        > The formbuilder is semantically different in V3 between C\# and Node.js.  
        
5.  A proactive bot for handling external events.  
    *   >[!IMPORTANT]
        > Proactive bots are currently not supported by Cortana skills.  

Cortana supports building responsive interfaces that look great on any surface with the [Adaptive Cards](http://adaptivecards.io) tool.  

>[!NOTE]
> The examples are bot framework specific.  
> For all cases you must add a line of code to enable Cortana speech.  
>
> >[!TIP]
> > To message objects replace `session.send( 'text' )` with `session.say('text','speech')` or `add.speak('speech')`.  

As Cortana Skills Kit evolves, Microsoft provides speech-enabled templates through Azure and github.  

## Next Steps  
