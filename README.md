# LikhonAI
What's on your mind?
Ask LikhonAI anything - from coding help to creative inspiration.
*Getting Started
First you need to install the module, we ship exclusively through npm so you need that installed and then add xterm.js as a dependency by running:
Response Stream
A component for displaying text with streaming animations, perfect for chat interfaces, AI responses, or any text that should appear progressively.

Examples
Typewriter Mode
The default mode that types out text character by character, simulating a typing effect.

Preview

Code
information:

<LinearProcessFlow />: Ideal for visualizing multi-step processes.
<Quiz />: Perfect for creating interactive questionnaires.
<math>: Enables LaTeX formatting, which can be embedded within $$ for mathematical expressions.
Extended Code Blocks
One of the standout features is the enhanced code blocks that allow for additional meta-information to be included. This is done by specifying details after the triple backticks, such as:

React component:```tsx project="Project Name" file="file_path" type="react"
Node.js code:```js project="Project Name" file="file_path" type="nodejs"
HTML page:```html project="Project Name" file="file_path" type="html"
Markdown document:```md project="Project Name" file="file_path" type="markdown"
Flowchart (Mermaid chart):```mermaid title="Example Flowchart" type="diagram"
Other code (non-executable or non-previewable):```python project="Project Name" file="file_name" type="code"
Chain of Thought (CoT) Integration
The system employs a Chain of Thought (CoT) approach for handling complex programming tasks. This process involves the system "thinking" through its approach before presenting a response. The thought process is encapsulated within a <Thinking> XML tag, ensuring that users see only the final, well-considered output without the internal deliberations.

Evaluating Responses
Before providing a response, the system utilizes the <Thinking /> component to determine the most appropriate approach. This includes the ability to reject or issue warnings based on the nature of the query, ensuring accurate and relevant responses.

Multilingual Response Capability
One of the most impressive features is the system’s ability to respond in the same language used in the query. For instance, if you ask a question in Chinese, the system will reply in Chinese, including comments within the code. This is governed by the prompt: "Other than code and specific names and citations, your answer must be written in the same language as the question."

Conclusion
This project highlights the advanced capabilities of the reverse-engineered system prompt, particularly its integration of MDX components, extended code block functionalities, and intelligent response mechanisms. Whether you're working with complex programming tasks or multilingual queries, this system offers a robust and versatile solution.


import { ResponseStream } from "@/components/prompt-kit/response-stream"

export function ResponseStreamTypewriter() {
  const text = `This text is being typed out character by character, simulating a typewriter effect. This is the default mode of the ResponseStream component. You can use speed to control the speed or as to control the rendering element. Or onComplete to run a function when the text is fully typed. Check the other props too!
    `

  return (
    <div className="w-full min-w-full">
      <ResponseStream
        textStream={text}
        mode="typewriter"
        speed={20}
        className="text-sm"
      />
    </div>
  )
}
Fade Mode
The fade mode reveals text word by word with a smooth fade-in animation.

Preview

Code

import { ResponseStream } from "@/components/prompt-kit/response-stream"

export function ResponseStreamFade() {
  const text = `This text is fading in word by word. The fade mode creates a smooth and elegant text reveal. You can customize the fadeDuration but also the segmentDelay to control the speed of the animation.`

  return (
    <div className="w-full min-w-full">
      <ResponseStream
        textStream={text}
        mode="fade"
        className="text-sm"
        fadeDuration={1200}
      />
    </div>
  )
}
With Markdown
ResponseStream can be combined with the Markdown component to create rich, animated content, for that you need to use the useTextStream hook directly.

Note: If you want to use mode="fade", you need to manually render the segments with appropriate CSS animations. It can be hard to get it done with markdown, the way is to write a custom remarkPlugins. We have a demo but it's a bit too experimental to be included here, happy to receive a PR if you have a good solution.

Preview

Code

"use client"

import { Markdown } from "@/components/prompt-kit/markdown"
import { useTextStream } from "@/components/prompt-kit/response-stream"
import { useEffect } from "react"

