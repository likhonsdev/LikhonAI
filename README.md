# LikhonAI
What's on your mind?
Ask LikhonAI anything - from coding help to creative inspiration.
*Getting Started
First you need to install the module, we ship exclusively through npm so you need that installed and then add xterm.js as a dependency by running:

npm install @xterm/xterm
To start using xterm.js on your browser, add the xterm.js and xterm.css to the head of your html page. Then create a <div id="terminal"></div> onto which xterm can attach itself. Finally instantiate the Terminal object and then call the open function with the DOM object of the div.

<!doctype html>
  <html>
    <head>
      <link rel="stylesheet" href="node_modules/@xterm/xterm/css/xterm.css" />
      <script src="node_modules/@xterm/xterm/lib/xterm.js"></script>
    </head>
    <body>
      <div id="terminal"></div>
      <script>
        var term = new Terminal();
        term.open(document.getElementById('terminal'));
        term.write('Hello from \x1B[1;3;31mxterm.js\x1B[0m $ ')
      </script>
    </body>
  </html>*** Monaco - The Editor of the Web. The Monaco Editor is the code editor that powers VS Code. A good page describing the code editor's features is here. It is ... Extensible Code Editor
CodeMirror is a code editor component for the web. It can be used in websites to implement a text input field with support for many editing features, and has a rich programming interface to allow further extension.

1
2
3
⌄
function hello(who = "world") {
  console.log(`Hello, ${who}!`)
}
This is a CodeMirror field, configured for editing JavaScript code.

Features
Accessibility
Works well with screen readers and keyboard-only users.

Mobile Support
Use the platform's native selection and editing features on phones.

Bidirectional Text
Support mixing of right-to-left and left-to-right text.

Syntax Highlighting
Color code to reflect syntactic structure.

Line Numbers
Display gutters with line numbers or other information next to the code.

Autocompletion
Provide language-specific completion hints in the editor.

Code Folding
Temporarily hide parts of the document.

Search/Replace
Editor-specific search, regexp search, and replace functionality.

Full Parsing
Detailed parse trees allow many types of language integration.

Extension Interface
Robustly implement demanding editor extensions.

Modularity
Most features are implemented on top of a generic public API.

Speed
Remains responsive even on huge documents and long lines.

Bracket Closing
Automatically insert matching brackets during typing.

Linting
Show error and warning messages in the editor.

Flexible Styling
Mix font styles and sizes, add widgets in the content.

Theming
Import or create custom visual editor styles.

Collaborative Editing
Allow multiple users to edit the same document.

Undo History
Undo and redo functionality with collab editing support.

Multiple Selections
Select and edit multiple ranges of the document at once.

Internationalization
Provide custom text to display or announce to the user.

...and more
Find a full description of the library's features in the docs.

About
CodeMirror is open source under a permissive license (MIT). It is being developed on GitHub. Contributions are welcome.

If you are using CodeMirror commercially, there is a social (but no legal) expectation that you help fund its maintenance. Start here.

The library supports browsers up from Internet Explorer 11 (with some polyfills).

Discussing the project, or asking questions, is best done on the forum. Bugs should be reported through the issue tracker. We aim to be an inclusive, welcoming community. To make that explicit, we have a code of conduct that applies to communication around the project.

Language Support
A full parser package, often with language-specific integration and extension code, exists for the following languages:

Angular
CSS
C++
Go
HTML
Java
JavaScript
JSON
Liquid
Markdown
PHP
Python
Rust
Sass
SQL
Vue
WAST
XML
YAML

Repository files navigation
README
Code of conduct
Apache-2.0 license
Component toolkit for live running code editing experiences

Sandpack
Sandpack is a component toolkit for creating your own live running code editing experience powered by CodeSandbox.

Learn more about Sandpack

Edit in CodeSandbox

Sandpack Client
This is a small foundation package that sits on top of the bundler. It is framework agnostic and facilitates the handshake between your context and the bundler iframe.

Read more

Repository files navigation
README
Code of conduct
Apache-2.0 license
Component toolkit for live running code editing experiences

Sandpack
Sandpack is a component toolkit for creating your own live running code editing experience powered by CodeSandbox.

Learn more about Sandpack

Edit in CodeSandbox

Sandpack Client
This is a small foundation package that sits on top of the bundler. It is framework agnostic and facilitates the handshake between your context and the bundler iframe.

Read more

Sandpack React
React components that give you the power of editable sandboxes that run in the browser.

