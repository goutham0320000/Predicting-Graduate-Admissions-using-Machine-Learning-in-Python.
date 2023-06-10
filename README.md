# Predicting-Graduate-Admissions-using-Machine-Learning-in-Python.
May 2023 (version 1.79)

Show release notes after an update

Welcome to the May 2023 release of Visual Studio Code. There are many updates in this version that we hope you'll like, some of the key highlights include:

Read-only mode - Mark specific files and folders in your workspace as read-only.
'Paste as' options - Choose how you'd like item links pasted into the editor.
Automatic copy of external files - Drag or paste to Markdown adds new files to your workspace.
Default Git repo branch name - Use "main" as the default or override via a user setting.
Notebooks rich content search - Search based on Notebook output or filter on cell type.
Linked editing for JSX tags - Simultaneously change opening and closing JSX tags.
Preview: GitHub Copilot Chat improvements - Easily manage your chat session history. Inline chat "live preview."
VS Code at Microsoft Build 2023 - Catch up on the sessions in the YouTube playlist.
If you'd like to read these release notes online, go to Updates on code.visualstudio.com.

Insiders: Want to try new features as soon as possible? You can download the nightly Insiders build and try the latest updates as soon as they are available.

Accessibility
Verbosity settings
Additional accessibility.verbosity settings have been added to inform screen reader users how to interact with features when they are focused.

For GitHub Copilot, there are hints describing how to access the accessible help menus for the Copilot chat view and in editor code chat via:

accessibility.verbosity.chat
accessibility.verbosity.interactiveEditor
These help menus provide information about what to expect, how to navigate from the input box to other elements, and more.

Other new verbosity settings provide information for specific VS Code UI:

accessibility.verbosity.keybindingsEditor - when in the Keyboard Shortcuts editor.
accessibility.verbosity.notebook - when in a notebook.
The accessibility.verbosity settings are enabled by default (set to 'true') but you can silence them individually.

Settings editor
VoiceOver on macOS now reads the descriptions of enum setting options in the Settings editor. Try it out with enum settings such as files.autoSave and editor.accessibilitySupport.

onFocusChange option description of files.autoSave setting being displayed by VoiceOver's high-contrast textbox on macOS

Workbench
Readonly mode
In some development scenarios, it can be helpful to explicitly mark some of a workspace's folders or files as read-only. For example, if the folder or file contents is being managed by a different process (such as the node_modules folder that is managed by Node.js package manager), marking them are read-only can avoid inadvertent changes.

For this use case, there are new settings to mark file paths as read-only in the Explorer and in text and notebook editors:

files.readonlyInclude - Paths or glob patterns to make a file read-only if matching.
files.readonlyExclude- Paths or glob patterns to skip files from being read-only when they match files.readonlyInclude.
files.readonlyFromPermissions - Whether a file that has no write-permissions on disk should be read-only.
According to the rules of the settings, if a path is considered to be read-only, you cannot modify it from the Explorer (for example, delete it) and the text or notebook editor is read-only.


For more ad-hoc toggling of the read-only mode, there are new commands to change the mode for the current session only, overruling your setting configurations:

Set Active Editor Readonly in Session - Mark active editor read-only.
Set Active Editor Writeable in Session - Mark active editor writeable.
Toggle Active Editor Readonly in Session - Toggle between read-only and writeable.
Reset Active Editor Readonly in Session - Reset the session state.
Windows UNC host allowlist improvements
As part of an important security fix, VS Code introduced an allowlist for UNC hosts. This milestone we addressed many of the usability problems reported by Windows users when they have UNC paths in their day to day work with VS Code.

Dialog improvements
The confirmation dialog to allow a UNC host on startup now updates the security.allowedUNCHosts setting and adds the host when you select the checkbox.

Windows UNC allow dialog

In addition, clicking the Learn More button no longer closes the dialog.

New security.restrictUNCAccess setting
A new setting security.restrictUNCAccess lets you disable the UNC allowlist for hosts and restore the behavior to how it was before this security fix. We strongly advise against changing this setting, as it makes your system vulnerable again to the Information Disclosure Vulnerability.

New tab sizing option fixed
The workbench.editor.tabSizing setting has a new option fixed that makes each tab equal width. When space becomes limited, tabs will shrink equally up to a minimum. The new setting workbench.editor.tabSizingFixedMaxWidth sets the initial size of the tab.


In this mode, when you rapidly close tabs using the mouse, the widths of tabs remain stable to allow for closing each tab by clicking onto the same point. The width is then adjusted when you leave the mouse from the editor tab area.