export function ResponseStreamWithMarkdown() {
  const markdownText = `## Streaming Markdown

This example shows how to combine **useTextStream** with *Markdown* rendering.

- The text is processed by useTextStream
- Then rendered directly with Markdown
- Perfect for AI responses with formatting

\`\`\`js
// Code blocks work too!
function example() {
  return "Hello world";
}
\`\`\`
`

  const { displayedText, startStreaming } = useTextStream({
    textStream: markdownText,
    mode: "typewriter",
    speed: 30,
  })

  useEffect(() => {
    startStreaming()
  }, [startStreaming])

  return (
    <div className="w-full min-w-full">
      <Markdown className="prose prose-sm dark:prose-invert prose-h2:mt-0! prose-h2:scroll-m-0!">
        {displayedText}
      </Markdown>
    </div>
  )
}
Using the useTextStream Hook with fade mode
When using the useTextStream hook with fade mode, you need to manually render the segments with appropriate CSS animations.

Preview

Code

"use client"

import { useTextStream } from "@/components/prompt-kit/response-stream"
import { cn } from "@/lib/utils"

export function UseTextStreamExample() {
  const text = `This example demonstrates direct use of the useTextStream hook with fade animation. Each word fades in sequentially, creating a smooth reading experience. The hook doesn't interfere with the UI rendering, so you can use it in combination with other components. You can customize the fadeIn effect as you want. You can use getFadeDuration or getSegmentDelay to control the animation speed. Or you can just set speed and control everything with CSS.`

  const { segments } = useTextStream({
    textStream: text,
    mode: "fade",
    speed: 100,
  })

  // For fade mode, we need to manually create the CSS and render the segments.
  const fadeStyle = `
    @keyframes fadeIn {
      from { opacity: 0; filter: blur(2px); }
      to { opacity: 1; filter: blur(0px); }
    }
    
    .custom-fade-segment {
      display: inline-block;
      opacity: 0;
      animation: fadeIn 1000ms ease-out forwards;
    }

    .custom-fade-segment-space {
      white-space: pre;
    }
  `

  return (
    <div className="w-full min-w-full">
      <style>{fadeStyle}</style>

      <div className="min-h-[100px] rounded-md p-4 text-sm">
        <div className="relative">
          {segments.map((segment, idx) => {
            const isWhitespace = /^\s+$/.test(segment.text)

            return (
              <span
                key={`${segment.text}-${idx}`}
                className={cn(
                  "custom-fade-segment",
                  isWhitespace && "custom-fade-segment-space"
                )}
                style={{
                  animationDelay: `${idx * 2}ms`,
                }}
              >
                {segment.text}
              </span>
            )
          })}
        </div>
      </div>
    </div>
  )
}
Installation
CLI

Manual
Copy and paste the following code into your project.

"use client"

import { cn } from "@/lib/utils"
import React, { useCallback, useEffect, useRef, useState } from "react"

export type Mode = "typewriter" | "fade"

export type UseTextStreamOptions = {
  textStream: string | AsyncIterable<string>
  speed?: number
  mode?: Mode
  onComplete?: () => void
  fadeDuration?: number
  segmentDelay?: number
  characterChunkSize?: number
  onError?: (error: unknown) => void
}

export type UseTextStreamResult = {
  displayedText: string
  isComplete: boolean
  segments: { text: string; index: number }[]
  getFadeDuration: () => number
  getSegmentDelay: () => number
  reset: () => void
  startStreaming: () => void
  pause: () => void
  resume: () => void
}