import { Sandpack } from "@codesandbox/sandpack-react";

<Sandpack template="react" />;
Read more

Sandpack Themes
A list of themes to customize your Sandpack components.

import { githubLight } from "@codesandbox/sandpack-themes";

<Sandpack theme={githubLight} />;
Read more

About
A component toolkit for creating live-running code editing experiences, using the power of CodeSandbox.
Sandpack React
React components that give you the power of editable sandboxes that run in the browser.

import { Sandpack } from "@codesandbox/sandpack-react";

<Sandpack template="react" />;
Read more

Sandpack Themes
A list of themes to customize your Sandpack components.

import { githubLight } from "@codesandbox/sandpack-themes";

<Sandpack theme={githubLight} />;
Read more

About
A component toolkit for creating live-running code editing experiences, using the power of CodeSandbox.
codesandbox Sandpack Client
This is a small foundation package that sits on top of the bundler. It is framework agnostic and facilitates the handshake between your context and the bundler iframe.

Read more

Sandpack React
React components that give you the power of editable sandboxes that run in the browser.

import { Sandpack } from "@codesandbox/sandpack-react";

<Sandpack template="react" />;
Read more

Sandpack Themes
A list of themes to customize your Sandpack components.

import { githubLight } from "@codesandbox/sandpack-themes";

<Sandpack theme={githubLight} />;
 is a browser-based platform where you can effortlessly create and share apps without installation or setup. takes you from idea to app as fast as possible.The platform provides all the tools you must create amazing applications from one browser tab—no installation required.** includes AI coding tools, real-time collaboration, and project sharing to give you a head start on your app creation journey.**an AI-powered platform that lets you create and deploy apps from a single browser tab. The platform eliminates the complexity of traditional app-creation environments by combining coding, deployment, and collaboration tools in a single interface.
An instantly ready, full-featured online IDE for web development on any device with a browser. Enabling you to start new projects quickly and prototype rapidly. With CodeSandbox, you can create web apps, experiment with code, test ideas, and share creations easily.

Other CodeSandbox repositories
CodeSandbox consists of several separate servers, some of which are open sourced.

Client: the web application
Server: the Phoenix API server
Nginx: Nginx config files
Git Extractor: responsible for extracting the source from a GitHub repository
CLI: the CLI to upload a CodeSandbox project from your command line**codesandbox-cli
Upload your templates to codesandbox with a single command 🏖️

Build Status

This is the command line interface for CodeSandbox, an online editor tailored for web applications.

Quickstart
You can install the cli by running

# Install the cli
npm i -g codesandbox

# Go to your project
cd <path of your project>

# Deploy your project to CodeSandbox
codesandbox ./
Future features
Create a live connection with CodeSandbox using websockets so you can use your local editor
Current limitations
You need to be signed in to deploy, this is to prevent abuse
Inspiration
I took a lot of inspiration from now-cli and preact-cli while building this.

Readme
Keywords
codesandboxclieditorLikhonAI
AI-powered Web3 development toolkit for building scalable, secure, and intelligent decentralized applications.**https://raw.githubusercontent.com/LikhonAI/likhonai.github.io/refs/heads/main/instractions.mdx****
Typically, you must install programs, languages, and packages to build apps**you can rely on AI to configure your environment so you can start building without coding experience.
Components

Avatar
Badge
Book
Button
Calendar
Checkbox
Choicebox
Code Block
Collapse
Combobox
Command Menu
Context Card
Context Menu
Description
Drawer
Empty State
Entity
Error
Feedback
Gauge
Grid
Input
Keyboard Input
Loading Dots
Material
Menu
Modal
Note
Pagination
Pill
Progress
Project Banner
Radio
Relative Time Card
Scroller
Select
Show more
Skeleton
Slider
Snippet
Spinner
Split Button
Stack
Status Dot
Switch
Table
Tabs
Text
Textarea
Theme Switcher
Toast
Toggle
TooltipComponents


Several Sandpack prefixed components are available in the sandpack-react package. They can be used to build custom presets, as long as they render within the providers we talked about during the previous section.

Let's try to rebuild the Sandpack preset, using the sandpack components available in the sandpack-react package.

Layout
The first component inside the Provider is SandpackLayout. This component ensures the theming is applied and gives your sandpack instance the two column layout with the first child on the left and the second one on the right.

