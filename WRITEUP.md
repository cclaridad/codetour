# CSE P 590 B Final Project

This is the final project write-up for Professor Jen Mankoff's course, [<ins>CSE P 590 B: The Future of Access Technology</ins>](https://courses.cs.washington.edu/courses/csep590b/23wi/assignments/project.html).
<br/><br/>

## Group members

The group members of the project are the following people:

- Brian Rogers
- Chloe Claridad
- Johnny Ahmad
- Mary Giambrone
- Thierry Kimenyi

We also have one project sponsor, Venkatesh Potluri.
<br/><br/>

## Introduction

We evaluated the accessibility of the Visual Studio Code CodeTour extension for blind and low-vision (BLV) users. Based on our findings, we made prototype-quality changes to CodeTour to improve accessibility. Finally, we identified future work items that could make CodeTour and Visual Studio Code more accessible.
<br/><br/>

## Related Work

Visual Studio Code has many features that make it the editor of choice for many people. However, its [<ins>accessibility</ins>](https://code.visualstudio.com/docs/editor/accessibility) features, such as Zoom, high contrast themes, keyboard navigation, screen reader optimized mode, terminal accessibility, and audio cues, make it the editor of choice for most BLV programmers. [<ins>Accessibility in VS Code</ins>](https://www.youtube.com/watch?v=9biCDjSSwqw) shows how to use those features and how they help programmers with different disabilities.

In [<ins>vscode setup for accessibility</ins>](https://www.youtube.com/watch?v=uZCwXDK-QPc), Taylor Arndt shows how to set up Visual Studio Code with screen readers and explains why it is her editor of choice. The YouTube channel Coding Blind Tech titled [<ins>Why I use NVDA And VS Code To write code</ins>](https://www.youtube.com/watch?v=7hU5PFa6Zoc) where a blind user explains why they use and prefer NVDA and Visual Studio Code to write code instead of other applications. That channel also has a [<ins>tutorial</ins>](https://www.youtube.com/watch?v=UaSZ0BpscQs) on installing extensions using a screen reader.
<br/><br/>

## Methodology

Throughout the project, we worked with Venkatesh Potluri, our project sponsor and a BLV programmer. We learned a lot about the experience of using NVDA with VS Code to read and write code. We had regular meetings and discussions with Venkatesh to ensure that the enhancements and improvements we worked on would be helpful and usable by BLV programmers.

Before our first meeting with Venkatesh, our team had some initial ideas about areas of improvement in the CodeTour extension based on VS Code tutorials from BLV programmers that we watched. We didn’t have a specific list of feature ideas from BLV programmers, knowledge of the complexity of the work, or an understanding of the limitations of CodeTour or VS Code.

In that initial meeting with Venkatesh, he shared high-level ideas about improving the experience. These included parsing metadata to pass information to the screen reader, audio cues, keyboard shortcuts, and notifications. We also learned about his first-person experience writing code with a screen reader: using a combination of VS Code as an editor and the command line terminal.

This first-person account taught us about tools for onboarding to unfamiliar code without code tours. In addition to code comments written by other developers, Venkatesh used the F12 shortcut (go to definition) to better understand the context.
After this discussion, we decided to focus on code tour consumption instead of code tour creation. Existing bugs prevented any context from being associated with the code tour steps. A screen reader user trying to create a code tour already has the relevant context, which would be annoying but somewhat usable. But someone trying to consume a tour for the first time would be completely blocked from understanding the content.

We continued iterating on our workstreams based on Venkatesh’s feedback. We also pivoted strategies based on blockers we faced on the extension or VS Code side that would require much more time to overcome than we had for this final project. We made the CodeTour extension more accessible than previously by making code changes and bug fixes. The “How you made your app accessible?” section below details the changes and fixes we made.
<br/><br/>

## Disability Justice Perspective

Our project sponsor, Venkatesh, gave us a first-person disability perspective and informed much of our work. We specifically focused on the following disability justice principles.
<br/>

### Leadership of Most Impacted

We directly engaged with Venkatesh to gather feedback on the CodeTour experience for blind users. Based on his usability and accessibility feedback, we made changes and further improvements to our prototype. We are grateful for his valuable time and advice.
<br/>

### Recognizing Wholeness

We recognize that blind people are also programmers. We must ensure CodeTour functionality is accessible to these programmers, whether they use a mouse, keyboard, monitor, or screen reader.
<br/>

### Interdependence

CodeTour is an open-source project on GitHub. Open source allows groups like ours to collaborate directly in the developer community without corporate sponsors. We can make improvements to meet our needs and the needs of community members with disabilities.
<br/><br/>

## How We Made The App More Accessible

With the technical challenges we faced with Visual Studio Code, CodeTour, and the time constraints, we decided to scope our changes to consuming tours. All the changes we made do not break the current functionality, and we respect user preferences for opting out via the Visual Studio Code setting “accessibilitySupport”.

We added audio announcements when stepping through tours to make it easier for the user to know where they are within the tour. We improved the key bindings when stepping through the tour to make it easier to remember and to avoid conflicts with existing shortcuts.

In CodeTour, each step in a code tour is similar to a comment on a line of code, which makes it harder for BLV users to know which part of the file they are in (i.e whether they are inside a function, class, etc.) without extra context. We provided additional context to make it easier for the user to know the file, line number, and scope for each step.

We added the “Go to step” command with keyboard shortcuts.This allows a BLV used to easily go to a particular step in a tour. Other users can click on a particular step in the tree view section of CodeTour.

The original tour provided in the repo (that explains how to use the extension) was not accessible because it used a lot of emojis, links to commands that took too long to read, and lists that were inaccessible and created noise for the screen reader. We created an additional tour that is easier to consume for a BLV user. The modified tour does not have emojis and command links. It is split into more steps which creates a better flow for the user.

The initial codebase had obsolete packages that made it impossible to debug the code and test locally on Windows and MacOs operating systems. We updated all of those packages and fixed security vulnerabilities in the node modules that this extension relies on.
<br/><br/>

## Learnings and Future Work

As mentioned in the Methodology section above, we learned a lot from our first meeting with Venkatesh. This learning was important for deciding our starting workstreams. All follow-up meetings helped us refocus our efforts based on this user feedback.

In our follow-up meetings, we learned that Venkatesh prefers using hotkeys over the command palette. We also discussed some of the blockers related to audio cues, the VS Code API, and alternative approaches. Venkatesh also gave us feedback on how much context info about enclosing functions would be helpful.

Following our in-person demo meeting, we made several changes to the prototype. Previously, moving forward and backward when already at the beginning or end of the tour would end the tour. But Venkatesh explained that this was confusing. So, we changed the logic to stay on the current step and played an announcement instead.

In addition, we learned about some problems with switching between the different pane views in VS Code. Venkatesh also clarified which context was most helpful; line numbers and filenames weren’t meaningful without also knowing the function name that the code tour step was in. He also helped us troubleshoot some verbose Markdown NVDA output with the Comment VS Code API. Due to NVDA settings, we heard very different output for some comments. He also pointed out accessibility issues with “gutter decorations” (icons in the code editor that indicate where tour steps are). And finally, he walked us through how he would set up a code tour if he were authoring one.

In our final demo meeting with Venkatesh, he suggested that a “Go to step” command would be helpful and speed up keyboard-only navigation, so we added that to our prototype. He also gave feedback on the wording for the announcement text, so we updated that too.

To summarize, we made some improvements that were a direct result of Venkatesh’s perspective: info announcements, step navigation logic fixes and key binding improvements, step context (enclosing function name, filename, and line number), and the GoTo Step command.

And based on all this learning, there are several directions for future work. Several issues require fixes in the VS Code API, Comments API, and the Markdown package. Specifically, the VS Code API could allow extensions to register their own audio cues and define more accessible behavior for gutter decorations. The Comments implementation has several focus order issues, which should be addressed to enable better keyboard accessibility. The Comments view should also adjust how it passes information about the Markdown for VS Code Commands to the screen reader because the current output is prohibitively verbose.

Also, we currently only provide context for function names for tour steps in TypeScript files. Future work could generalize this logic to add support for all languages. The Visual Studio Code API does not provide an easy way to do this. One example of how this could be improved is this open issue: [<ins>Can I get scope / scopeRange at a position?</ins>](https://github.com/microsoft/vscode/issues/580). The [<ins>hscopes extension</ins>](https://github.com/draivin/hscopes/blob/58365d2969dbe0e55a5b469dd8c8c1b4dc1a0522/src/document.ts#L49) provides an API that can be used to get the scope at a particular position. Given more time, this would be an interesting direction for future work.
