# Claude, the Anthropic API, and the Context Window

You know Opus, Sonnet, and Haiku by name now. You understand that Opus handles the hardest problems, Sonnet balances speed and depth, and Haiku moves fast. But if you are a junior developer about to build your first feature with Claude, you will probably ask a practical question. "I get that the models are different, but how does my application actually reach them? And if I keep chatting back and forth, will the model eventually forget what I said at the start?"

Those two worries point to the same infrastructure. You need a reliable way to send requests from your code to Anthropic's servers. And you need to understand how much information the model can hold in its head while it answers you. The first piece is the Anthropic API. The second is the context window.

The Anthropic API is the interface through which Opus, Sonnet, and Haiku are accessed. Think of it as the post office between your application and the model. Your code does not run Claude on your laptop. The models live in Anthropic's data centers. When your app needs a response, it packages up a request and sends it to the API. The API delivers that package to the model you chose, waits for the reply, and brings it back. You can reach this same family of models through other channels, such as the Amazon Bedrock API or the Google Vertex AI API, but the direct Anthropic API is the main doorway. No matter which path you use, the pattern is identical. You pass in text, select a model, and receive a generated response.

That response is built from only what the model can see at that exact moment. Here is where the context window comes in. The context window is the amount of text a Claude model can consider in a single request. It is not long-term memory. It is not a hard drive. It is the live workspace the model reads right before it types its answer. Everything you want the model to know must fit inside this single space. That includes your current prompt, the entire conversation history, any system instructions you set, and any files you attach through the Files API. It also includes special setup documents like CLAUDE.md, which some Anthropic tools load into the start of every session automatically. All of it sits on the same desk, and the desk has a fixed size.

## The API is your line to the model

When you use the Anthropic API, you are making a remote call over the internet. This is different from the public chat interface on Anthropic's website. The website is for exploration. The API is for building. You choose which model family member you want. Opus for deep reasoning. Sonnet for everyday coding and analysis. Haiku for speed and low cost. You send a structured message that contains your text and your chosen model identifier. The API handles the routing, the security, and the response formatting. Because the API is the shared interface for the whole Claude family, switching from Haiku to Opus is usually just a matter of changing one name in your request. You do not rebuild your entire application.

This also means the API is where you manage the boundaries of your conversation. You decide what text goes in. You decide how much history to include. The API will faithfully carry whatever you give it, but it cannot make extra room if you send too much. It delivers the mail. It does not expand the mailbox.

## The context window is the model's desk

A useful way to picture the context window is a desk with a fixed surface. Every sheet of paper you add is part of the conversation. Your initial instructions are one sheet. The user's first question is another. Each reply from the model becomes a sheet too. Any uploaded documents are more sheets. The model can read every sheet that is currently on the desk. But if you keep adding pages, the oldest ones slide off the edge and disappear. The model does not know they ever existed.

This matters because it happens silently. Your application does not crash. The API still returns a perfect-looking answer. But that answer might ignore the first page of your instructions because it fell off the desk. If you load a long CLAUDE.md file at the start of a coding session, that file consumes desk space. If you then paste a huge error log, you might crowd out the very guidelines you wanted the model to follow. The window is large enough for serious work, but it is not infinite. The combined text of everything you send in one request must fit inside it. If you exceed the hard limit, you will usually get an error. If you approach the limit by piling on conversation history, the model simply loses sight of the oldest material.


<InlineQuiz
  id="quiz-s2-l3-context-window-limits"
  question="You are running a long conversation with Claude through the API. With each back-and-forth message, the conversation history grows larger. As the total text approaches the context window limit, what happens to the oldest messages?"
  options='["The API returns an error and refuses the request until you delete some history.","The oldest messages are silently dropped and the model no longer sees them.","The model automatically compresses older turns into a summary to save space.","The context window expands automatically to fit everything and your API cost increases."]'
  correct="1"
  explanation="The lesson describes the context window as a desk with a fixed surface. When you keep adding pages, the oldest ones slide off the edge and disappear silently. The API does not crash or warn you, and the model simply loses sight of the oldest material. Exceeding the hard limit in a single request can produce an error, which makes option A tempting, but gradually approaching the limit through conversation history is silent. The model does not auto-summarize old turns, so option C is wrong. The window size is fixed and never auto-expands, so option D is also wrong."
  courseSlug="claude-for-developers-beginner"
  lessonSlug="03-claude-the-anthropic-api-and-the-context-window"
/>

## Matching the model to the workspace

Choosing a model and managing the context window are two sides of the same coin. The API gives you access to all three tiers, but you still have to decide which tier fits your task and how much text you can afford to place on the desk.

Imagine you are building a legal assistant that analyzes contracts. The contracts are long and dense. You need Opus, because the reasoning is complex and the stakes are high. But a fifty-page contract plus your detailed questions eat a large share of the context window. You face a real trade-off. You can send the full text and risk pushing out your system instructions, or you can summarize the contract first and send only the summary with targeted excerpts. The model is smart enough to handle the depth, but the desk is only so big. You are constantly deciding what stays in view.

Now picture a customer support chatbot. Thousands of users want quick answers at all hours. Haiku is the right choice because it is fast and inexpensive through the API. Early in a conversation, the context window is roomy. But after twenty back-and-forth messages, the opening of the chat might fall off the desk. The bot could forget the user already provided their order number or email address. To prevent this, you have to actively manage history. You might summarize old turns and drop the raw text, or you might simply delete the oldest messages once the thread grows long. The trade-off here is not model capability. It is memory management versus API cost and response quality.

Finally, consider a coding tool that uses Sonnet to review pull requests. Your team maintains a CLAUDE.md file that explains naming conventions, architecture decisions, and testing rules. That file loads into context automatically at the start of every session. Then you paste three large files of code for review. The conventions file and the code files compete for the same limited space. If you send too many files, Sonnet might miss the style guide or overlook the first file you sent. The solution is to send only the files that changed, not the entire repository. You are budgeting space, and every line counts.

## A simple loop to keep in mind

When you build with Claude, you are managing three controls at once. You choose the model based on how much brainpower the task needs. You send the request through the Anthropic API, which is the bridge between your software and Anthropic's servers. And you make sure everything you send fits inside the context window, because that window is the model's entire world for that one reply.

The API is the pipe. The model is the brain. The context window is the workbench. A brilliant brain with a cluttered workbench cannot spread out a large problem. A large workbench does not help if the brain is wrong for the job. Your work as a developer is to pair the right model with the right task, then clear enough space on the bench for the model to do that task well.

So far, everything we have placed on that workbench has been text. But most real applications need the model to do more than write back. They need it to act, to query a database, check live prices, or run a command. In the next lesson, we will look at Tool Use. That is how you give Claude the ability to call functions through the same API and context window you are learning to manage.