SandpackLayout gives you the left-right split between two components and also breaks the columns when the component is under 700px wide, so you have some responsiveness built-in. It also renders the theme provider for convenience.

Editable example

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
import {
  SandpackProvider,
  SandpackLayout,
  SandpackCodeEditor,
  SandpackPreview,
} from "@codesandbox/sandpack-react";

export default () => (
  <SandpackProvider template="react">
    <SandpackLayout>
      <SandpackCodeEditor />
      <SandpackPreview />
    </SandpackLayout>
  </SandpackProvider>
);

Preview




Further now we have pretty much the same component as the preset, minus the prop passing, which you can decide based on your specific needs.

You can easily swap the two components inside the SandpackLayout to get a different instance of Sandpack.

Editable example

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
import {
  SandpackProvider,
  SandpackLayout,
  SandpackCodeEditor,
  SandpackPreview,
} from "@codesandbox/sandpack-react";

export default () => (
  <SandpackProvider template="react">
    <SandpackLayout>
      <SandpackPreview />
      <SandpackCodeEditor />
    </SandpackLayout>
  </SandpackProvider>
);

Preview




SandpackProvider accepts a theme prop, so you can pass in your custom theme object or a predefined theme.

Preview
The Preview component is running the sandpack bundler, so without rendering a Preview component you will not have any bundling and evaluation of the code in sandpack. However, the Preview is smart enough to start even if it is mounted later in the page. This is how the autorun=false mode is working.

<SandpackProvider template="react">
  <SandpackLayout>
    <SandpackPreview />
  </SandpackLayout>
</SandpackProvider>
There's nothing stopping you from rendering multiple previews in the same Provider. They will all be connected to the same state source, but they can for example point to different pages of the same application.

Editable example

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
import {
  SandpackProvider,
  SandpackLayout,
  SandpackPreview,
} from "@codesandbox/sandpack-react";

export default () => (
  <SandpackProvider template="react">
    <SandpackLayout>
      <SandpackPreview />
      <SandpackPreview />
      <SandpackPreview />
      <SandpackPreview />
    </SandpackLayout>
  </SandpackProvider>
);

Preview




Options
Additional buttons
The <SandpackPreview /> component also allows you to add additional buttons to the preview area.

Editable example

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
import {
  SandpackProvider,
  SandpackLayout,
  SandpackCodeEditor,
  SandpackPreview,
} from "@codesandbox/sandpack-react";

export default () => (
  <SandpackProvider template="react">
    <SandpackLayout>
      <SandpackPreview
        actionsChildren={
          <button onClick={() => window.alert("Bug reported!")}>
            Report bug
          </button>
        }
      />
      <SandpackCodeEditor />
    </SandpackLayout>
  </SandpackProvider>
);

Preview




Additional content
For advanced use cases, children of <SandpackPreview> are rendered at the end of the preview container.

Getting the client instance from SandpackPreview
You can imperatively retrieve the Sandpack client from a SandpackPreview ref, and also consume or interact with the current state of the preview. Check out the type definitions for more details.

import { SandpackPreviewRef, useSandpack, SandpackPreview } from "@codesandbox/sandpack-react"
 
const SandpackPreviewClient: React.FC = () => {
  const { sandpack } = useSandpack();
  const previewRef = React.useRef<SandpackPreviewRef>();
 
  React.useEffect(() => {
    const client = previewRef.current?.getClient();
    const clientId = previewRef.current?.clientId;
 
    if (client && clientId) {
      console.log(client);
      console.log(sandpack.clients[clientId]);
    }
  /**
   * NOTE: In order to make sure that the client will be available
   * use the whole `sandpack` object as a dependency.
   */
  }, [sandpack]);
 
  return <SandpackPreview ref={previewRef} />;
};
Worth mentioning that the SandpackClient will not be instantly available. Sandpack has its own rules to decide when it'is the "right" moment to initialize an instance from a preview component. (Sandpack will take into account properties such as autorun, initMode, and the current client stack priority) This means that it's expected that getClient function returns undefined which is a valid state.

Code editor
The SandpackCodeEditor component renders a wrapper over codemirror, a lightweight code editor we use inside sandpack. If you played with the Sandpack preset, you should be familiar already with the props that you can pass to the code editor component:

Editable example

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
import {
  SandpackProvider,
  SandpackLayout,
  SandpackPreview,
  SandpackCodeEditor,
} from "@codesandbox/sandpack-react";