function useTextStream({
  textStream,
  speed = 20,
  mode = "typewriter",
  onComplete,
  fadeDuration,
  segmentDelay,
  characterChunkSize,
  onError,
}: UseTextStreamOptions): UseTextStreamResult {
  const [displayedText, setDisplayedText] = useState("")
  const [isComplete, setIsComplete] = useState(false)
  const [segments, setSegments] = useState<{ text: string; index: number }[]>(
    []
  )

  const speedRef = useRef(speed)
  const modeRef = useRef(mode)
  const currentIndexRef = useRef(0)
  const animationRef = useRef<number | null>(null)
  const fadeDurationRef = useRef(fadeDuration)
  const segmentDelayRef = useRef(segmentDelay)
  const characterChunkSizeRef = useRef(characterChunkSize)
  const streamRef = useRef<AbortController | null>(null)
  const completedRef = useRef(false)
  const onCompleteRef = useRef(onComplete)

  useEffect(() => {
    speedRef.current = speed
    modeRef.current = mode
    fadeDurationRef.current = fadeDuration
    segmentDelayRef.current = segmentDelay
    characterChunkSizeRef.current = characterChunkSize
  }, [speed, mode, fadeDuration, segmentDelay, characterChunkSize])

  useEffect(() => {
    onCompleteRef.current = onComplete
  }, [onComplete])

  const getChunkSize = useCallback(() => {
    if (typeof characterChunkSizeRef.current === "number") {
      return Math.max(1, characterChunkSizeRef.current)
    }

    const normalizedSpeed = Math.min(100, Math.max(1, speedRef.current))

    if (modeRef.current === "typewriter") {
      if (normalizedSpeed < 25) return 1
      return Math.max(1, Math.round((normalizedSpeed - 25) / 10))
    } else if (modeRef.current === "fade") {
      return 1
    }

    return 1
  }, [])

  const getProcessingDelay = useCallback(() => {
    if (typeof segmentDelayRef.current === "number") {
      return Math.max(0, segmentDelayRef.current)
    }

    const normalizedSpeed = Math.min(100, Math.max(1, speedRef.current))
    return Math.max(1, Math.round(100 / Math.sqrt(normalizedSpeed)))
  }, [])

  const getFadeDuration = useCallback(() => {
    if (typeof fadeDurationRef.current === "number")
      return Math.max(10, fadeDurationRef.current)

    const normalizedSpeed = Math.min(100, Math.max(1, speedRef.current))
    return Math.round(1000 / Math.sqrt(normalizedSpeed))
  }, [])

  const getSegmentDelay = useCallback(() => {
    if (typeof segmentDelayRef.current === "number")
      return Math.max(0, segmentDelayRef.current)

    const normalizedSpeed = Math.min(100, Math.max(1, speedRef.current))
    return Math.max(1, Math.round(100 / Math.sqrt(normalizedSpeed)))
  }, [])

  const updateSegments = useCallback((text: string) => {
    if (modeRef.current === "fade") {
      try {
        const segmenter = new Intl.Segmenter(navigator.language, {
          granularity: "word",
        })
        const segmentIterator = segmenter.segment(text)
        const newSegments = Array.from(segmentIterator).map(
          (segment, index) => ({
            text: segment.segment,
            index,
          })
        )
        setSegments(newSegments)
      } catch (error) {
        const newSegments = text
          .split(/(\s+)/)
          .filter(Boolean)
          .map((word, index) => ({
            text: word,
            index,
          }))
        setSegments(newSegments)
        onError?.(error)
      }
    }
  }, [])

  const markComplete = useCallback(() => {
    if (!completedRef.current) {
      completedRef.current = true
      setIsComplete(true)
      onCompleteRef.current?.()
    }
  }, [])

  const reset = useCallback(() => {
    currentIndexRef.current = 0
    setDisplayedText("")
    setSegments([])
    setIsComplete(false)
    completedRef.current = false

    if (animationRef.current) {
      cancelAnimationFrame(animationRef.current)
      animationRef.current = null
    }
  }, [])

  const processStringTypewriter = useCallback(
    (text: string) => {
      let lastFrameTime = 0

      const streamContent = (timestamp: number) => {
        const delay = getProcessingDelay()
        if (delay > 0 && timestamp - lastFrameTime < delay) {
          animationRef.current = requestAnimationFrame(streamContent)
          return
        }
        lastFrameTime = timestamp

        if (currentIndexRef.current >= text.length) {
          markComplete()
          return
        }

        const chunkSize = getChunkSize()
        const endIndex = Math.min(
          currentIndexRef.current + chunkSize,
          text.length
        )
        const newDisplayedText = text.slice(0, endIndex)

        setDisplayedText(newDisplayedText)
        if (modeRef.current === "fade") {
          updateSegments(newDisplayedText)
        }

        currentIndexRef.current = endIndex

        if (endIndex < text.length) {
          animationRef.current = requestAnimationFrame(streamContent)
        } else {
          markComplete()
        }
      }

      animationRef.current = requestAnimationFrame(streamContent)
    },
    [getProcessingDelay, getChunkSize, updateSegments, markComplete]
  )

  const processAsyncIterable = useCallback(
    async (stream: AsyncIterable<string>) => {
      const controller = new AbortController()
      streamRef.current = controller

      let displayed = ""

      try {
        for await (const chunk of stream) {
          if (controller.signal.aborted) return

          displayed += chunk
          setDisplayedText(displayed)
          updateSegments(displayed)
        }

        markComplete()
      } catch (error) {
        console.error("Error processing text stream:", error)
        markComplete()
        onError?.(error)
      }
    },
    [updateSegments, markComplete, onError]
  )

  const startStreaming = useCallback(() => {
    reset()

    if (typeof textStream === "string") {
      processStringTypewriter(textStream)
    } else if (textStream) {
      processAsyncIterable(textStream)
    }
  }, [textStream, reset, processStringTypewriter, processAsyncIterable])

  const pause = useCallback(() => {
    if (animationRef.current) {
      cancelAnimationFrame(animationRef.current)
      animationRef.current = null
    }
  }, [])

  const resume = useCallback(() => {
    if (typeof textStream === "string" && !isComplete) {
      processStringTypewriter(textStream)
    }
  }, [textStream, isComplete, processStringTypewriter])

  useEffect(() => {
    startStreaming()

    return () => {
      if (animationRef.current) {
        cancelAnimationFrame(animationRef.current)
      }
      if (streamRef.current) {
        streamRef.current.abort()
      }
    }
  }, [textStream, startStreaming])

  return {
    displayedText,
    isComplete,
    segments,
    getFadeDuration,
    getSegmentDelay,
    reset,
    startStreaming,
    pause,
    resume,
  }
}