Network quality indication
When you are connected to a remote machine, the best experience for VS Code remote editing capabilities requires a good network connection with low latency. In this milestone, we updated the remote indicator in the Status bar to give you some feedback when either latency is very high or the network connection appears to be offline.

High latency (web, desktop)
We periodically measure the latency to the remote you are connected to. When a certain threshold is hit, the remote indicator updates to reflect that.

Slow network detection shown in the right of the Status bar

Offline detection (web only)
If you are using a web browser to connect to a remote and you suddenly lose internet connection, the remote indicator updates to reflect that.

Web offline detection displaying "Network appears to be offline" message from the Status bar

Continue Working On
The Continue Working On feature allows you to store and retrieve working changes between VS Code development environments for the same repository, for example, when you upgrade from a local Git repository to a GitHub codespace, or when you switch between different machines for the same repository.

You can now transfer working changes between development environments for a GitHub repository even if it is configured with an HTTP remote in one environment and an SSH remote in another. Additionally, we have started to transfer additional workbench state, such as your Source Control view state preference, for a more seamless transition.

Editor
Paste as
When pasting a file into a text editor, there are multiple ways you might want to insert it. You may want an absolute path point to the file. You may want a path relative to the current workspace. Or you may even want something specific to the current editor's language, such as inserting a Markdown link to the file when pasting into Markdown. VS Code's new 'paste as' functionality gives you control over how the pasted content is inserted.

After pasting, VS Code now shows a small 'paste as' control if there are other ways the pasted content could have been inserted:


You can open the 'paste as' control by clicking on it or using the Ctrl+. keyboard shortcut. The paste selector goes away as soon as you start typing or move the cursor outside of the inserted text. You can also fully disable the drop selector control using "editor.pasteAs.showPasteSelector": "never".

When you paste content into a Markdown cell in a notebook, for example, the 'paste as' control lets you switch between:

Inserting the image as an attachment
Inserting a Markdown image reference
Inserting a relative path (for files in the workspace)
Inserting an absolute path
If you prefer selecting how content in the clipboard should be pasted before actually pasting, you can instead use the new Paste As... command. This lets you select how the content should be pasted:

Using the Paste As... command to select how content is pasted

Quick suggestions and snippets
Quick suggestions mean that VS Code shows suggestions as you type, without having to press Ctrl+Space. This feature is widely popular, around 90% of all suggestion sessions are started by typing. A large number of suggestions are accepted via Tab (versus Enter and typing accept characters).

When a snippet is being inserted, the Tab key is used to navigate between snippet placeholders. Now, when quick suggestion becomes active while a snippet is being inserted, the Tab key can accept a completion or navigate to the next snippet placeholder. To resolve this conflict, there is the editor.suggest.snippetsPreventQuickSuggestions setting to disable quick suggestions when a snippet is inserted. It defaulted to true and as long as this setting existed, we received feedback that it was confusing. So we have decided to change its default value to false, so that typing inside a snippet placeholder will trigger quick suggestions.

You can then use the following keystrokes:

Press Tab to accept a completion.
Press Escape to hide quick suggestions.
And Tab without suggestions navigates to the next snippet placeholder.
Terminal
Automatic shell integration for fish shell
Shell integration and its enhanced user experience will now automatically activate for fish shell. You may need to update fish for this to work.

Shell integration in fish enables several features

Overline support
The overline escape sequences (SGR 53, SGR 55) specified in ECMA-48 are now supported in the terminal. The most common use of this sequence is to add a line above an app's "status bar" on the bottom row of the terminal.

The overline feature is similar to underline but will draw a line on top of the text

Source Control
Default branch name
Starting with this milestone, all new Git repositories created using VS Code set main as their default branch. If you prefer a different name for the default branch, you can change it with the git.defaultBranchName setting. When the setting is set to empty, VS Code defers to the default branch name configured in Git. Publishing a folder to GitHub also honors the default branch name configured on GitHub.

Branch picker integration with vscode.dev and GitHub
You can now checkout a branch in vscode.dev or open it on GitHub.com from the branch picker on VS Code desktop.

In the short video below, each branch listed in the branch picker dropdown has buttons on the right to either Open on GitHub or Checkout on vscode.dev.


