---  
title: Configure tenant publishing of Cortana Skills for Enterprise | Cortana Skills Kit for Enterprise
description: Configure tenant publishing of Cortana Skill for Enterprise. 

ms.date: 10/11/2018
ms.topic: article
ms.prod: cortana

keywords: cortana
---  

# Configure Tenant Publication  

After your Cortana Skill is ready to be published, you must complete the required fields in the *Tenant Publishing* section.  

![Tenant Publishing - not configured](./media/images/enterprise-tenant_publishing-not_configured.png)  

### Access Configure Cortana Channel  

[!INCLUDE [enterprise-open-configure-cortana](../../includes/enterprise-open-configure-cortana.md)]  

### Update Configure Cortana Channel  

1.  In the *Tenant Publishing* section.  
    1.  Under the *Skill Summary* section.  
        *   `Display Name` | required  
            *   Unique name that Cortana presents to the user.  
                Displayed in Directory, Canvas, and Bing Search.  
        *   `Invocation Name` | required  
            *   Add a descriptive invocation name.  
                
                >[!TIP]
                > For more information about invocation names, visit the [Invocation Name guidelines](../skills/cortana-invocation-guidelines.md) page.  
                
        *   `Short description` | required  
            *   Displayed in the Cortana Notebook.  
        *   `Long description` | required  
            *   Required as part of certification.  
        *   `Sample Invocation Phrase` | required  
            *   Provide at least 3 samples, such as `Hey Cortana, ask Outlook to show my urgent messages`.  
        *   `Primary category` | required  
            *   Ignored for enterprise.  
        *   `Secondary category` | optional  
            *   Ignored for enterprise.  
        *   `Tags` | optional  
            *   Ignored for enterprise.  
        *   `Supported platforms` | required  
            *   Ignored for enterprise. Windows 10 is the only supported platform.  
    2.  Under the *Developer Information* section.  
        *   `Developer Account` | required  
            *   Select `Developer` or `Company`.  
        *   `First name` | required  
            *   First Name of Microsoft Account owner.  
        *   `Last name` | required  
            *   Last Name of Microsoft Account owner.  
        *   `Email` | required  
            *   Developer email.  
        *   `Phone number` | required  
            *   Full Phone Number with extension.  
        *   `Address 1` | required  
            *   Street number, street name, and apartment number.  
        *   `Address 2` | optional  
        *   `City/District` | required  
            *   Enter city/district.  
        *   `State` | required  
            *   Enter state or province.  
        *   `Zip code` | required  
            *   Postal Code.  
        *   `Country` | required  
            *   2-digit Country code, such as `US`, `UK`, `CA`, or `CN`.  
        *   `Developed by (for ISVs)`  
            *   Name of the person who developed the Cortana Skill (if different from Microsoft Account owner).  
        *   `Published by`  
            *   Name of the developer/company who owns the Cortana Skill.  
        *   `Developer or Company Website URL`  
            *   Personal website of the developer or website of the company, such as `https://www.microsoft.com`.  
    3.  Support Contact  
        *   Provide at least one method of communication, either `Email` or `Website`.  
        *   `Email` | required  
            *   Support email.  
        *   `Website URL` | required  
            *   Support website or website of the company, such as `https://www.microsoft.com`.  
    4.  Publisher information (context for enterprise skills?)  
        *   Optional (if different from the developer account information)  
        *   `Name`  
        *   `Email`  
        *   `Phone number`  
            *   Full Phone Number with country code, area code, prefix, and line number, such as `+1 (800) 642-7676`.  
    5.  Privacy policy and terms of use  
        *   `Privacy Policy` | required  
            *   Direct URL link to privacy policy.  
        *   `Terms of Use` | required  
            *   Direct URL link to terms of use.  
    6.  Notices  
        *   As applicable; such as `This Cortana Skill is for entertainment purposes only`, `This Cortana Skill is not associated with XYZ company` or `Currently, this Cortana Skill does not work on Windows Phone`.  
    7.  Validation and testing instructions  
        *   Provide instructions to use your Cortana Skill along with any requirements or information that may assist during validation.  
            
            >[!TIP]
            > *   What your Cortana Skill does, such as order pizza.  
            > *   Limitation with your Cortana Skill, such as support for select regions/states.  
            > *   Additional intents and phrases users may say to launch and run your Cortana Skill.  
            > *   Set up directions, requirements, and credentials for a validation account with your Cortana Skill. Validation accounts should run under any specified scenarios.  
            
>[!NOTE]
> You may save the information and review as part of a change control process before submitting for certification and publishing. You are not able to change the configuration of your Cortana Skill after submission.  

## Next Steps  
