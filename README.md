<div align="center">
       <h1> 
        <p>
           <a href="https://github.com/RocketChat/Apps.RC.AI.Programmer">AI Programmer App </a> for <a href="https://rocket.chat/">Rocket.Chat</a>
        </p>
      </h1>
    <a href="https://summerofcode.withgoogle.com/programs/2024/projects/ZRkQn5bb"><img src="https://i.imgur.com/pgkUceb.png" width="650" alt="google-summer-of-code"></a>
    <br>
</div>

<p align="center">
    <code> 
        <a href="#-project-abstract">Project Abstract</a>&nbsp;&nbsp;&nbsp;
        <a href="#-deliverables">Deliverables</a>&nbsp;&nbsp;&nbsp;
        <a href="#-demo">Demo</a>&nbsp;&nbsp;&nbsp;
        <a href="#-contributions">Contributions</a>&nbsp;&nbsp;&nbsp;
        <a href="#pushing-limits">Pushing Limits</a>&nbsp;&nbsp;&nbsp;
        <a href="#documentation">Documentation</a>&nbsp;&nbsp;&nbsp;
        <a href="#-mentors">Mentors</a>
    </code>
</p>

I am the open-source contributor for the Google Summer of Code 2024 working on the AI Programmer project for Rocket.Chat. In this repository I will clarify a final report summary of my GSoC work and a quick guide for all future GSoC aspirants.

## ⭐ Project Abstract

The AI Programmer Rocket.Chat App enables users to generate a short piece of code in C/C++, Java, Javascript, Typescript or Python based on their specification. They can switch between different LLMs (Mistral, CodeLlama, etc.) and ask for a new refinement on the code generation result to make augment or fine-tune. A well-designed interactive UX aiming to simplify user's interactions is also implemented. Finally, the app bridges the generated codes with sharing APIs, allowing users to share the code pieces in RC channel or their Github repositories. 


## 🚢 Deliverables

The following were the deliverables of this project:

- Interactive User Interface : Unlock the true potential of the UiKit and add an interactive user interface for each of the added features of the application, eliminating the need to type long slash commands for more complex tasks.
- Minimal Slash Command Interface : Adding slash command to trigger the application to manipulate on the AI programmer's functions with minimal interactions.
- User Configuration: Users can specify their personalized configuration for code generation tasks, for example, use which programming language and LLM.
- Code Generation: Allowing users to generate code pieces by providing their requirements and specifications.
- Code Refinement: Users can further ask for a new variation of the code or augment/fine-tune the system for a more precise result.
- Share Code to Github Repository: By configuring the OAuth2 connection with Github, users can upload their generated code pieces to the target Github repository, branch, file.

Extra Features which were suggested by mentors throughout the Google Summer of Code period:

- Share Code in RC Channel: The generated code is not only viewable by the users, but can also be shared into current RC channels for other users to check.
- Compatible with New Version UI-Kit: Since the RC server and app engine's ui-kit update frequently, the entire user interface is well-designed and implemented with new version features and compatible with RC servers.   

**It's glad to complete all of the above deliverables and meet expected goals within the GSoC period! 🎉**

## 📺 Demo

### Minimal Slash Command Interface

The Minimal Slash commands allow users to handle ai programmer functions using simple slash commands. Users can generate code, set personalized configuration, connect to Github, and share codes. These commands allow users to access the app's features more conveniently. 