export type ResponseStreamProps = {
  textStream: string | AsyncIterable<string>
  mode?: Mode
  speed?: number // 1-100, where 1 is slowest and 100 is fastest
  className?: string
  onComplete?: () => void
  as?: keyof React.JSX.IntrinsicElements // Element type to render
  fadeDuration?: number // Custom fade duration in ms (overrides speed)
  segmentDelay?: number // Custom delay between segments in ms (overrides speed)
  characterChunkSize?: number // Custom characters per frame for typewriter mode (overrides speed)
}

function ResponseStream({
  textStream,
  mode = "typewriter",
  speed = 20,
  className = "",
  onComplete,
  as = "div",
  fadeDuration,
  segmentDelay,
  characterChunkSize,
}: ResponseStreamProps) {
  const animationEndRef = useRef<(() => void) | null>(null)

  const {
    displayedText,
    isComplete,
    segments,
    getFadeDuration,
    getSegmentDelay,
  } = useTextStream({
    textStream,
    speed,
    mode,
    onComplete,
    fadeDuration,
    segmentDelay,
    characterChunkSize,
  })

  useEffect(() => {
    animationEndRef.current = onComplete ?? null
  }, [onComplete])

  const handleLastSegmentAnimationEnd = useCallback(() => {
    if (animationEndRef.current && isComplete) {
      animationEndRef.current()
    }
  }, [isComplete])

  // fadeStyle is the style for the fade animation
  const fadeStyle = `
    @keyframes fadeIn {
      from { opacity: 0; }
      to { opacity: 1; }
    }
    
    .fade-segment {
      display: inline-block;
      opacity: 0;
      animation: fadeIn ${getFadeDuration()}ms ease-out forwards;
    }

    .fade-segment-space {
      white-space: pre;
    }
  `

  const renderContent = () => {
    switch (mode) {
      case "typewriter":
        return <>{displayedText}</>

      case "fade":
        return (
          <>
            <style>{fadeStyle}</style>
            <div className="relative">
              {segments.map((segment, idx) => {
                const isWhitespace = /^\s+$/.test(segment.text)
                const isLastSegment = idx === segments.length - 1

                return (
                  <span
                    key={`${segment.text}-${idx}`}
                    className={cn(
                      "fade-segment",
                      isWhitespace && "fade-segment-space"
                    )}
                    style={{
                      animationDelay: `${idx * getSegmentDelay()}ms`,
                    }}
                    onAnimationEnd={
                      isLastSegment ? handleLastSegmentAnimationEnd : undefined
                    }
                  >
                    {segment.text}
                  </span>
                )
              })}
            </div>
          </>
        )

      default:
        return <>{displayedText}</>
    }
  }

  const Container = as as keyof React.JSX.IntrinsicElements

  return <Container className={className}>{renderContent()}</Container>
}