Similarity threshold
Git status uses a similarity index (number of additions/deletions compared to the file's size) to determine whether an add/delete pair is considered a rename. You can now configure the similarity threshold with the git.similarityThreshold setting, which takes a value between 0 and 100. The default value is 50.

Notebooks
Rich content search
You can now search for rich content in open notebooks from the Search control. If your notebook is open, the Search control shows results based on how it appears in the notebook editor (rather than searching the content of the raw source file). This also allows for replacing text in the notebook inputs.


Using the new notebook search toggle, you can also filter which types of cell content you would like to search in.


Improved cell output interaction
The new context key notebookOutputInputFocused was added to determine if a text box within a cell output has focus, so that raw hotkeys a/b/j/k can safely be used while the output has focus. Focusing on an input box prevents those hotkeys from triggering.


Format on Run
Notebooks now can format cells upon cell execution. This will trigger using Run Cell, Run All, Run Above/Below, and combined kernel+run commands. This feature can be turned on via setting "notebook.formatOnCellExecution": true.


Code Actions on save
Notebooks now support Code Actions being run upon save. Code Actions can be specified under the notebook.codeActionsOnSave setting. Extension authors can define providers using the standard typings for cell level Code Actions, or use the new notebook. prefix to define Code Actions that manage the entire notebook. You can review the clean-nb-imports-ext sample extension to learn how extensions can use this new setting.

Languages
TypeScript 5.1
VS Code now ships with TypeScript 5.1.3. This major update brings new TypeScript language features, better performance, and many important improvements and bug fixes. You can read about TypeScript 5.1 on the TypeScript blog.

Linked editing for JSX tags
With linked editing, when you change an opening JSX tag VS Code will automatically update the corresponding closing tag. This can be a great time saver:


The feature is off by default but can be enabled by setting:

"editor.linkedEditing": true

You can also explicitly start linked editing with the Start Linked Editing command.

Rename matching JSX tags using F2
When you trigger rename on a JSX tag, VS Code now renames just the matching tag instead of trying to update all references to the tag:


This requires TypeScript 5.1+ and matches how rename works in HTML.

You can disable this behavior using javascript.preferences.renameMatchingJsxTags and typescript.preferences.renameMatchingJsxTags.

JSDoc @param completions
When writing JSDoc comments, VS Code now shows suggestions for all missing parameters:

JS Doc @param completions in a TypeScript file

This can help you quickly fill in the documentation.

In JavaScript files, @param completions create placeholders for the parameter type description:


Copy external media files into workspace on drop or paste for Markdown
Want to add an image or video into a Markdown document? Instead of wasting time first manually copying the file into your workspace and then adding a link to it, now you can just drop or paste the file into your Markdown. If the file currently isn't part of the workspace, VS Code will automatically copy the file into your workspace and insert a link to it:


This also works great for image data in the clipboard. For example, if you take a screenshot with the Snipping tool on Windows, you can press Paste in a Markdown file and VS Code will create a new image file from the clipboard data and insert a Markdown image link to the new file. This also works on macOS if you hold the Ctrl key while taking a screenshot to copy it to the clipboard.

You can also customize the behavior of this feature using a few settings:

markdown.copyFiles.destination
The markdown.copyFiles.destination setting controls where new media files are created. This setting maps globs that match on the current Markdown document to image destinations. The image destinations can also use some simple variables. See the markdown.copyFiles.destination setting description for information about the available variables.

For example, if we want every Markdown file under /docs in our workspace to put new media files into an images directory specific to the current file, we can write:

"markdown.copyFiles.destination": {
  "/docs/**/*": "images/${documentBaseName}/"
}

Now when a new file is pasted in /docs/api/readme.md, the image file is created at /docs/api/images/readme/image.png.

You can even use simple regular expressions to transform variables in a similar way to snippets. For example, this transform uses only the first letter of the document file name when creating the media file

"markdown.copyFiles.destination": {
  "/docs/**/*": "images/${documentBaseName/(.).*/$1/}/"
}

When a new file is pasted into /docs/api/readme.md, the image is now created under /docs/api/images/r/image.png.

markdown.copyFiles.overwriteBehavior
The markdown.copyFiles.overwriteBehavior setting controls whether newly created media files overwrite existing files.

By default, VS Code will never overwrite existing files. Instead if you have a file called image.png and try pasting it into a Markdown document in a workspace where an image.png already exists, VS Code will instead create a new file called image-1.png. If you then try pasting another file called image.png, it will instead be created as image-2.png.

If you prefer having existing files be overwritten by new files, set "markdown.copyFiles.overwriteBehavior": "overwrite". Now VS Code will always use the original file name, overwriting any existing files that that path.

Disabling copying files into the workspace
VS Code will only try copying files into your workspace if they are not already part of workspace. Additionally, we currently only copy media files (images, videos, audio) into the workspace.

However if you find this new behavior too intrusive, you can disable it for both drop and paste by setting:

"markdown.editor.drop.copyIntoWorkspace": "never"
"markdown.editor.filePaste.copyIntoWorkspace": "never"

IntelliSense for HTML paths in Markdown files
Many Markdown dialects allow raw HTML tags to be used in Markdown documents. In this update, we've extended most of VS Code's Markdown IntelliSense features to file paths used in these HTML tags. This includes support for:

Path completions.
Finding all references to a linked to file.
Automatically updating file paths when a file is renamed or moved.
Safely renaming files using F2.
Validating that the linked to file exists in the workspace.
Finding all references to an image file used in an HTML tag

Insert audio into Markdown
When you drag and drop or copy and paste an audio file into a Markdown document, VS Code now inserts an <audio> element.

Syntax highlighting for JSON with Lines (JSONL) files
JSON with Lines describe a sequence of JSON objects separated by newline characters. If the file extension jsonl is used, VS Code provides syntax highlighting.

Remote Development
The Remote Development extensions, allow you to use a Dev Container, remote machine via SSH or Remote Tunnels, or the Windows Subsystem for Linux (WSL) as a full-featured development environment.

Highlights include:

Open new Remote connections (via a Remote Tunnel, to a Dev Container) in either the current or a new VS Code window.
Easier workflow to make a forwarded port public.
Preliminary support for connecting to WSL from VS Code for the Web (vscode.dev).
You can learn about new extension features and bug fixes in the Remote Development release notes.

Contributions to extensions
GitHub Copilot
Note: To get access to the chat view and inline chat, you'll need to sign up for the GitHub Copilot chat waitlist.

Use Copilot Chat in Stable VS Code
Previously, you had to use VS Code Insiders to use Copilot Chat. As of VS Code 1.79, you can use Copilot Chat in stable VS Code as well. You will still have to install the GitHub Copilot Nightly extension.

Editor chat
We have improved editor chat, most notably we have changed its default mode to be "livePreview". In this mode, changes are applied directly to the document and shown with an embedded diff view. Let's look at the example below:

A new property was added to the IUserFriendlyStatusItemEntry type and
Copilot updated the isUserFriendlyStatusItemEntry check accordingly.
The reply is shown in the editor using an embedded diff view. Its right hand side is editable and checked by VS Code's language extensions.
This lets you spot an error in the reply (below the isMarkdownString function doesn't exist) and you can fix it before accepting the suggestion.
Copilot inline chat suggestion with proposed code change displayed as a live preview

Notebook improvements
We have improved the chat experience in notebook editors this month. When using Copilot in a notebook document, Copilot can use the notebook context to provide more relevant suggestions. For example, the code suggestions use variables or modules defined in previous cells without recreating or re-importing them.


When running notebook cells, Copilot now also provides suggestions for cell execution failures. You can display these by selecting the Fix using Copilot action on the cell status bar.


The Copilot suggestions are also accepted automatically on cell execution, so you don't have to accept them manually.

GitHub Pull Request and Issues integration
When the GitHub Pull Requests and Issues extension is installed and enabled and you are viewing a review thread, it is now possible to directly apply a review comment using Copilot. You can do this via the Apply Suggestion with AI button in the comment menu.


Experimental Quick Question experience

Theme: Panda Theme (preview on vscode.dev)

This iteration, we experimented with using chat to ask quick programming questions without leaving context. If you have access to the chat experience, you can enable this feature with the following setting:

"chat.experimental.quickQuestion.enable": true

Feature overview:

Ask Copilot a quick question.
Toggle the experience with Ctrl+Shift+I (state is remembered for 30s so you can easily show, hide, and show again).
An Open in chat button for continuing the conversation to a long form chat in the chat view.
Delete chat entry
You can now delete a chat request/response pair by clicking the X icon in the chat request.

A chat request with X icon

Why would you want to do this? Sometimes, Copilot provides a response that is off topic or incorrect. You can ask your question again, but removing the bad response from your session's chat history may also help keep the conversation on track. There is also a limit to the amount of context that can be included with each chat request, so removing a long poor response might help save your context budget for more useful information.

Move chat session from sidebar to editor
It was already possible to open a chat session in an editor by running the Chat: Open Editor command, but now it is also possible to move chat sessions back and forth between the sidebar and editor. You can find the Open Session in Editor and Open Session in Sidebar commands under the "..." menu in the chat view title or the editor title menus.


Chat session history
Your chat sessions are now saved to history, which you can browse by selecting the Show History button in the chat view title menu. You can select a history entry to load that conversation into a chat editor, and then seamlessly continue where you left off. You can remove sessions from history by clicking the X button on each row.

Export chat sessions to JSON file
We've added a command, Chat: Export Session, which exports the current focused chat session to a JSON file. You can then run the Chat: Import Session command to import this session and continue your conversation. You can check this file into your repo, share it with others, or just save your conversation for reference later. Note that when you are continuing your conversation in an imported chat session, those new messages won't be saved unless you export the session again.

Codeblock navigation and keybindings
We've added some commands and keybindings that make it easier to work with codeblocks in chat responses. Chat: Next Codeblock (F9) and Chat: Previous Codeblock (Shift+F9) move the cursor to the next or previous codeblock in the current chat response. When a codeblock is focused, the commands in the codeblock toolbar can also be invoked from the Command Palette, or you can assign keybindings to them. Run in Terminal has a keybinding assigned by default, Ctrl+Alt+Enter. And the Copy command will now be run when you press the normal copy keybinding in the codeblock without having a selection.


We've also added keybindings to focus the chat window (unassigned) and to clear the chat session (Ctrl+L).

Copilot YouTube playlist
To learn more about GitHub Copilot as well as tips and tricks and best practices, have a look at the VS Code Copilot Series on YouTube. There you'll find an introduction to GitHub Copilot, language-specific usage, and guidance on effective prompting when using Copilot for development.

Python
Run Python file in dedicated terminal
The Python extension will now create a new terminal for each file you run using the Run button on the top of the editor or the Python: Run Python File in Terminal command, and will keep using this file's "dedicated" terminal every time you re-run it.


Any time you wish to run the same file in a separate terminal, you can run select Python: Run Python File in Dedicated Terminal under the Run button menu.

Options under the run button menu

Test discovery and run rewrite
This month, we are beginning the roll out of our testing rewrite as an experiment. This rewrite redesigns the architecture behind test discovery and execution for both unittest and pytest in the extension. While it does not provide any additional functionality exposed to the user, it reduces buggy behavior and opens up new functional opportunities moving forward. The rewrite is being rolled out behind the experiment pythonTestAdapter, which you can opt in and out of using python.experiments.optInto in your settings.json. Eventually, we plan to remove this setting and adopt this new architecture. If you have any comments or suggestions regarding this experiment or rewrite, you can share them in the vscode-python repository.

Configurable indexing limits with Pylance
There's a new Pylance setting that allows you to configure the file count limit for indexing: "python.analysis.userFileIndexingLimit", which is set to 2000 by default. This setting can be helpful when working with very large projects and you're willing to compromise performance for an enhanced IntelliSense experience.

Jupyter
Resume execution of cells against remote Jupyter kernels
The Jupyter extension now supports resuming execution of cells against remote Jupyter kernels, if the cell is still busy executing, even when reopening the Notebook after having shutdown VS Code.

For instance, assume you execute a long running section of code such as training of a model against a remote Jupyter kernel. This could take a few minutes or longer, so you might decide to shut down VS Code in the interim. A few minutes later VS Code is restarted with the same notebook opened and if the cell is still busy executing, this state is reflected in the Notebook cell and any new output is displayed in the cell output.

If on the other hand, the cell completed execution while VS Code was shut down, the outputs generated in the interim would not be preserved in the notebook. Resuming executions in this manner and displaying new output is limited to simple output such as plain text, HTML, images, images, and the like. Restoring the state of widgets and other such complex outputs is not supported.

Resuming notebook cell execution after closing and reopening VS Code

GitHub Pull Requests and Issues
There has been more progress on the GitHub Pull Requests and Issues extension, which allows you to work on, create, and manage pull requests and issues. Highlights include:

Two new actions for viewing diffs of checked out PRs: Compare Base With Pull Request Head (readonly) and Compare Pull Request Head with Local.
The new setting "githubPullRequests.pullPullRequestBranchBeforeCheckout" can be used to turn off pulling a previously checked out PR branch when checking out that same branch again.
Review the changelog for the 0.66.0 release of the extension to learn about the other highlights.

Preview features
Project wide JS/TS IntelliSense on insiders.vscode.dev
vscode.dev is a lightweight version of VS Code running fully in your browser. This iteration, we've significantly enriched vscode.dev's JavaScript and TypeScript support so that it can analyze all files in your workspace instead of being limited to currently opened files. This greatly improves navigation through code, letting you Go to Definition and Find All References to a symbol. It also improves IntelliSense by making sure settings from your tsconfig.json / jsconfig.json are respected. We even now support auto-imports while writing code.

In the image below, the References view is displaying all references to ITextDocument in the workspace.

Find All References in a TypeScript project on vscode.dev

These new IntelliSense features work for folders you open from your local machine and in GitHub repos you open using vscode.dev's built-in GitHub Repositories extension.

Keep in mind that there are still a few limitations with JS/TS IntelliSense on vscode.dev:

There is not currently IntelliSense support for third party libraries.
There is not currently support for automatic type acquisition for JavaScript projects.
Because of the above limitations, all typing errors are disabled on vscode.dev.
Project wide IntelliSense is currently only enabled on the Insiders version of vscode.dev: insiders.vscode.dev. This feature is currently disabled on github.dev.
We plan on addressing these limitations going forward, and are excited to continue enriching our JavaScript and TypeScript support on the web!

Images in the terminal
There is now experimental support for images in the terminal. Images in a terminal typically work by encoding the image pixel data as text, which is written to the terminal via a special escape sequence. The current protocols that are supported are sixel and the inline images protocol pioneered by iTerm.

Enable this feature by setting:

"terminal.integrated.experimentalImageSupport": true

Once enabled, to test it, you can download and cat a .six example file from the libsixel repository:

Running cat with a sixel file will print an image

Or use the imgcat python package or imgcat script with a png, gif or jpg file:

Running imgcat with a png file will print the image

The current limitations of this feature are:

Serialization does not work, so reloading a terminal will not retain any images (tracked in jerch/xterm-addon-image#47).
Copying the selection as HTML does not include the selected image (tracked in jerch/xterm-addon-image#50).
Animated gifs don't work (tracked in jerch/xterm-addon-image#51).
Images that are shorter than a cell will not work properly, this is a design flaw with the sequences and also occurs in XTerm.
TypeScript 5.2 support
This update includes support for the upcoming TypeScript 5.2 release. Check out the TypeScript 5.2 iteration plan for more details about what the TypeScript team is currently working on. Some exciting upcoming tooling highlights include:

A new Inline constant refactoring.
A new Move to file refactoring that lets you move a symbol into an existing file.
To start using the TypeScript 5.2 nightly builds, install the TypeScript Nightly extension.

Move to file refactoring for JavaScript and TypeScript
The Move to file refactoring in TypeScript 5.2 nightly lets you move a class, function, or constant into an existing file. This will also automatically update all references to the symbol and also update imports as needed:


When you select Move to file, VS Code shows you a list of all files in the current TypeScript or JavaScript project. You can start typings to quickly find the file you want.

Alternatively, you can use Select existing file... to select a file using the normal file picker or Enter new file path... to specify a new file that should be created.

This feature is still being actively developed, so give it a try and share your feedback!

WebAssemblies in VS Code for the Web
To add more programming language support to vscode.dev, the VS Code team has been investigating how to run general WebAssembly in VS Code for the Web. If you are interested in this approach and want to learn more, check out the recent VS Code and WebAssemblies blog post.

Extension authoring
Improved vscode.fs performance for local files
When you are using vscode.fs API to work with files (you should!), operations to files that are local to the extension host will now resolve much faster.

Previously the extension host would delegate these operations to the VS Code client for execution, but now they execute directly inside the extension host, saving round trips.

Stricter Status bar API
The API to create a Status bar item createStatusBarItem lets extensions pass an identifier. This identifier is used to control hiding and showing the Status bar item. The identifier should be unique for the extension but until now this wasn't enforced. With this release, we make this a little more strict and Status bar items that are created by the same extension with the same identifier will now be merged into one.

Tasks
The task presentation option to close the terminal on task completion has been finalized.

Proposed APIs
Every milestone comes with new proposed APIs and extension authors can try them out. As always, we want your feedback. Here are the steps to try out a proposed API:

Find a proposal that you want to try and add its name to package.json#enabledApiProposals.
Use the latest @vscode/dts and run npx @vscode/dts dev. It will download the corresponding d.ts files into your workspace.
You can now program against the proposal.
You cannot publish an extension that uses a proposed API. There may be breaking changes in the next release and we never want to break existing extensions.

EnvironmentVariableCollection.description
This proposal allows specifying a description for EnvironmentVariableCollection, displayed to the user in the terminal tab hover, explaining what exactly the change is doing.

// Example of what the Git extension could use
context.environmentVariableCollection.description = 'Enables a Git authentication provider';

Environment variable collection descriptions are explained in a terminal tab's hover

EnvironmentVariableMutator.options
This proposal adds options that can be provided to EnvironmentVariableMutators, allowing you to specify exactly when the environment variable change is applied, either on process creation or in the shell integration script (after shell init scripts have run).

const collection = context.environmentVariableCollection;
// Apply only when the process is created
collection.replace('FOO', 'bar');
// Apply only during the shell integration script
collection.replace('FOO', 'bar', { applyAtProcessCreation: false, applyAtShellIntegration: true });
// Apply twice, during process creation and the shell integration script
collection.replace('FOO', 'bar', { applyAtProcessCreation: true, applyAtShellIntegration: true });

Share provider
The Share API proposal allows extensions to provide ways to share resources in VS Code.

Share provider results are currently surfaced as a top-level Share... Command Palette action and as a new icon near the Command Center, provided you have opted in with "workbench.experimental.share.enabled": true and "window.commandCenter": true.


You can leave feedback in the API proposal issue #176316.

Static Status bar items
Status bar items can now be contributed statically via package.json#contributes/statusBarItems. With this contribution point, an extension can delay its activation and only activate when the Status bar item is interacted with, for example, on the command. Once activated, extensions can access their static Status bar items via the vscode.window.createStatusBarItem API.

workspace.save and workspace.saveAs
The Save Editor API proposal allows extensions to trigger the flow of saving an editor either to its resource or by asking the user to provide a resource.

All the methods for saving will return the resulting Uri or undefined if the operation was canceled. Untitled files will always ask the user for a destination unless a path is already associated.

Authentication authGetSessions proposed API
As we move closer to having Multiple GitHub account support, we have a new proposed authentication API that lets your extension get all accessible sessions for a specific set of scopes. The proposal for these API additions has several things to call out:

The introduction of vscode.authentication.getSessions to get sessions for each account that your extension has access to. If you want to request an additional account, use { createIfNone: true, clearSessionPreference: true } to ask the user to choose an account.
The forceNewSession property now can take in a { sessionToRecreate: session } object so that consuming extensions can specify the exact session they want to be recreated.
The createSession function that an Auth Provider implements will now get passed in the session to recreate (using the extension's session preference if true is used for the value of forceNewSession).
There is still more work involved to make this ready for adoption in the GitHub Authentication extension so if you're interested, you can follow along and provide feedback in the issue that tracks this proposal.

Window Activity API
A new API is available to notify extensions if the window becomes active or inactive. This can be used to dispose of or create persistent resources or processes that can be idled to save resources.

This is implemented by the addition of a new active boolean to the existing WindowState type.

vscode.window.onDidChangeWindowState(state => {
  if (state.active && !longRunningProcess) {
    longRunningProcess = startLongRunningProcess();
  } else if (!state.active && longRunningProcess) {
    longRunningProcess.end();
    longRunningProcess = undefined;
  }
})

Engineering
Electron sandbox enabled for all users
We are happy to announce that the Electron sandbox is rolling out to all of our users. This was a journey that started in early 2020 and now finally comes to an end. You can refer to the Migrating VS Code to Process Sandboxing blog post for more details.

Extension host restart participation
Certain actions in the workbench can lead to the extension host restarting without reloading the current window. For example, when you switch profiles, VS Code restarts the extension host to handle running a different set of extensions for that profile.

Some custom and notebook editors however may no longer be functional after having switched profiles because a required extension is not installed in that profile. If the editor has unsaved changes, this could cause data loss. As a fix, components in VS Code can now participate in extension host restarts and make sure any unsaved changes are saved before the extension host restarts.


We plan to further develop this experience in the next milestone so stay tuned for more!

Windows 8 and 8.1 support has ended
As mentioned in our v1.77 release notes, v1.79 is the last release that supports Windows 8 / Windows Server 2012 and Windows 8.1 / Windows Server 2012 R2. Refer to our FAQ for additional information.

Milestone automation
We have implemented automated milestone replication throughout all of our GitHub repositories. This means that the monthly milestones established in microsoft/vscode serve as the foundation for all other milestones that are created and maintained.

VS Code at Microsoft Build
If you didn't get a chance to watch Microsoft Build 2023 live, you can catch up on the keynotes and sessions on the Microsoft Developer YouTube channel.

Some sessions of particular interest to VS Code users include:

Next generation AI for developers with the Microsoft Cloud
Develop from anywhere with Visual Studio Code
Pragmatic techniques to get the most out of GitHub Copilot
Inject the power of the cloud and AI into your development workflow
Notable fixes
165933 [emmet] http-equiv="X-UA-Compatible" in 2023
181889 treeView.reveal with expand: 3 only expands the first level 3 folder
Thank you
Last but certainly not least, a big Thank You to the contributors of VS Code.

Issue tracking
Contributions to our issue tracking:

@gjsjohnmurray (John Murray)
@starball5 (starball)
@IllusionMH (Andrii Dieiev)
@tamuratak (Takashi Tamura)
Pull requests
Contributions to vscode:

@akbyrd (Adam Byrd): Fix issues with msCompile problem matcher PR #182167
@ashgti (John Harrison): Fixing an issue in debug output prompts to not show up as 'object Object' PR #181964
@benibenj (Benjamin Simmonds): TreeView Checkbox State set to 0 fixed PR #183342
@bitekas (Viktor Korsun): Fixing the Pseudoterminal onDidClose example PR #180026
@dan-petty (Daniel Petty): Fix cannot specify custom path for built-in profiles on Windows PR #175464
@dcourv (Dylan): Fixes #181207 - Add padding to extension viewer bottom PR #181723
@DoctorKrolic: Add JSON Lines language definition PR #183035
@dyedgreen (Tilman Roeder): Fix: Encode paths as URI components when opening a folder or workspace PR #182398
@ElectricRCAircraftGuy (Gabriel Staples): all color themes: treat comment docstrings as comments too PR #182162
@gjsjohnmurray (John Murray)
Fix spelling in description of security.restrictUNCAccess setting PR #182842
Prevent duplicate text in workspace folder picker when path has no parent (fix #183418) PR #183427
@hermannloose (Hermann Loose)
Add separate overview ruler colors for resolved & unresolved comments PR #181520
Fix color descriptions for comment icons PR #181628
@iAnujParajuli (Anuj Parajuli): Adds #181652 html audio tag for audio file PR #183328
@jacekkopecky (Jacek Kopecký)
Add settings for fixed-width tabs PR #181729
fixed tab sizing: restore tab widths when the last tab is closed PR #183188
@jackpunt (Ganesh)
Add a setting to mark file(s) readonly (nonEditable)PR #161716
precedence for isReadonly() for #181708 PR #181955
@jairbubbles (Julien Richard): Fix context menu for deleted lines in diff inline mode PR #182542
@jeanp413 (Jean Pierre)
Fixes ITerminalService#getActiveOrCreateInstance returns a disposed terminal PR #180451
Fixes empty terminal editor after reload PR #182121
Fixes terminal doesn't take editor background color into account PR #182557
Fix Improve terminal find behavior when there are more than 1000 results PR #182917
Fix cannot hide terminal find widget when pressing esc PR #183090
Fix Terminals aren't persisting anymore PR #183516
@Juneezee (Eng Zer Jun): refactor(userDataSync): replace indexOf with includes PR #182635
@markw65
Fix a task startup race PR #180546
Make _activeTasks synchronous wrt _executeTask PR #180617
@max06 (Flo): Fix: Changed bash-syntax to fish-syntax in shellIntegration PR #181637
@r3m0t (Tomer Chachamu)
Interactive window- don't leave space for insert toolbar PR #181949
Prevent ligatures between inlay hints and editor contents (Fix #170449) PR #182379
@rehmsen (Ole): Add F10 keybinding for debugger step, even on Web. PR #183510
@soulshined (David Freer): PHP Snippets Quality of Life and Continuity PR #174889
@TheSylvester (Sylvester Wong): Added use snippet body as a description when none is provided #181115 PR #181381
@tisilent (xie jialong 努力鸭)
Modify innerWidth PR #180480
Fix contributed profile icons PR #182615
fix #182702 PR #182705
@ugultopu (Utku Gultopu): Add similarity threshold option to Git extension PR #178266
@vadimcn: Preserve breakpoint ids in workspace state PR #182704
@Viijay-Kr (Vijaya Krishna): fix: #169151 fallback to editor hover if no breakpoint PR #181274
@Yash-Singh1 (Yash Singh): feat: .vuerc as json file PR #153017
@yshaojun: fix: fix perl bracket pair by adding unbalancedBracketScopes(#168110) PR #181203
Contributions to vscode-css-languageservice:

@romainmenke (Romain Menke): css nesting : increase support PR #345
Contributions to vscode-js-debug:

@NotAndOr (notandor): Launch browser with argument user-data-dir specified without directory junction. PR #1656
Contributions to vscode-pull-request-github:

@kabel (Kevin Abel): Simplify AuthProvider enum PR #4779
@SKPG-Tech (Salvijus K.): Add missing index in template PR #4822
@unknovvn (Andzej Korovacki): Use git setting to fetch before checkout in checkoutExistingPullRequestBranch PR #4759
Contributions to monaco-editor:

@dlitsman (Dmitry Litsman): Extend the "Rendering Glyphs In The Margin" example to include a transparent color note. PR #3945
@dneto0 (David Neto): Avoid a hack in the WGSL lexer PR #3887
@spahnke (Sebastian Pahnke)
JS, TS Add Monarch support for private identifiers PR #3919
JS Add static keyword PR #3922
@titouanmathis (Titouan Mathis): Webpack Plugin Fix CJS being injected in ESM files PR #3933