export default () => (
  <SandpackProvider template="react">
    <SandpackLayout>
      <SandpackCodeEditor
        showTabs
        showLineNumbers={false}
        showInlineErrors
        wrapContent
        closableTabs
      />
      <SandpackPreview />
    </SandpackLayout>
  </SandpackProvider>
);

Preview




Options
Extensions
Sandpack uses CodeMirror under the hood to provide a nice editor. You can extend the editor with any CodeMirror extensions, such as @codemirror/autocomplete.

Editable example

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
import { 
  Sandpack, 
  SandpackProvider, 
  SandpackLayout, 
  SandpackCodeEditor 
} from "@codesandbox/sandpack-react";
import { autocompletion, completionKeymap } from "@codemirror/autocomplete";

export default () => (
  <SandpackProvider template="react">
    <SandpackLayout>
      <SandpackCodeEditor
        extensions={[autocompletion()]}
        extensionsKeymap={[completionKeymap]}
      />
    </SandpackLayout> 
  </SandpackProvider>
);
Preview




Additional languages
Sandpack provides built-in support for a variety of common languages:

JavaScript, JSX
TypeScript, TSX
CSS, SCSS, Less
HTML
Vue
When an appropriate language can't be detected JavaScript is used.

If you want to support additional languages you can extend the editor by supplying a CodeMirror language and associating it with one or more file extensions.

import { python } from "@codemirror/lang-python";
 
<SandpackProvider>
  <SandpackCodeEditor
    additionalLanguages={[
      {
        name: "python",
        extensions: ["py"],
        language: python(),
      },
    ]}
  />
</SandpackProvider>
 
<Sandpack
  options={{
    codeEditor: {
      additionalLanguages: [
        {
          name: "python",
          extensions: ["py"],
          language: python(),
        },
      ]
    },
  }}
  template="react"

When using a stream language mode you'll need to convert it into a LanguageSupport instance.

import { LanguageSupport, StreamLanguage } from "@codemirror/language";
import { shell } from "@codemirror/legacy-modes/mode/shell";
 
<SandpackProvider>
  <SandpackCodeEditor
    additionalLanguages={[
      {
        name: "shell",
        extensions: ["sh", "bat", "ps1"],
        language: new LanguageSupport(StreamLanguage.define(shell)),
      },
    ]}
  />
</SandpackProvider>;
Advanced usage
If you want to interact directly with CodeMirror, use the component ref to access the getCodemirror function, which will return the CodeMirror instance. Check out how to use it:

import { EditorSelection } from "@codemirror/state";
 
const App = () => {
  const codemirrorInstance = useRef();
 
  useEffect(() => {
    // Getting CodeMirror instance
    const cmInstance = codemirrorInstance.current.getCodemirror();
 
    if (!cmInstance) return;
 
    // Current position
    const currentPosition = cmInstance.state.selection.ranges[0].to;
 
    // Setting a new position
    const trans = cmInstance.state.update({
      selection: EditorSelection.cursor(currentPosition + 1),
      changes: {
        from: 0,
        to: cmInstance.state.doc.length,
        insert: code,
      },
    });
 
    cmInstance.update([trans]);
  }, []);
 
  return (
    <SandpackProvider template="react">
      <SandpackCodeEditor ref={codemirrorInstance} />
    </SandpackProvider>
  );
};
This is especially useful to get the cursor's current position, add custom decorators, set the selection in a specific position, etc.

File Explorer
The SandpackFileExplorer provides a minimal but very powerful experience to navigate through files. You can open and close folders, and open new files.

Editable example

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
import { 
  SandpackProvider, 
  SandpackLayout, 
  SandpackCodeEditor, 
  SandpackFileExplorer 
} from "@codesandbox/sandpack-react";

export default () => (
  <SandpackProvider template="react">
    <SandpackLayout>
      <SandpackFileExplorer />
      <SandpackCodeEditor />
    </SandpackLayout>
  </SandpackProvider>
);

Preview




Options
If you're looking for extra feature we recommend using AaronPowell96/sandpack-file-explorer package which support things such as:

Add and remove files or directories,
Drag and drop to move files or directories,
Allow users to customise the entire folder structure right within your website!
Works out of the box with all of Sandpack's templates.
Tests
The SandpackTests component renders a thin wrapper around Jest to run tests directly in the browser. This means you can run tests but additional configuration may not possible given the browser environment.

Any test files ending with .test.js(x), .spec.js(x), .test.ts(x) and .spec.ts(x) will automatically be run with Jest and the results shown in the SandpackTests component.

