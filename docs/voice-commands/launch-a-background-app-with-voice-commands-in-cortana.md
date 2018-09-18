---
title: Activate a background app in Cortana using voice commands - Cortana UWP design and development
description: Extend Cortana with features from your app (as a background task) using voice commands.
author: kbridge
label: Conceptual
ms.assetid: e2c7eae3-6beb-4156-92a5-474bba53451e
ms.author: wdg-dev-content
ms.date: 02/08/2017
ms.topic: article
ms.prod: cortana
keywords: cortana
---

# Activate a background app in Cortana using voice commands

In addition to using voice commands within **Cortana** to access system features, you can also extend **Cortana** with features and functionality from your app (as a background task) using voice commands that specify an action or command to execute. When an app handles a voice command in the background, it does not take focus. Instead, it returns all feedback and results through the **Cortana** canvas and the **Cortana** voice.

**Important APIs**

- [**Windows.ApplicationModel.VoiceCommands**](https://msdn.microsoft.com/library/windows/apps/dn706594)
- [**VCD elements and attributes v1.2**](https://msdn.microsoft.com/library/windows/apps/dn706593)

Apps can be activated to the foreground (the app takes focus) or activated in the background (**Cortana** retains focus), depending on the complexity of the interaction. For example, voice commands that require additional context or user input (such as sending a message to a specific contact) are best handled in a foreground app, while basic commands (such as listing upcoming trips) can be handled in **Cortana** through a background app.

If you want to activate an app to the foreground using voice commands, see [Activate a foreground app with voice commands through Cortana](launch-a-foreground-app-with-voice-commands-in-cortana.md).

> [!NOTE]
> A voice command is a single utterance with a specific intent, defined in a Voice Command Definition (VCD) file, directed at an installed app through **Cortana**.
>
> A VCD file defines one or more voice commands, each with a unique intent.
>
> A voice command definition can vary in complexity. It can support anything from a single, constrained utterance to a collection of more flexible, natural language utterances, all denoting the same intent.

To demonstrate background app features, we'll use a trip planning and management app named **Adventure Works** from the [Cortana voice command sample](https://go.microsoft.com/fwlink/p/?LinkID=619899).

Here's an overview of the **Adventure Works** app integrated with the **Cortana** canvas.

![cortana canvas overview ](../images/voicecommands/cortana-overview.png)

To view an **Adventure Works** trip without **Cortana**, a user would launch the app and navigate to the **Upcoming trips** page.

Using voice commands through **Cortana** to launch your app in the background, the user can instead just say, "Adventure Works, when is my trip to Las Vegas?". Your app handles the command and **Cortana** displays results along with your app icon and other app info, if provided. Here's an example of a basic trip query and **Cortana** result screen that both shows and speaks "Your next trip to Las Vegas is on Friday July 31st, 2015".

![a basic query and result screen using the adventure works app in the background](../images/voicecommands/cortana-backgroundapp-result.png)

These are the basic steps to add voice-command functionality and extend **Cortana** with background functionality from your app using speech or keyboard input:

1. Create an app service (see [**Windows.ApplicationModel.AppService**](https://msdn.microsoft.com/library/windows/apps/dn921731)) that **Cortana** invokes in the background.
2. Create a VCD file. This is an XML document that defines all the spoken commands that the user can say to initiate actions or invoke commands when activating your app. See [**VCD elements and attributes v1.2**](https://msdn.microsoft.com/library/windows/apps/dn706593).
3. Register the command sets in the VCD file when the app is launched.
4. Handle the background activation of the app service and the execution of the voice command.
5. Display and speak the appropriate feedback to the voice command within **Cortana**.

**Prerequisites**

If you're new to developing Universal Windows Platform (UWP) apps, have a look through these topics to get familiar with the technologies discussed here.

- [Create your first app](https://msdn.microsoft.com/library/windows/apps/bg124288)
- Learn about events with [Events and routed events overview](https://msdn.microsoft.com/library/windows/apps/mt185584)

**User experience guidelines**

See [Cortana design guidelines](https://msdn.microsoft.com/library/windows/apps/dn974233) for info about how to integrate your app with **Cortana** and [Speech design guidelines](https://msdn.microsoft.com/library/windows/apps/dn596121) for helpful tips on designing a useful and engaging speech-enabled app.

## <span id="Create_a_new_solution_with_a_primary_project_in_Visual_Studio"></span><span id="create_a_new_solution_with_a_primary_project_in_visual_studio"></span><span id="CREATE_A_NEW_SOLUTION_WITH_A_PRIMARY_PROJECT_IN_VISUAL_STUDIO"></span>Create a new solution with a primary project in Visual Studio

1. Launch Microsoft Visual Studio 2015.

    The Visual Studio 2015 Start page appears.

2. On the **File** menu, select **New** > **Project**.

    The **New Project** dialog appears. The left pane of the dialog lets you select the type of templates to display.

3. In the left pane, expand **Installed > Templates > Visual C\# > Windows**, then pick the **Universal** template group. The dialog's center pane displays a list of project templates for Universal Windows Platform (UWP) apps.
4. In the center pane, select the **Blank App (Universal Windows)** template.

    The **Blank App** template creates a minimal UWP app that compiles and runs, but contains no user-interface controls or data. You add controls to the app over the course of this tutorial.

5. In the **Name** text box, type your project name. For this example, we use "AdventureWorks".
6. Click **OK** to create the project.

    Microsoft Visual Studio creates your project and displays it in the **Solution Explorer**.

## <span id="Add_image_assets_to_primary_project_and_specify_them_in_the_app_manifest"></span><span id="add_image_assets_to_primary_project_and_specify_them_in_the_app_manifest"></span><span id="ADD_IMAGE_ASSETS_TO_PRIMARY_PROJECT_AND_SPECIFY_THEM_IN_THE_APP_MANIFEST"></span>Add image assets to  primary project and specify them in the app manifest
      
UWP apps can automatically select the most appropriate images based on specific settings and device capabilities (high contrast, effective pixels, locale, and so on). All you need to do is provide the images and ensure you use the appropriate naming convention and folder organization within the app project for the different resource versions. If you don't provide the recommended resource versions, accessibility, localization, and image quality can suffer, depending on the user's preferences, abilities, device type, and location.

For more detail on image resources for high contrast and scale factors, see [Guidelines for tile and icon assets](https://msdn.microsoft.com/windows/uwp/controls-and-patterns/tiles-and-notifications-app-assets).

You name resources using qualifiers. Resource qualifiers are folder and filename modifiers that identify the context in which a particular version of a resource should be used.

The standard naming convention is `foldername/qualifiername-value[_qualifiername-value]/filename.qualifiername-value[_qualifiername-value].ext`. For example, `images/en-US/logo.scale-100_contrast-white.png`, which can be referred to in code using just the root folder and the filename: `images/logo.png`. See [How to name resources using qualifiers](https://msdn.microsoft.com/library/windows/apps/xaml/hh965324.aspx).

We recommend that you mark the default language on string resource files (such as `en-US\resources.resw`) and the default scale factor on images (such as `logo.scale-100.png`), even if you do not currently plan to provide localized or multiple resolution resources. However, at a minimum, we recommend that you provide assets for 100, 200, and 400 scale factors.

> [!IMPORTANT]
> The app icon used in the title area of the **Cortana** canvas is the Square44x44Logo icon specified in the "Package.appxmanifest" file. 

> You can also specify an icon for each entry in the content area of the **Cortana** canvas. Valid image sizes for the results icons are:

> - 68w x 68h 
> - 68w x 92h 
> - 280w x 140h 

The content tile is not validated until a [**VoiceCommandResponse**](https://msdn.microsoft.com/library/windows/apps/dn974182) is passed to the [**VoiceCommandServiceConnection**](https://msdn.microsoft.com/library/windows/apps/dn974204). If you pass a **VoiceCommandResponse** object to **Cortana** that contains a content tile with an image that does not adhere to these size ratios, an exception can occur. 

In this example from the **Adventure Works** app (VoiceCommandService\\AdventureWorksVoiceCommandService.cs), we specify a simple grey square ("GreyTile.png") on the [**VoiceCommandContentTile**](https://msdn.microsoft.com/library/windows/apps/dn974168) using the [**TitleWith68x68IconAndText**](https://msdn.microsoft.com/library/windows/apps/dn974169) tile template. The logo variants are located in VoiceCommandService\\Images, and are retrieved using the [**GetFileFromApplicationUriAsync**](https://msdn.microsoft.com/library/windows/apps/hh701741) method.

```CSharp
var destinationTile = new VoiceCommandContentTile();

destinationTile.ContentTileType = 
  VoiceCommandContentTileType.TitleWith68x68IconAndText;
destinationTile.Image = 
  await StorageFile.GetFileFromApplicationUriAsync(
    new Uri("ms-appx:///AdventureWorks.VoiceCommands/Images/GreyTile.png"));
```

## <span id="Create_an_app_service_project"></span><span id="create_an_app_service_project"></span><span id="CREATE_AN_APP_SERVICE_PROJECT"></span>Create an app service project

<ol>
    <li>
    Right-click your Solution name, select **New > Project**.
    </li>
    <li>
    Under **Installed > Templates > Visual C# > Windows > Universal**, select **Windows Runtime Component**. This is the component that implements the app service (**[Windows.ApplicationModel.AppService](https://msdn.microsoft.com/library/windows/apps/dn921731)**).
    </li>
    <li>
    Type a name for the project (for example, "VoiceCommandService") and click **OK**.
    </li>
    <li>
    In **Solution Explorer**, select the "VoiceCommandService" project and rename the "Class1.cs" file generated by Visual Studio. For the **Adventure Works** example we use "AdventureWorksVoiceCommandService.cs".
    </li>
    <li>
    Click **Yes** when asked if you want to rename all occurrences of "Class1.cs". 
    </li>
    <li>
    In the "AdventureWorksVoiceCommandService.cs" file:
        <ol type="i">
 <li>
 Add the following using directive.  
 ```using Windows.ApplicationModel.Background;```
 </li>
 <li>
 When you create a new project, the project name is used as the default root namespace in all files. Rename the namespace to nest the app service code under the primary project. For example, `namespace AdventureWorks.VoiceCommands`. 
 </li>
 <li>
 Right click the app service project name in Solution Explorer and select **Properties**. 
 </li>
 <li>
 On the **Library** tab, update the **Default namespace** field with this same value (for this example, "AdventureWorks.VoiceCommands"). 
 </li>
 <li>
 Create a new class that implements the [**IBackgroundTask**](https://msdn.microsoft.com/library/windows/apps/br224794) interface. This class requires a [**Run**](https://msdn.microsoft.com/library/windows/apps/br224811) method, which is the entry point when Cortana recognizes the voice command. 
 </li>
        </ol>
    </li>
</ol>

Here's a basic background task class from the **Adventure Works** app. We'll fill in more detail later.
> [!NOTE]   
> The background task class itself, and all other classes in the background task project, need to be sealed public classes.

``` csharp
namespace AdventureWorks.VoiceCommands
{
    ...
    
    /// <summary>
    /// The VoiceCommandService implements the entry point for all voice commands.
    /// The individual commands supported are described in the VCD xml file. 
    /// The service entry point is defined in the appxmanifest.
    /// </summary>
    public sealed class AdventureWorksVoiceCommandService : IBackgroundTask
    {
        ...
        
        /// <summary>
        /// The background task entrypoint. 
        /// 
        /// Background tasks must respond to activation by Cortana within 0.5 seconds, and must 
        /// report progress to Cortana every 5 seconds (unless Cortana is waiting for user
        /// input). There is no execution time limit on the background task managed by Cortana,
        /// but developers should use plmdebug (https://msdn.microsoft.com/library/windows/hardware/jj680085%28v=vs.85%29.aspx)
        /// on the Cortana app package in order to prevent Cortana timing out the task during
        /// debugging.
        /// 
        /// The Cortana UI is dismissed if Cortana loses focus. 
        /// The background task is also dismissed even if being debugged. 
        /// Use of Remote Debugging is recommended in order to debug background task behaviors. 
        /// Open the project properties for the app package (not the background task project), 
        /// and enable Debug -> "Do not launch, but debug my code when it starts". 
        /// Alternatively, add a long initial progress screen, and attach to the background task process while it executes.
        /// </summary>
        /// <param name="taskInstance">Connection to the hosting background service process.</param>
        public void Run(IBackgroundTaskInstance taskInstance)
        {
          //
          // TODO: Insert code 
          //
          //
    }
  }
}
```

<ol start="7">
    <li>
    Declare your background task as an **AppService** in the app manifest.
    <ol type="i">
        <li>
        In **Solution Explorer**, right click the "Package.appxmanifest" file and select **View Code**. 
        </li>
        <li>
        Find the [**Application**](https://msdn.microsoft.com/library/windows/apps/dn934738) element.
        </li>
        <li>
        Add an [**Extensions**](https://msdn.microsoft.com/library/windows/apps/dn934720) element to the [**Application**](https://msdn.microsoft.com/library/windows/apps/dn934738) element.
        </li>
        <li>
        Add a [**uap:Extension**](https://msdn.microsoft.com/library/windows/apps/dn986788) element to the [**Extensions**](https://msdn.microsoft.com/library/windows/apps/dn934720) element.
        </li>
        <li>Add a **Category** attribute to the **uap:Extension** element and set the value of the **Category** attribute to "windows.appService".
        </li>
        <li>
        Add an **EntryPoint** attribute to the **uap:Extension** element and set the value of the **EntryPoint** attribute to the name of the class that implements [**IBackgroundTask**](https://msdn.microsoft.com/library/windows/apps/br224794), in this case "AdventureWorks.VoiceCommands.AdventureWorksVoiceCommandService".
        </li>
        <li>
        Add a [**uap:AppService**](https://msdn.microsoft.com/library/windows/apps/dn934779) element to the **uap:Extension** element.
        </li>
        <li>
        Add a **Name** attribute to the [**uap:AppService**](https://msdn.microsoft.com/library/windows/apps/dn934779) element and set the value of the **Name** attribute to a name for the app service, in this case "AdventureWorksVoiceCommandService".
        </li>
        <li>
        Add a second [**uap:Extension**](https://msdn.microsoft.com/library/windows/apps/dn986788) element to [**Extensions**](https://msdn.microsoft.com/library/windows/apps/dn934720).
        </li>
        <li>
        Add a **Category** attribute to this [**uap:Extension**](https://msdn.microsoft.com/library/windows/apps/dn986788) element and set the value of the **Category** attribute to "windows.personalAssistantLaunch".
        </li>
    </li> 
    </ol>
    </li>    
</ol>  

Here's the manifest from the Adventure Works app:
```xml
<Package>
  <Applications>
    <Application>

      <Extensions>
        <uap:Extension Category="windows.appService" 
          EntryPoint="CortanaBack1.VoiceCommands.AdventureWorksVoiceCommandService">
          <uap:AppService Name="AdventureWorksVoiceCommandService"/>
        </uap:Extension>
        <uap:Extension Category="windows.personalAssistantLaunch"/>
      </Extensions>

    <Application>
  <Applications>
</Package>
```

<ol start="8">
    <li>
    Add this app service project as a reference in the primary project. 
    <ol type="i">
        <li>
        Right click **References**. 
        </li>
        <li>
        Select **Add Reference...** 
        </li>
        <li>
        In the **Reference Manager** dialog, expand **Projects** and select the app service project. 
        </li>
        <li>
        Click **OK**. 
        </li>
    </ol>
    </li>
</ol>

## <span id="Create_a_VCD_file"></span><span id="create_a_vcd_file"></span><span id="CREATE_A_VCD_FILE"></span>Create a VCD file


1. In Visual Studio, right-click your primary project name, select **Add > New Item**. Add an **XML File**.
2. Type a name for the [**VCD**](https://msdn.microsoft.com/library/windows/apps/dn706593) file (for this example, "AdventureWorksCommands.xml"), and click Add. 
3. In **Solution Explorer**, select the [**VCD**](https://msdn.microsoft.com/library/windows/apps/dn706593) file.
4.  In the **Properties** window, set **Build action** to **Content**, and then set **Copy to output directory** to **Copy if newer**.

## <span id="Edit_the_VCD_file"></span><span id="edit_the_vcd_file"></span><span id="EDIT_THE_VCD_FILE"></span>Edit the VCD file

1. Add a **VoiceCommands** element with an **xmlns** attribute pointing to `https://schemas.microsoft.com/voicecommands/1.2`.

2. For each language supported by your app, create a [**CommandSet**](https://msdn.microsoft.com/library/windows/apps/dn722331) element that contains the voice commands supported by your app.

  You can declare multiple [**CommandSet**](https://msdn.microsoft.com/library/windows/apps/dn722331) elements, each with a different [**xml:lang**](https://msdn.microsoft.com/library/windows/apps/dn722331) attribute so your app to be used in different markets. For example, an app for the United States might have a [**CommandSet**](https://msdn.microsoft.com/library/windows/apps/dn722331) for English and a [**CommandSet**](https://msdn.microsoft.com/library/windows/apps/dn722331) for Spanish.

	> [!IMPORTANT]
	> To activate an app and initiate an action using a voice command, the app must register a VCD file that contains a [**CommandSet**](https://msdn.microsoft.com/library/windows/apps/dn722331) with a language that matches the speech language selected by the user for their device. The speech language is located in **Settings > System > Speech > Speech Language**.

3. Add a **Command** element for each command you want to support.

  Each **Command** declared in a [**VCD**](https://msdn.microsoft.com/library/windows/apps/dn706593) file must include this information:

  - A **Name** attribute that your application uses to identify the voice command at runtime. 
  - An **Example** element that contains a phrase describing how a user can invoke the command. **Cortana** shows this example when the user says "What can I say?", "Help", or they tap **See more**.    
  -   A **ListenFor** element that contains the words or phrases that your app recognizes as a command. Each **ListenFor** element can contain references to one or more **PhraseList** elements that contain specific words relevant to the command.
> [!NOTE]
> **ListenFor** elements cannot be programmatically modified. However, **PhraseList** elements associated with **ListenFor** elements can be programmatically modified. Applications should modify the content of the **PhraseList** at runtime based on the data set generated as the user uses the app. See [Dynamically modify Voice Command Definition (VCD) phrase lists](dynamically-modify-voice-command-definition-vcd-phrase-lists.md).

  -   A **Feedback** element that contains the text for **Cortana** to display and speak as the application is launched.

A **Navigate** element indicates that the voice command activates the app to the foreground. In this example, the ```showTripToDestination``` command is a foreground task.

A **VoiceCommandService** element indicates that the voice command activates the app in the background. The value of the **Target** attribute of this element should match the value of the **Name** attribute of the [**uap:AppService**](https://msdn.microsoft.com/library/windows/apps/dn934779) element in the package.appxmanifest file. In this example, the ```whenIsTripToDestination``` and ```cancelTripToDestination``` commands are background tasks that specify the name of the app service as "AdventureWorksVoiceCommandService".

For more detail, see the [**VCD elements and attributes v1.2**](https://msdn.microsoft.com/library/windows/apps/dn706593) reference.

Here's a portion of the [**VCD**](https://msdn.microsoft.com/library/windows/apps/dn706593) file that defines the en-us voice commands for the **Adventure Works** app.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<VoiceCommands xmlns="https://schemas.microsoft.com/voicecommands/1.2">
  <CommandSet xml:lang="en-us" Name="AdventureWorksCommandSet_en-us">
    <AppName> Adventure Works </AppName>
    <Example> Show trip to London </Example>

    <Command Name="showTripToDestination">
      <Example> Show trip to London </Example>
      <ListenFor RequireAppName="BeforeOrAfterPhrase"> show [my] trip to {destination} </ListenFor>
      <ListenFor RequireAppName="ExplicitlySpecified"> show [my] {builtin:AppName} trip to {destination} </ListenFor>
      <Feedback> Showing trip to {destination} </Feedback>
      <Navigate />
    </Command>

    <Command Name="whenIsTripToDestination">
      <Example> When is my trip to Las Vegas?</Example>
      <ListenFor RequireAppName="BeforeOrAfterPhrase"> when is [my] trip to {destination}</ListenFor>
      <ListenFor RequireAppName="ExplicitlySpecified"> when is [my] {builtin:AppName} trip to {destination} </ListenFor>
      <Feedback> Looking for trip to {destination}</Feedback>
      <VoiceCommandService Target="AdventureWorksVoiceCommandService"/>
    </Command>
    
    <Command Name="cancelTripToDestination">
      <Example> Cancel my trip to Las Vegas </Example>
      <ListenFor RequireAppName="BeforeOrAfterPhrase"> cancel [my] trip to {destination}</ListenFor>
      <ListenFor RequireAppName="ExplicitlySpecified"> cancel [my] {builtin:AppName} trip to {destination} </ListenFor>
      <Feedback> Cancelling trip to {destination}</Feedback>
      <VoiceCommandService Target="AdventureWorksVoiceCommandService"/>
    </Command>

    <PhraseList Label="destination">
      <Item>London</Item>
      <Item>Las Vegas</Item>
      <Item>Melbourne</Item>
      <Item>Yosemite National Park</Item>
    </PhraseList>
  </CommandSet>
```

## <span id="Install_the_VCD_commands"></span><span id="install_the_vcd_commands"></span><span id="INSTALL_THE_VCD_COMMANDS"></span>Install the VCD commands

Your app must run once to install the VCD. 

> [!NOTE]
> Voice command data is not preserved across app installations. To ensure the voice command data for your app remains intact, consider initializing your VCD file each time your app is launched or activated, or maintain a setting that indicates if the VCD is currently installed.

In the "app.xaml.cs" file:

1. Add the following using directive:  
	```csharp
	using Windows.Storage;
	```
2. Mark the "OnLaunched" method with the async modifier.  
	```csharp
	protected async override void OnLaunched(LaunchActivatedEventArgs e)
	```
3. Call [**InstallCommandDefinitionsFromStorageFileAsync**](https://msdn.microsoft.com/library/windows/apps/dn708205) in the [**OnLaunched**](https://msdn.microsoft.com/library/windows/apps/br242335) handler to register the voice commands that the system should recognize.

  In the Adventure Works sample, we first define a [**StorageFile**](https://msdn.microsoft.com/library/windows/apps/br227171) object. 

  We then call [**GetFileAsync**](https://msdn.microsoft.com/library/windows/apps/br227272) to initialize it with our "AdventureWorksCommands.xml" file.

  This [**StorageFile**](https://msdn.microsoft.com/library/windows/apps/br227171) object is then passed to [**InstallCommandDefinitionsFromStorageFileAsync**](https://msdn.microsoft.com/library/windows/apps/dn708205).    
	```CSharp
	try
	{
	  // Install the main VCD. 
	  StorageFile vcdStorageFile = 
	    await Package.Current.InstalledLocation.GetFileAsync(
	      @"AdventureWorksCommands.xml");
	
	  await Windows.ApplicationModel.VoiceCommands.VoiceCommandDefinitionManager.
	    InstallCommandDefinitionsFromStorageFileAsync(vcdStorageFile);
	
	  // Update phrase list.
	  ViewModel.ViewModelLocator locator = App.Current.Resources["ViewModelLocator"] as ViewModel.ViewModelLocator;
	  if(locator != null)
	  {
	     await locator.TripViewModel.UpdateDestinationPhraseList();
	  }
	}
	catch (Exception ex)
	{
	  System.Diagnostics.Debug.WriteLine("Installing Voice Commands Failed: " + ex.ToString());
	}
	```

## <span id="Handle_activation_and_execute_voice_commands"></span><span id="handle_activation_and_execute_voice_commands"></span><span id="HANDLE_ACTIVATION_AND_EXECUTE_VOICE_COMMANDS"></span>Handle activation

Specify how your app responds to subsequent voice command activations (after it has been launched at least once and the voice command sets have been installed).

1.  Confirm that your app was activated by a voice command.

    Override the [**Application.OnActivated**](https://msdn.microsoft.com/library/windows/apps/br242330) event and check whether [**IActivatedEventArgs**](https://msdn.microsoft.com/library/windows/apps/br224727).[**Kind**](https://msdn.microsoft.com/library/windows/apps/br224728) is [**VoiceCommand**](https://msdn.microsoft.com/library/windows/apps/br224693).

2.  Determine the name of the command and what was spoken.

    Get a reference to a [**VoiceCommandActivatedEventArgs**](https://msdn.microsoft.com/library/windows/apps/dn609755) object from the [**IActivatedEventArgs**](https://msdn.microsoft.com/library/windows/apps/br224727) and query the [**Result**](https://msdn.microsoft.com/library/windows/apps/dn609758) property for a [**SpeechRecognitionResult**](https://msdn.microsoft.com/library/windows/apps/dn631432) object.

    To determine what the user said, check the value of [**Text**](https://msdn.microsoft.com/library/windows/apps/dn631441) or the semantic properties of the recognized phrase in the [**SpeechRecognitionSemanticInterpretation**](https://msdn.microsoft.com/library/windows/apps/dn631443) dictionary.

3.  Take the appropriate action in your app, such as navigating to the desired page.

For this example, we refer back to the VCD in Step 3: Edit the VCD file.

Once we get the speech-recognition result for the voice command, we get the command name from the first value in the [**RulePath**](https://msdn.microsoft.com/library/windows/apps/dn631438) array. As the VCD file defined more than one possible voice command, we need to compare the value against the command names in the VCD and take the appropriate action.

The most common action an application can take is to navigate to a page with content relevant to the context of the voice command. For this example, we navigate to a **TripPage** page and pass in the value of the voice command, how the command was input, and the recognized "destination" phrase (if applicable). Alternatively, the app could send a navigation parameter to the [**SpeechRecognitionResult**](https://msdn.microsoft.com/library/windows/apps/dn631432) when navigating to the page.

You can find out whether the voice command that launched your app was actually spoken, or whether it was typed in as text, from the [**SpeechRecognitionSemanticInterpretation.Properties**](https://msdn.microsoft.com/library/windows/apps/dn631445) dictionary using the **commandMode** key. The value of that key will be either "voice" or "text". If the value of the key is "voice", consider using speech synthesis ([**Windows.Media.SpeechSynthesis**](https://msdn.microsoft.com/library/windows/apps/dn278951)) in your app to provide the user with spoken feedback.

Use the [**SpeechRecognitionSemanticInterpretation.Properties**](https://msdn.microsoft.com/library/windows/apps/dn631445) to find out the content spoken in the **PhraseList** or **PhraseTopic** constraints of a **ListenFor** element. The dictionary key is the value of the **Label** attribute of the **PhraseList** or **PhraseTopic** element. Here, we show how to access the value of **{destination}** phrase.

``` csharp
/// <summary>
/// Entry point for an application activated by some means other than normal launching. 
/// This includes voice commands, URI, share target from another app, and so on. 
/// 
/// NOTE:
/// A previous version of the VCD file might remain in place 
/// if you modify it and update the app through the store. 
/// Activations might include commands from older versions of your VCD. 
/// Try to handle these commands gracefully.
/// </summary>
/// <param name="args">Details about the activation method.</param>
protected override void OnActivated(IActivatedEventArgs args)
{
	base.OnActivated(args);

	Type navigationToPageType;
	ViewModel.TripVoiceCommand? navigationCommand = null;

    // Voice command activation.
	if (args.Kind == ActivationKind.VoiceCommand)
	{
		// Event args can represent many different activation types. 
        // Cast it so we can get the parameters we care about out.
		var commandArgs = args as VoiceCommandActivatedEventArgs;

		Windows.Media.SpeechRecognition.SpeechRecognitionResult speechRecognitionResult = commandArgs.Result;

		// Get the name of the voice command and the text spoken. 
        // See VoiceCommands.xml for supported voice commands.
		string voiceCommandName = speechRecognitionResult.RulePath[0];
		string textSpoken = speechRecognitionResult.Text;

		// commandMode indicates whether the command was entered using speech or text.
        // Apps should respect text mode by providing silent (text) feedback.
		string commandMode = this.SemanticInterpretation("commandMode", speechRecognitionResult);
		
		switch (voiceCommandName)
		{
			case "showTripToDestination":
				// Access the value of {destination} in the voice command.
				string destination = this.SemanticInterpretation("destination", speechRecognitionResult);

				// Create a navigation command object to pass to the page. 
				navigationCommand = new ViewModel.TripVoiceCommand(
					voiceCommandName,
					commandMode,
					textSpoken,
					destination);

				// Set the page to navigate to for this voice command.
				navigationToPageType = typeof(View.TripDetails);
				break;
			default:
				// If we can't determine what page to launch, go to the default entry point.
				navigationToPageType = typeof(View.TripListView);
				break;
		}
	}
	// Protocol activation occurs when a card is clicked within Cortana (using a background task).
    else if (args.Kind == ActivationKind.Protocol)
	{
		// Extract the launch context. In this case, we're just using the destination from the phrase set (passed
		// along in the background task inside Cortana), which makes no attempt to be unique. A unique id or 
		// identifier is ideal for more complex scenarios. We let the destination page check if the 
		// destination trip still exists, and navigate back to the trip list if it doesn't.
		var commandArgs = args as ProtocolActivatedEventArgs;
		Windows.Foundation.WwwFormUrlDecoder decoder = new Windows.Foundation.WwwFormUrlDecoder(commandArgs.Uri.Query);
		var destination = decoder.GetFirstValueByName("LaunchContext");

		navigationCommand = new ViewModel.TripVoiceCommand(
								"protocolLaunch",
								"text",
								"destination",
								destination);

		navigationToPageType = typeof(View.TripDetails);
	}
	else
	{
		// If we were launched via any other mechanism, fall back to the main page view.
        // Otherwise, we'll hang at a splash screen.
		navigationToPageType = typeof(View.TripListView);
	}

	// Repeat the same basic initialization as OnLaunched() above, taking into account whether
	// or not the app is already active.
	Frame rootFrame = Window.Current.Content as Frame;

	// Do not repeat app initialization when the Window already has content,
	// just ensure that the window is active.
	if (rootFrame == null)
	{
		// Create a frame to act as the navigation context and navigate to the first page.
		rootFrame = new Frame();
		App.NavigationService = new NavigationService(rootFrame);

		rootFrame.NavigationFailed += OnNavigationFailed;

		// Place the frame in the current window.
		Window.Current.Content = rootFrame;
	}

	// Since we're expecting to always show a details page, navigate even if 
	// a content frame is in place (unlike OnLaunched).
	// Navigate to either the main trip list page, or if a valid voice command
	// was provided, to the details page for that trip.
	rootFrame.Navigate(navigationToPageType, navigationCommand);

	// Ensure the current window is active
	Window.Current.Activate();
}

/// <summary>
/// Returns the semantic interpretation of a speech result. 
/// Returns null if there is no interpretation for that key.
/// </summary>
/// <param name="interpretationKey">The interpretation key.</param>
/// <param name="speechRecognitionResult">The speech recognition result to get the semantic interpretation from.</param>
/// <returns></returns>
private string SemanticInterpretation(string interpretationKey, SpeechRecognitionResult speechRecognitionResult)
{
  return speechRecognitionResult.SemanticInterpretation.Properties[interpretationKey].FirstOrDefault();
}
```

## <span id="Handle_the_voice_command_in_the_app_service"></span><span id="handle_the_voice_command_in_the_app_service"></span><span id="HANDLE_THE_VOICE_COMMAND_IN_THE_APP_SERVICE"></span>Handle the voice command in the app service


Process the voice command in the app service.


1.  Add the following using directives to your voice command service file, "AdventureWorksVoiceCommandService.cs" for this example.
	```csharp
	using Windows.ApplicationModel.VoiceCommands;
	using Windows.ApplicationModel.Resources.Core;
	using Windows.ApplicationModel.AppService;
	```

2.  Take a service deferral so your app service is not terminated while handling the voice command.
3.  Confirm that your background task is running as an app service activated by a voice command.

    1.  Cast the [**IBackgroundTaskInstance.TriggerDetails**](https://msdn.microsoft.com/library/windows/apps/br224802) to [**Windows.ApplicationModel.AppService.AppServiceTriggerDetails**](https://msdn.microsoft.com/library/windows/apps/dn921727).
    2.  Check that [**IBackgroundTaskInstance.TriggerDetails.Name**](https://msdn.microsoft.com/library/windows/apps/br224807) is the name of the app service in the "Package.appxmanifest" file.

4.  Use [**IBackgroundTaskInstance.TriggerDetails**](https://msdn.microsoft.com/library/windows/apps/br224802) to create a [**VoiceCommandServiceConnection**](https://msdn.microsoft.com/library/windows/apps/dn974204) to **Cortana** to retrieve the voice command.
5.  Register an event handler for [**VoiceCommandServiceConnection**](https://msdn.microsoft.com/library/windows/apps/dn974204).[**VoiceCommandCompleted**](https://msdn.microsoft.com/library/windows/apps/dn706584) to receive notification when the app service is closed due to a user cancellation.
6.  Register an event handler for the [**IBackgroundTaskInstance.Canceled**](https://msdn.microsoft.com/library/windows/apps/br224798) to receive notification when the app service is closed due to an unexpected failure.
7.  Determine the name of the command and what was spoken.

    1.  Use the [**VoiceCommand**](https://msdn.microsoft.com/library/windows/apps/dn974162).[**CommandName**](https://msdn.microsoft.com/library/windows/apps/dn706589) property to determine the name of the voice command.
    2.  To determine what the user said, check the value of [**Text**](https://msdn.microsoft.com/library/windows/apps/dn631441) or the semantic properties of the recognized phrase in the [**SpeechRecognitionSemanticInterpretation**](https://msdn.microsoft.com/library/windows/apps/dn631443) dictionary.

7.  Take the appropriate action in your app service.
8.  Display and speak the feedback to the voice command with **Cortana**.

    1.  Determine the strings that you want **Cortana** to display and speak to the user in response to the voice command and create a [**VoiceCommandResponse**](https://msdn.microsoft.com/library/windows/apps/dn974182) object. For guidance on how to select the feedback strings that **Cortana** shows and speaks, see [Cortana design guidelines](https://msdn.microsoft.com/library/windows/apps/dn974233).
    2.  Use the [**VoiceCommandServiceConnection**](https://msdn.microsoft.com/library/windows/apps/dn974204) instance to report progress or completion to **Cortana** by calling [**ReportProgressAsync**](https://msdn.microsoft.com/library/windows/apps/dn706579) or [**ReportSuccessAsync**](https://msdn.microsoft.com/library/windows/apps/dn706580) with the **VoiceCommandServiceConnection** object.

    For this example, we refer back to the VCD in Step 3: Edit the VCD file.

```csharp
public sealed class VoiceCommandService : IBackgroundTask
    {
      private BackgroundTaskDeferral serviceDeferral;
      VoiceCommandServiceConnection voiceServiceConnection;

      public async void Run(IBackgroundTaskInstance taskInstance)
      {
      //Take a service deferral so the service isn&#39;t terminated.
        this.serviceDeferral = taskInstance.GetDeferral();

        taskInstance.Canceled += OnTaskCanceled;

        var triggerDetails = 
          taskInstance.TriggerDetails as AppServiceTriggerDetails;

        if (triggerDetails != null &amp;&amp; 
          triggerDetails.Name == "AdventureWorksVoiceServiceEndpoint")
        {
          try
          {
 voiceServiceConnection = 
   VoiceCommandServiceConnection.FromAppServiceTriggerDetails(
     triggerDetails);

 voiceServiceConnection.VoiceCommandCompleted += 
   VoiceCommandCompleted;

 VoiceCommand voiceCommand = await
 voiceServiceConnection.GetVoiceCommandAsync();

 switch (voiceCommand.CommandName)
 {
   case "whenIsTripToDestination":
   {
     var destination = 
       voiceCommand.Properties["destination"][0];
     SendCompletionMessageForDestination(destination);
     break;
   }

   // As a last resort, launch the app in the foreground.
   default:
     LaunchAppInForeground();
     break;
 }
          }
          finally
          {
 if (this.serviceDeferral != null)
 {
   // Complete the service deferral.
   this.serviceDeferral.Complete();
 }
          }
        }
      }

      private void VoiceCommandCompleted(
        VoiceCommandServiceConnection sender, 
        VoiceCommandCompletedEventArgs args)
      {
        if (this.serviceDeferral != null)
        {
          // Insert your code here.
          // Complete the service deferral.
          this.serviceDeferral.Complete();
        }
      }

      private async void SendCompletionMessageForDestination(
        string destination)
      {
        // Take action and determine when the next trip to destination
        // Insert code here.
        
        // Replace the hardcoded strings used here with strings 
        // appropriate for your application.

        // First, create the VoiceCommandUserMessage with the strings 
        // that Cortana will show and speak.
        var userMessage = new VoiceCommandUserMessage();
        userMessage.DisplayMessage = "Here’s your trip.";
        userMessage.SpokenMessage = "Your trip to Vegas is on August 3rd.";

        // Optionally, present visual information about the answer.
        // For this example, create a VoiceCommandContentTile with an 
        // icon and a string.
        var destinationsContentTiles = new List<VoiceCommandContentTile>();

        var destinationTile = new VoiceCommandContentTile();
        destinationTile.ContentTileType = 
          VoiceCommandContentTileType.TitleWith68x68IconAndText;
        // The user can tap on the visual content to launch the app. 
        // Pass in a launch argument to enable the app to deep link to a 
        // page relevant to the item displayed on the content tile.
        destinationTile.AppLaunchArgument = 
          string.Format("destination={0}”, “Las Vegas");
        destinationTile.Title = "Las Vegas";
        destinationTile.TextLine1 = "August 3rd 2015";
        destinationsContentTiles.Add(destinationTile);

        // Create the VoiceCommandResponse from the userMessage and list    
        // of content tiles.
        var response = 
          VoiceCommandResponse.CreateResponse(
 userMessage, destinationsContentTiles);

        // Cortana will present a “Go to app_name” link that the user 
        // can tap to launch the app. 
        // Pass in a launch to enable the app to deep link to a page 
        // relevant to the voice command.
        response.AppLaunchArgument = 
          string.Format("destination={0}”, “Las Vegas");
        
        // Ask Cortana to display the user message and content tile and 
        // also speak the user message.
        await voiceServiceConnection.ReportSuccessAsync(response);
      }

      private async void LaunchAppInForeground()
      {
        var userMessage = new VoiceCommandUserMessage();
        userMessage.SpokenMessage = "Launching Adventure Works";

        var response = VoiceCommandResponse.CreateResponse(userMessage);

        // When launching the app in the foreground, pass an app 
        // specific launch parameter to indicate what page to show.
        response.AppLaunchArgument = "showAllTrips=true";

        await voiceServiceConnection.RequestAppLaunchAsync(response);
      }
    }
```

Once activated, the app service has .5 seconds to call [**ReportSuccessAsync**](https://msdn.microsoft.com/library/windows/apps/dn706580). **Cortana** shows and says a feedback string. 

[!NOTE] You can declare a **Feedback** string in the VCD file. This string does not affect the UI text displayed on the Cortana canvas, it only affects the text spoken by **Cortana**.

If the app takes longer than .5 seconds to make the call, **Cortana** inserts a hand-off screen, as shown here. **Cortana** displays the hand-off screen until the application calls **ReportSuccessAsync**, or for up to 5 seconds. If the app service doesn’t call **ReportSuccessAsync**, or any of the [**VoiceCommandServiceConnection**](https://msdn.microsoft.com/library/windows/apps/dn974204) methods that provide **Cortana** with information, the user receives an error message and the app service is cancelled.

![a basic query with progress and result screens using the adventure works app in the background](../images/voicecommands/cortana-backgroundapp-progress-result.png)

## <span id="related_topics"></span>Related articles


**Developers**
* [Voice commands](vcd.md)
* [Interact with a background app in Cortana](interact-with-a-background-app-in-cortana.md)
* [VCD elements and attributes v1.2](https://msdn.microsoft.com/library/windows/apps/dn706593)
* [Quickstart: Using file or image resources](https://msdn.microsoft.com/library/windows/apps/xaml/hh965325)
* [How to name resources using qualifiers](https://msdn.microsoft.com/library/windows/apps/xaml/hh965324)

**Designers**
* [Cortana design guidelines](https://msdn.microsoft.com/library/windows/apps/dn974233)
* [Speech design guidelines](https://msdn.microsoft.com/library/windows/apps/dn596121)
* [Responsive design 101 for UWP apps](https://msdn.microsoft.com/library/windows/apps/dn958435)
* [Guidelines for tile and icon assets](https://msdn.microsoft.com/library/windows/apps/mt412102)

**Samples**
* [Cortana voice command sample](https://go.microsoft.com/fwlink/p/?LinkID=619899)
 

 