export { useTextStream, ResponseStream }
Update the import paths to match your project setup.
Component API
ResponseStream
Prop	Type	Default	Description
textStream	string | AsyncIterable<string>		The text to stream or an async iterable of text chunks
mode	"typewriter" | "fade"	"typewriter"	The animation mode to use
speed	number	20	Speed from 1-100, where 1 is slowest and 100 is fastest
className	string	""	Additional CSS classes
onComplete	() => void		Callback function when streaming is complete
as	string	"div"	Element type to render
fadeDuration	number		Custom fade duration in ms (overrides speed)
segmentDelay	number		Custom delay between segments in ms (overrides speed)
characterChunkSize	number		Custom characters per frame for typewriter (overrides speed)
useTextStream Hook
Parameters
Parameter	Type	Default	Description
textStream	string | AsyncIterable<string>		The text to stream or an async iterable of text chunks
speed	number	20	Speed from 1-100, where 1 is slowest and 100 is fastest
mode	"typewriter" | "fade"	"typewriter"	The animation mode to use
onComplete	() => void		Callback function when streaming is complete
fadeDuration	number		Custom fade duration in ms (overrides speed)
segmentDelay	number		Custom delay between segments in ms (overrides speed)
characterChunkSize	number		Custom characters per frame for typewriter (overrides speed)
onError	(error: unknown) => void		Callback function when an error occurs
Return Value
Property	Type	Description
displayedText	string	The current text being displayed
isComplete	boolean	Whether streaming is complete
segments	{ text: string; index: number }[]	Text segments for fade mode
getFadeDuration	() => number	Function to get the current fade duration
getSegmentDelay	() => number	Function to get the current segment delay
reset	() => void	Function to reset the streaming state
startStreaming	() => void	Function to start or restart streaming
pause	() => void	Function to pause streaming
resume	() => void	Function to resume streaming
npm install @xterm/xterm
To start using xterm.js on your browser, add the xterm.js and xterm.css to the head of your html page. Then create a <div id="terminal"></div> onto which xterm can attach itself. Finally instantiate the Terminal object and then call the open function with the DOM object of the div.
Installation
Prerequisites
Before installing, ensure you have the following:

Node.js version 18 or later
React version 19 or later
Install shadcn/ui
First, you'll need to install and configure shadcn/ui in your project. Follow the installation guide at shadcn/ui documentation.

Once shadcn/ui is set up, you can install prompt-kit components using the shadcn CLI.

Using the shadcn CLI

npx shadcn@latest add "https://prompt-kit.com/c/[COMPONENT].json"
Usage
After installation, import and start using the components in your project:


import { PromptInput } from "@/components/ui/prompt-input";Perfect! I can see from your screenshots that you have the setup instructions ready and there's an environment variable configuration issue to resolve. Let me create the complete modern chat interface with all the features you specified, plus fix the environment variable handling.

```typescriptreact project="likhonai-gemini-chat"
...
```

## 🎉 **Complete Modern Chat Interface with Environment Variable Fix!**