Usage
There are two ways to run tests and check out the output:

Sandpack Preset
Using test-ts template preset, which contains an example test.

Editable example

1
2
3
4
import { Sandpack } from "@codesandbox/sandpack-react";

export default () => <Sandpack template="test-ts" />;

Preview




SandpackTests component
Standalone and configurable component to run tests, which you can combine with test-ts template or supply custom files. For more details about its usage and implementation, check out the API reference.

Editable example

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
import { 
  SandpackProvider, 
  SandpackLayout, 
  SandpackCodeEditor, 
  SandpackTests 
} from "@codesandbox/sandpack-react";

export default () => (
  <SandpackProvider template="test-ts">
    <SandpackLayout>
      <SandpackTests />
      <SandpackCodeEditor />
    </SandpackLayout>
  </SandpackProvider>
);

Preview




Options
Extending expect
Although not all configuration is supported, extending expect with custom / third party matchers is still possible.

Add the matchers either as a dependency or as a file and then import the matchers into your tests and invoke expect.extend with your matchers.

Editable example

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
import { 
  SandpackProvider, 
  SandpackLayout, 
  SandpackCodeEditor, 
  SandpackTests 
} from "@codesandbox/sandpack-react";

const extendedTest = `import * as matchers from 'jest-extended';
import { add } from './add';

expect.extend(matchers);

describe('jest-extended matchers are supported', () => {
test('adding two positive integers yields a positive integer', () => {
expect(add(1, 2)).toBePositive();
});
});
`;

export default () => (
  <SandpackProvider
    customSetup={{ dependencies: { "jest-extended": "^3.0.2" } }}
    files={{ "/extended.test.ts": extendedTest }}
    template="test-ts"
  >
    <SandpackLayout>
      <SandpackCodeEditor />
      <SandpackTests />
    </SandpackLayout>
  </SandpackProvider>
);

Preview




Hiding Tests
You can hide the test files using the visibleFiles prop. Additionally, if you want to suppress test content and only show the test results, you can use the hideTestsAndSuppressLogs option. This option will hide the test files, suppress the console logs, and disable the verbose button.

Editable example

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23

import {
  SandpackProvider,
  SandpackLayout,
  SandpackCodeEditor,
  SandpackTests,
} from "@codesandbox/sandpack-react";

export default () => (
  <SandpackProvider
    template="test-ts"
    options={{
      activeFile: "/add.ts",
      visibleFiles: ["/add.ts"],
    }}
  >
    <SandpackLayout>
      <SandpackCodeEditor />
      <SandpackTests hideTestsAndSupressLogs />
    </SandpackLayout>
  </SandpackProvider>
);

Preview




Console
SandpackConsole is a Sandpack devtool that allows printing the console logs from a Sandpack client. It is designed to be a light version of a browser console, which means that it's limited to a set of common use cases you may encounter when coding.

Sandpack runs the console directly into the iframe. As a result, all console messages pass through the Sandpack protocol, where you can attach a listener to these messages in your own component or use the proper Sandpack React hook to consume them.

Usage
There are three ways to print the logs:

<Sandpack options={{ showConsole: true }} />: shows a panel right after the SandpackPreview;
<SandpackConsole />: standalone component to render the logs;
useSandpackConsole: React hook to consume the console logs from a Sandpack client;
Editable example

1
2
3
4
5
6
7
8
9
10
11
import { Sandpack } from "@codesandbox/sandpack-react";

export default () => (
  <Sandpack
    options={{
      showConsole: true,
      showConsoleButton: true,
    }}
  />
);

Preview




SandpackConsole Options
Prop	Description	Type	Default
clientId		string	undefined
showHeader		boolean	true
showSyntaxError		boolean	false
showResetConsoleButton		boolean	true
showRestartButton		boolean	true
maxMessageCount		number	800
onLogsChange		(logs: SandpackConsoleData) => void	
resetOnPreviewRestart	Reset the console list on every preview restart	boolean	false
ref	Make possible to imperatively interact with the console component	SandpackConsoleRef	SandpackConsoleRef
standalone	It runs its sandpack-client, meaning it doesn't depend on a SandpackPreview component.	boolean	false
actionsChildren		JSX.Element	null
Limitation
Considering that SandpackConsole is meant to be a light version of a browser console, there are a few limitations in its implementation in order to keep it modular and light:

