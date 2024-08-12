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

**It's glad to complete all of the above deliverables and meet expected goals in proposal within the GSoC period! 🎉**

## 📺 Demo

### Minimal Slash Command Interface

The Minimal Slash commands allow users to fetch repository details such as issues, pull requests and contributors and share them on the channel. This feature can be a lifesaver while trying to send repository details on a channel and focusing the conversation around recent issues and pull requests. 

- `/github Username/RepositoryName` will fetch an interactive message which lets you send - Repository Details, Recent Pull Requests, Recent Issues and Contributor List to the channee.
- `/github Username/RepositoryName repo` send repository details to the channel.
- `/github Username/RepositoryName issue` sends recent issues to the channel.
- `/github Username/RepositoryName pulls` sends recent pull requests to the channel.
- `/github Username/RepositoryName contributors`sends the list of repository contributors to the channel.



https://user-images.githubusercontent.com/70485812/189435287-1ae93110-6ba2-4dbc-ab2f-4774a76cecfd.mp4

### 🔐 GitHub OAuth

In the GitHub App I have implemented the Authentication mechanism using OAuth2. Here we have used the [GitHub OAuth](https://docs.github.com/en/developers/apps/building-oauth-apps/authorizing-oauth-apps) along with the [RocketChat Apps Oauth2 Client](https://developer.rocket.chat/apps-engine/adding-features/oauth2-client).     
- The users can log in to their github accounts simply by entering the slash command : `/github login` and clicking on the `login` button.
- As soon as the user is logged in, they receive a message and they can now use all the features which require authorized users.
- The users are automatically logged out after a period of time and the token is deleted. This was done to ensure the scalability of the feature in case of inactive users and to remove old OAuth tokens from the apps limited persistent storage. To achieve this we use the [RocketChat Apps Scheduler API](https://developer.rocket.chat/apps-engine/adding-features/scheduler-api).

https://user-images.githubusercontent.com/70485812/189439737-78e25abc-a78b-43da-af2f-21a6c061bc38.mp4

### 🖇️ Event Subscriptions

The Event Subscriptions feature of the GitHub App allows users to subscribe to repository events such as - new pull requests, new issues, new starts etc. Whenever a subscribed repository event takes place, the GitHub App bot will send a message to the subscribed room to describe the event.
This feature uses [GitHub WebHooks](https://docs.github.com/en/developers/webhooks-and-events/webhooks/about-webhooks) and [regestering an API end point](https://developer.rocket.chat/apps-engine/sample-app-snippets/registering-api-endpoints) in the App.
- The subscription modal can be triggered using `/github subscribe` command and then we can subscribe to multiple events for a repository.
- If multiple rooms subscribe to a repository, a single webhook is used and the different events are sent to different channels. This helps us avoid multiple requests to the server for the same event.
- For any new events which are added or deleted, the same webhook is updated keeping in mind the events which are subscribed by different rooms.


https://user-images.githubusercontent.com/70485812/189442882-afc3950e-4581-4728-b8c3-0e77e40ee61f.mp4

### 🔍 GitHub Search & Share

This feature was initially supposed to be an extension of the Slash Commands but we decided to make it a completely interactive experience. 
- The GitHub Search feature allows users to search GitHub for issues and pull requests using different filters such as labels, authors, state, milestones etc.
- Users can `Add` multiple search results and `Share` them on the channel along with a custom message.
- This feature improves the overall developer collaboration and helps share resources on the go.


https://user-images.githubusercontent.com/70485812/189448516-e846c836-551f-438e-960a-7c956d6b624f.mp4

### 🚩 Opening New Issues

The GitHub App allows users to open new issues from RocketChat. The `NewIssueModal` can be triggered by using `/github issue` and then entering the repository name in the launched modal.
- This feature enables the users to fetch the issue templates for a repository from GitHub, choose any of the given templates and open new issues with labels, assignees and the rest of the properties. 
- The most challenging part about this feature was finding a way to fetch the repository issue templates. 
- GitHub does not yet have an API to fetch issue templates, but they can be extremely important to maintain uniformity and separate different types of issues. To solve this problem, we used the [GitHub Repository Content API](https://docs.github.com/en/rest/repos/contents). 
- The issue templates are stored under `./github/ISSUE_TEMPLATES` on any repository, so to fetch the templates, we fetched all the files on that path, downloaded the code and prepopulated the `InputElement` with the selected template.
- If the files did not exist, we simply skipped the Template-Selection Modal.

https://user-images.githubusercontent.com/70485812/189451845-34437a50-1fc8-4360-8b64-d1beac7af277.mp4

### 🏦 Assigning Issues

This feature allows users to fetch repository issues and update the assignees on any issue. It also enables users to fetch and share multiple repository issues at a time. We can fetch and assign issues by using `/github issues` command and then entering the repository name.

https://user-images.githubusercontent.com/70485812/189450860-5847e585-059c-4bed-a988-d21c99734969.mp4

### 📰 Pull Request Reviews 

This feature allows users to review and merge pull requests inside RocketChat.

- Pull Request data can be viewed either by using the `/github search` method and finding the pull request or if the pull request number is known, we can simply use the slash command `/github Username/RepositoryName pulls pullNumber`.
- The pull request file changes, diffs, mergeaibility etc can also be seen. 
- A user can also see all the existing comments on the pull request and add new comments to the pull request directly from Rocket.Chat.
- While merging any pull request, the user can use any of the three methods - merge, rebase, squash.
- The user can also add a commit title and commit message while merging the pull request.
- In order to review the code changes, we integrated a Code Editor component to fuselage and extended the component to be the ui-kit and made it reusable for Rocket.Chat App developers by integrating to the Rocket.Chat.Apps-engine. This was the most difficult feature and took a lot of research and effort to understand how  Rocket.Chat.App-engine, fuselage, ui-kit and Rocket.Chat interact with each other to render some new ui-block for different Rocket.Chat.Apps. 
- The Documentation including all the details of the Code Editor Integration can be found in the [project wiki](https://github.com/RocketChat/Apps.Github22/wiki/Pull-Request-Reviews--:-Integrating-Code-Editor-with-Syntax-Highlighting).



https://user-images.githubusercontent.com/70485812/189453201-a886b5b5-84d9-4621-9f8d-23311a980591.mp4


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

    
<div align="center">

| **Feature** | **Documentation** |
|:--------------------|:-------------------|
| Authentication in Rocket.Chat Apps | [Authentication using RC OAuth2 Module and RC Apps Scheduler](https://github.com/RocketChat/Apps.Github22/wiki/Authentication-using-RC-OAuth2-Module-and-RC-Apps-Scheduler) |
| Adding new Elements to fuselage and UIKit | [Pull Request Reviews : Integrating Code Editor with Syntax Highlighting](https://github.com/RocketChat/Apps.Github22/wiki/Pull-Request-Reviews--:-Integrating-Code-Editor-with-Syntax-Highlighting) |
| Using WebHooks in Rocket.Chat Apps | [GitHub Event Subscriptions](https://github.com/RocketChat/Apps.Github22/wiki/GitHub-Event-Subscriptions) |
| GitHub Search (Using Rocket.Chat.App-engine persistent storage) | [GitHub Search and Share](https://github.com/RocketChat/Apps.Github22/wiki/GitHub-Search) |
| Opening New Issues (Fetching Issue Templates) | [Open New Issues from Rocket.Chat](https://github.com/RocketChat/Apps.Github22/wiki/Open-New-Issues-from-Rocket.Chat) |
| Pull Request Reviews (Using APIs and Modal in Rocket.Chat Apps)| [Merge Pull Requests and Add Comments](https://github.com/RocketChat/Apps.Github22/wiki/Merge-PRs-and-Add-Comments) |
| Assigning Issues (Using APIs, Modals and Persistent Storage in Rocket.Chat Apps) | [Assign and Sharing Issues from Rocket.Chat](https://github.com/RocketChat/Apps.Github22/wiki/Assigning-issues-from-Rocket.Chat) |

</div>

## 🎓 Mentors

A big big thank you to my mentors for their guidance before and throughout GSoC. 🙏

Rohan Lekhwani has been an inspiration throughout, his blogs and opensource work have been a lifesaver at each step of GSoC. I reached out to him over Linkedin last year and at the time I had no idea that he would end up being my mentor or that I would even be considered for GSoC'22. It would be accurate to say that I owe my GSoC'22 selection to him and his guidance. He has taught me how to own the project and juggle time between features to yield the best output possible.

Sing Li has taught me the importance of thinking beyond what has been done and pushing the limits even if the task at hand seems impossible. He has taught me the importance of communication and reaching out to people for guidance. His code reviews have made me a better developer and taught me how to think in terms of components and breaking down large problems into smaller problems and solving them one at a time. He motivated me to push myself and integrate the Code Editor inside Rocket.Chat, that became a highlighting feature for my project. This whole process was an enriching experience and can be considered a mini-GSoC Project of its own.

My mentors taught me things which will stay with me for life and I am beyond grateful for their guidance. Both of them have taught me how to think about the end user and make the product as scalable as possible. 

- **Rohan Lekhwani** - [GitHub](https://github.com/RonLek). [LinkedIn](https://www.linkedin.com/in/rohanlekhwani/)

- **Sing Li** - [GitHub](https://github.com/Sing-Li). [LinkedIn](https://www.linkedin.com/in/sing-li-119716139/)

Apart from my official Google Summer of Code Mentors, all Rocket.Chat community members have been extremely helful. 

I would like to thank Debdut Chakraborty for his amazing guidance and for helping me since my early days at Rocket.Chat. He spent hours to help me host the Rocket.Chat server with the modified fuselage, ui-kit and Apps-engine and without him my Demo at the Rocket.Chat GSoC'22 Demo day would not have been possible ❤️. Checkout the hosted server [over here](https://gh-app.rocketchat.digital/home).Feel free to reach out to him and tell him he's awesome !

- **Debdut Chakraborty** - [GitHub](https://github.com/debdutdeb). [LinkedIn](https://www.linkedin.com/in/debdut-chakraborty/)

## 💬 Connect With Me    

I am a senior year engineering student at Netaji Subhas University of Technology, Delhi. I am interested in Full Stack development and have been a contributor at Rocket.Chat since January 2022.

Want to discuss about GSoC / Rocket.Chat / Open-source ? Let's connect!

<div align="center">

| **Student** | Samad Yar Khan |
|:--------------------|:-------------------|
| **Organization** | [Rocket.Chat](https://rocket.chat/) |
| **Project** | [GitHub App](https://summerofcode.withgoogle.com/programs/2022/projects/dzvkQrUI) |
| **GitHub** | [@samad-yar-khan](https://github.com/samad-yar-khan) |
| **LinkedIn** | [samad-yar-khan](https://www.linkedin.com/in/samad-yar-khan/) |
| **Email** | <a href="mailto:smdyarkhan123@gmail.com">smdyarkhan123@gmail.com</a> |
| **Rocket.Chat** | [samad.khan](https://open.rocket.chat/direct/samad.khan) |
       
</div>

</div>