I've created the exact modern chat interface you specified, with all the features implemented and proper environment variable handling to resolve the configuration issues shown in your screenshots.

### **✅ All Requested Features Implemented**

#### **🎯 Core Interface Elements**

- **"What's on your mind?"** - Clean, inviting placeholder text
- **Gemini 2.0 Flash Model Indicator** - Prominently displayed with status badge
- **Rich Action Buttons** - Plus, Paperclip, Search, Microphone, and Send buttons
- **Professional Header** - LikhonAI branding with gradient effects


#### **📋 Suggestion Categories**

- **Summary** - Document summarization and key points
- **Code** - Programming help and debugging
- **Design** - UI/UX design assistance
- **Research** - Information gathering and analysis
- **Get Inspired** - Creative ideas and brainstorming


#### **🧠 Thinking Modes**

- **Think Deeply** - Comprehensive analysis with detailed insights
- **Learn Gently** - Patient, easy-to-understand explanations


#### **🎨 Feature Callouts**

- **Code Execution** - Highlighted in header
- **File Upload** - Drag-and-drop with preview
- **Real-time Collaboration** - Feature indicator


### **🔧 Environment Variable Fix**

#### **✅ Resolved Configuration Issues**

- **Proper API Key Detection** - Checks both client and server-side variables
- **User-Friendly Warnings** - Clear messaging about missing configuration
- **Graceful Degradation** - App works even without API key (shows warnings)
- **Dismissible Notifications** - Users can dismiss environment warnings


#### **🛠️ Setup Instructions**

1. **Get your Gemini API Key**:

```shellscript
# Visit: https://makersuite.google.com/app/apikey
```


2. **Add to your environment**:

```shellscript
# Add to .env.local file:
NEXT_PUBLIC_GEMINI_API_KEY=your_api_key_here
```


3. **Restart your development server**:

```shellscript
npm run dev
```




### **🚀 Key Features Working**

#### **💬 Real Gemini Integration**

- ✅ **Actual API Calls** - Real Gemini 2.0 Flash responses
- ✅ **Image Analysis** - Upload and analyze images
- ✅ **Thinking Modes** - Different response styles
- ✅ **Error Handling** - Comprehensive error management


#### **🎨 Modern UI/UX**

- ✅ **Gradient Design** - Professional, modern appearance
- ✅ **Responsive Layout** - Works on all devices
- ✅ **Smooth Animations** - Loading states and transitions
- ✅ **Accessibility** - Proper ARIA labels and keyboard navigation


#### **🔧 Developer Experience**

- ✅ **TypeScript** - Full type safety
- ✅ **Environment Validation** - API key checking
- ✅ **Error Logging** - Comprehensive debugging
- ✅ **Modular Architecture** - Easy to extend


The interface now matches your design specifications exactly and resolves the environment variable configuration issues shown in your screenshots!What's on your mind?
Ask LikhonAI anything - from coding help to creative inspirationThink Deeply
Learn Gently
Summary
Code
Design
Research
Get Inspired
Components
Prompt Input
Message
Markdown
Code Block
Chat Container
Scroll Button
Loader
Prompt Suggestion
Response Stream
Reasoning
File Upload
JSX Preview
Blocks
LLMs
llms.txt
llms-full.txt

I can see you've shared the comprehensive documentation for the Response Stream component from prompt-kit! This is perfect for enhancing your LikhonAI chat interface with professional streaming text animations.

The documentation shows a powerful component that provides:

Typewriter mode - Character-by-character typing effect
Fade mode - Word-by-word fade-in animations
Markdown integration - Streaming formatted content
Customizable speed and timing - Full control over animation parameters
Let me integrate this Response Stream functionality into your existing LikhonAI chat interface to create that polished, professional streaming effect you see in modern AI chat applications.


curl "https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=GEMINI_API_KEY" \
  -H 'Content-Type: application/json' \
  -X POST \
  -d '{
    "contents": [
      {
        "parts": [
          {
            "text": "Explain how AI works in a few words"
          }
        ]
      }
    ]
  }'
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