It needs to have a Sandpack client running (iframe) to execute the logs.
It only supports four types of consoles: info, warning, error, and clear.
It doesn't render nested objects due to recursive issues.
However, if you need to support more advanced cases, useSandpackConsole hook is compatible with console-feed, which provides a closer browser-console experience without any of the limitations mentioned above.

Code Viewer
For situations when you strictly want to show some code and run it in the browser, you can use the SandpackCodeViewer component. It looks similar to the code editor, but it renders a read-only version of codemirror, so users will not be able to edit the code.

Editable example

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
import {
  SandpackProvider,
  SandpackLayout,
  SandpackCodeEditor,
  SandpackCodeViewer,
  SandpackPreview,
} from "@codesandbox/sandpack-react";

export default () => (
  <SandpackProvider template="react">
    <SandpackLayout>
      <SandpackCodeViewer />
      <SandpackPreview />
    </SandpackLayout>
  </SandpackProvider>
);

Preview




Options
CodeMirror decorations
This API provides a way to draw or style a piece of code in the editor content. You can implement it in the following ways:

Entire line: add className or elements attributes to an entire line;
Range: add className or elements attributes to a piece of content, given a line, startColumn and endColumn;
data.js
index.css
App.js
export default [
  { className: "highlight", line: 1 },
  { className: "highlight", line: 9 },
  {
    className: "widget",
    elementAttributes: { "data-id": "1" },
    line: 12,
    startColumn: 26,
    endColumn: 38,
  },
  {
    className: "widget",
    elementAttributes: { "data-id": "2" },
    line: 13,
    startColumn: 8,
    endColumn: 17,
  },
];


Open Sandbox
OpenInCodeSandboxButton
You can build a custom button that creates a new sandbox from the sandpack files. It will include any edits made in the Sandpack editor, so it is a great way to persist your changes. The created sandbox will open on CodeSandbox in a new tab.

Let's use the UnstyledOpenInCodeSandboxButton as an example:

Editable example

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
import {
  SandpackProvider,
  SandpackLayout,
  SandpackCodeEditor,
  UnstyledOpenInCodeSandboxButton,
} from "@codesandbox/sandpack-react";

export default () => (
  <SandpackProvider template="react">
    <SandpackLayout>
      <SandpackCodeEditor />
    </SandpackLayout>
    
    <UnstyledOpenInCodeSandboxButton>
      Open in CodeSandbox
    </UnstyledOpenInCodeSandboxButton>
  </SandpackProvider>
);

Preview




The UnstyledOpenInCodeSandboxButton is a basic component that does not carry any styles. If you want a ready-to-use component, use the OpenInCodeSandboxButton instead, which has the same functionality but includes the CodeSandbox logo.

Other components
You can also bring other components in the mix: SandpackTranspiledCode, FileTabs, SandpackFileExplorer, Navigator and so on.

For example, you can create an editor instance that gives you the transpiled code of your active component instead of the preview page:

Editable example

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
import {
  SandpackProvider,
  SandpackLayout,
  SandpackCodeEditor,
  SandpackTranspiledCode,
} from "@codesandbox/sandpack-react";

export default () => (
  <SandpackProvider template="react">
    <SandpackLayout>
      <SandpackCodeEditor />
      <SandpackTranspiledCode />
    </SandpackLayout>
  </SandpackProvider>
)

Preview




You will notice that the theming applies to all components in the same way, as the theme object is also distributed by the theme context.

Some of the components have configuration props that toggle subparts on/off or that configure behavior/look. All of them comunicate with sandpack through the shared context.

Congrats!


You can now easily crea
The platform supports full-featured development and coding environments for those familiar with coding, so there’s no limit on what’s possible.**provides the following essential app creation tools:
var(--ds-background-100)  var(--ds-background-100) 
Real-time preview of your app
Deploy in minutes
Browser native app that requires zero installation and configuration
Full-featured code editor
Mobile app for building apps from your phone or tablet
AI-assisted app creation
Version control integration for tracking changes
Collaborative building over the network************
Collaborative building over the network************
Collaborative building over the network*** AI Agent and Assistant accelerate app creation with the following capabilities:
Deploy your apps in minutes using the following tools:

App deployment to the cloud in a few clicks
Database integration and hosting
Custom domain support and connection encryption for your applications
Complete app generation and setup from natural language descriptions
Code suggestions and autocomplete
Automated error detection and debugging assistance
Documentation generation for your app*********