1. Generate code pieces with specific description (please set language and llm correctly first!) -> \`/ai-programmer gen code_content\`
2. Set the language you want to use to generate code -> \`/ai-programmer set C++\`
3. Switch to the LLM you want to use to generate code -> \`/ai-programmer llm llama3-70b\`
4. List the available LLM options -> \`/ai-programmer list \`
5. Use the interactive user interface to handle your operations -> \`/ai-programmer ui \`
6. Login to Github (You should set OAuth2 settings first!) -> \`/ai-programmer login \`.
7. Logout to Github -> \`/ai-programmer logout \`.

### User Interface

For users who prefers UX interactions, the app also provides access by UX. The user interface will be invoked directly using command \`/ai-programmer\`, which will open a contexutal bar for users to set their configurations. After the configurations are set and ready, users can progress to other functions.

The friendly user interface implemented using RC app engine's ui-kit allows interactive operations on all features and functions provided by the ai programmer. All manipulation opereations can be seen in the video:



https://github.com/user-attachments/assets/eb169616-63c1-40c0-96e0-dadc4bc05e92



### 🔐 GitHub OAuth

In the GitHub App I have implemented the Authentication mechanism using OAuth2. Here we have used the [GitHub OAuth](https://docs.github.com/en/developers/apps/building-oauth-apps/authorizing-oauth-apps) along with the [RocketChat Apps Oauth2 Client](https://developer.rocket.chat/apps-engine/adding-features/oauth2-client).     
- The users can log in to their github accounts simply by entering the slash command : `/github login` and clicking on the `login` button.
- As soon as the user is logged in, they receive a message and they can now use all the features which require authorized users.
- The users are automatically logged out after a period of time and the token is deleted. This was done to ensure the scalability of the feature in case of inactive users and to remove old OAuth tokens from the apps limited persistent storage. To achieve this we use the [RocketChat Apps Scheduler API](https://developer.rocket.chat/apps-engine/adding-features/scheduler-api).

https://user-images.githubusercontent.com/70485812/189439737-78e25abc-a78b-43da-af2f-21a6c061bc38.mp4




## 🚀 Contributions

### Pull Requests

<div align="center">

| PR Link   | Description  | Status | 
| :-----------: | :------------------------------------:| :------:|
| [PR #1](https://github.com/RocketChat/Apps.RC.AI.Programmer/pull/1) | <b> [New] Setup development environment and make prototype demo.</b> <br><br> <div align="left"> Highlights include:<ul><li>Configured proper Rocket.chat app engine's development environment.</li><li>Enable users to automatically generate code pieces using the OpenAI GPT3.5 Turbo APIs.</li><div> | <img src="https://i.imgur.com/tskv8MM.png" width=50 height=40> |
| [PR #2](https://github.com/RocketChat/Apps.RC.AI.Programmer/pull/2) | <b>[Refactor] Refactor the entire app on new framework supporting open-source LLMs.</b> <br><br> <div align="left"> Highlights include:<ul><li> Rebased the code on an improved framework, which supports generic GPT-format LLM APIs.</li><li>Organize the entire code base to remove unnecessary files from commits.</li><li>Adopted the functionality of the open-source mistral-7b APIs on code generation tasks</li><div> | <img src="https://i.imgur.com/tskv8MM.png" width=50 height=40> |
| [PR #14](https://github.com/RocketChat/Apps.RC.AI.Programmer/pull/14) | <b>[Feature] Interactive UX to allow users to specify their configuration.</b> <br><br> <div align="left"> Highlights include:<ul><li> Users can make their configurations, switch between different LLMs, select their expected coding language.</li><li>Implemented the user interface for users to directly operate functions on.</li><li>Clarified the scope of available LLMs and add into options for users to choose from.</li><div> | <img src="https://i.imgur.com/tskv8MM.png" width=50 height=40> |
| [PR #20](https://github.com/RocketChat/Apps.RC.AI.Programmer/pull/20) | <b>[Feature]  Code Refinement & UX Enhancements</b> <br><br> <div align="left"> Highlights include:<ul><li> Users can type in their code refinement requirements and ask for a new code variantion.</li><li>Redesigned the contextual bar and modal windows for a better UX.</li><div> | <img src="https://i.imgur.com/tskv8MM.png" width=50 height=40> |
| [PR #28](https://github.com/RocketChat/Apps.RC.AI.Programmer/pull/28) | <b>[Feature]  Modal Window Design,  Prompt Engineering</b> <br><br> <div align="left"> Highlights include:<ul><li> Modal windows are enabled for UX stack and resolve contextual bar issues within app engine.</li><li>Prompt engineering tasks to make the prompts more effective and avoid injections.</li><div> | <img src="https://i.imgur.com/tskv8MM.png" width=50 height=40> |
| [PR #37](https://github.com/RocketChat/Apps.RC.AI.Programmer/pull/37) | [Feature] Code Sharing in RC Channel and Github via OAuth2  <br><br> <div align="left"> Highlights include:<ul><li>Setup OAuth2 mechanism for GitHub authentication.</li><li>The generated code pieces can be shared directly into RC channel.</li><li>The generated code pieces can be shared to Github repository</li><li>Redesign the entire UX to compatible with the new version of RC server.</li><div> | <img src="https://user-images.githubusercontent.com/70485812/189489748-ed27630f-36e7-4eb9-a9a4-e082d6894490.png" width=50 height=40> |


</div>

### Issues
    
<div align="center">
    
| Issue Link   | Description  | Status | 
| :-----------: | :------------------------------------:| :------:|
| [ISSUE #5](https://github.com/RocketChat/Apps.RC.AI.Programmer/issues/5) | [Refactor] Refactor the entire code base to support generic GPT-format LLM APIs | <img src="https://i.imgur.com/ihaDyZS.png" width=50 height=40> |
| [ISSUE #10](https://github.com/RocketChat/Apps.RC.AI.Programmer/issues/10) | [Feature] Add dropdown box on user interface for intuitive user configuration function | <img src="https://i.imgur.com/ihaDyZS.png" width=50 height=40> |
| [ISSUE #15](https://github.com/RocketChat/Apps.RC.AI.Programmer/issues/15) |[Feature] Support the use case of asking for code refinement| <img src="https://i.imgur.com/ihaDyZS.png" width=50 height=40> |
| [ISSUE #21](https://github.com/RocketChat/Apps.RC.AI.Programmer/issues/21) |[Feature] Design effective LLM prompts to avoid prompt injections| <img src="https://i.imgur.com/ihaDyZS.png" width=50 height=40> |
| [ISSUE #23](https://github.com/RocketChat/Apps.RC.AI.Programmer/issues/23) |[BUG] The elements on contextual bar will invoke incorrect roomid| <img src="https://i.imgur.com/ihaDyZS.png" width=50 height=40> |
| [ISSUE #29](https://github.com/RocketChat/Apps.RC.AI.Programmer/issues/29) |[Feature] Allow users to share code to Github repository| <img src="https://i.imgur.com/ihaDyZS.png" width=50 height=40> |
| [ISSUE #34](https://github.com/RocketChat/Apps.RC.AI.Programmer/issues/34) |[Feature] Configure OAuth2 features for authentication for Github connection| <img src="https://i.imgur.com/ihaDyZS.png" width=50 height=40> |
| [ISSUE #38](https://github.com/RocketChat/Apps.RC.AI.Programmer/issues/38) | [Feature] Design option to go back and choose another language | <img src="https://user-images.githubusercontent.com/70485812/189489748-ed27630f-36e7-4eb9-a9a4-e082d6894490.png" width=50 height=40> |


</div>

## Pushing Limits

- In order to make this project a success we have pushed Rocket.Chat to the limit. To improve the collaboration and bring the GitHub conversations to Rocket.Chat we decided to add a Code Editor component to Rocket.Chat. This task was not so easy and required a lot of research.  
- Adding any new Component to the UIKit and making it re-usable for other Rocket.Chat App developers requires us to go through a series of additions in different repositories and understanding how [fuselage](https://github.com/RocketChat/fuselage/tree/develop/packages/fuselage), [ui-kit](https://github.com/RocketChat/fuselage/tree/develop/packages/ui-kit), [fuselage-ui-kit](https://github.com/RocketChat/fuselage/tree/develop/packages/fuselage-ui-kit) and [Rocket.Chat.Apps-engine](https://github.com/RocketChat/Rocket.Chat.Apps-engine) work together to render components inside [Rocket.Chat](https://github.com/RocketChat/Rocket.Chat). 
- The detailed documentation on how we went about adding a Code Editor to Rocket.Chat can be seen over here : [Pull Request Reviews : Integrating Code Editor with Syntax Highlighting](https://github.com/RocketChat/Apps.Github22/wiki/Pull-Request-Reviews--:-Integrating-Code-Editor-with-Syntax-Highlighting).
- To use the GitHub App the full potential, feel free to use the version of the GitHub App which uses the upgraded version of Rocket.Chat and other packages with the CodeEditor Component, update the dependencies to use modified versions of the Rocket.Chat.Apps-engine, fuselgae, ui-kit and fuselage-ui-kit.
   - [GitHub App with CodeEditor Component](https://github.com/samad-yar-khan/Apps.Github22/tree/demoApp).
   - [fuselage, ui-kit and fuselage-ui-kit with Code Editor integration](https://github.com/samad-yar-khan/fuselage/tree/CodeEditorInputAce).
   - [Rocket.Chat with intigrated Code Editor in the fuselage-ui-kit package](https://github.com/samad-yar-khan/Rocket.Chat/tree/CodeEditorComponent).
 
- GitHub App with the integrated CodeEditor can be used on this [hosted server](https://gh-app.rocketchat.digital/). This server uses the above-mentioned, upgraded versions of fuselage, ui-kit, Rocket.Chat.Apps-engine and Rocket.Chat.

## Documentation 

I have documented all of the features mentioned above in the [Project Wiki](https://github.com/RocketChat/Apps.Github22/wiki). This documentation can prove useful to all future Rocket.Chat contributors working on Rocket.Chat Apps, Apps-engine, fuselage or the ui-kit. 

    

## 🎓 Mentors


I'm deeply grateful to my mentors for their invaluable guidance before and during GSoC. Their wisdom has imparted lifelong lessons, particularly in considering the end user's perspective and developing scalable products. My heartfelt thanks go to:

- **Sing Li** - [GitHub](https://github.com/Sing-Li). [LinkedIn](https://www.linkedin.com/in/sing-li-119716139/)
- **John Crisp** - [LinkedIn](https://www.linkedin.com/in/john-crisp-rocket-chat/)
- **Samad Yar Khan** - [GitHub](https://github.com/samad-yar-khan). [LinkedIn](https://www.linkedin.com/in/samad-yar-khan/)
- **Mustafa Hasan Khan** - [GitHub](https://github.com/mustafahasankhan). [LinkedIn](https://www.linkedin.com/in/mustafahasankhan/)



The entire Rocket.Chat community has been incredibly supportive. Special recognition goes to Devanshu Sharma, whose extensive assistance, especially in hosting the Rocket.Chat server with open-source LLM capabilities on safe dev server, was crucial for my GSoC'24 Demo Day presentation.

- **Devanshu Sharma** - [GitHub](https://github.com/Dnouv). 

A sincerely big thank to all of the Rocket.chat participant's help throughout GSoC. 🙏


## 💬 Connect With Me    

I am a self-motivated student pursuing Master’s degree of Computer Science at Texas A&M University in USA, with consolidated knowledge in both computer and finance fundamentals, and abundant hands-on experience in Full-Stack DevOps, Cloud, Data Analytics, Machine Learning (AIGC), Game Development, Vision, Graphics, and Finance. 

I am interested in Full Stack development and have been an open-source contributor at Rocket.Chat since March 2024.

Want to discuss about GSoC / Rocket.Chat / Open-source ? Let's connect!

<div align="center">

| **Student** | Ryan Zhou (Yuanlong Zhou) |
|:--------------------|:-------------------|
| **Organization** | [Rocket.Chat](https://rocket.chat/) |
| **Personal Page** | [ryanbowz's page](https://ryanbowz.github.io/) |
| **Project** | [GitHub App](https://summerofcode.withgoogle.com/programs/2024/projects/ZRkQn5bb) |
| **GitHub** | [@samad-yar-khan](https://github.com/RyanbowZ) |
| **LinkedIn** | [samad-yar-khan](https://www.linkedin.com/in/ryanbowz/) |
| **Email** | <a href="mailto:ryanbowz@outlook.com">ryanbowz@outlook.com</a> |
| **Rocket.Chat** | [samad.khan](https://open.rocket.chat/direct/ryan.zhou) |
       
</div>

</div>
