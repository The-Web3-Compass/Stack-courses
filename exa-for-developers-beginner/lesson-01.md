# Why AI Needs Its Own Search Engine

Imagine you are building an AI assistant. A user asks it to compare two JavaScript frameworks, or to summarize yesterday's news, or to debug an error using the latest version of a library. Your AI cannot know everything. Its training data stops at a cutoff date. If it guesses, it might invent facts. This is the hallucination problem, and the usual fix is to let the AI search the web.

So you hook it up to a traditional search engine. But the results come back formatted for human eyeballs. They are HTML pages stuffed with navigation bars, cookie banners, ads, and paragraphs optimized for advertising revenue rather than clarity. Your AI must wade through all that clutter just to find a single number or quote. It burns through its context window reading irrelevant markup. Worse, traditional search assumes a human will click a link, skim the page, and judge its trustworthiness. Your software cannot click. It has to parse messy HTML and guess which result matters. You end up writing layers of glue code just to clean up data that was never meant for a machine to read.

Even if you solve the cleanup problem, you hit another wall. Human search engines return the same kind of result for every query. Whether the user wants a quick phone number or a deep market analysis, the engine treats it the same way. It returns ten blue links and hopes a human finds what they need. An AI application needs more structure. It needs to know when an answer is fast and shallow versus slow and thorough. It needs a search layer that understands software, not just people.

This is the gap Exa was built to fill.

## A search engine built for code, not clicks

Exa is a search engine made for AIs. It is an API your application calls directly, not a website your users visit. Every part of its design assumes the consumer is software that reasons, not a person browsing links. Instead of giving you pages built for clicks, Exa gives you information built for consumption by code. Because an API has no eyes, Exa skips the visual noise and returns structured results your AI can use immediately.

Because not every question is the same, Exa offers different search types. They trade speed against depth. You can think of it as turning a dial from instant answers to thorough research. The right setting depends on what your user is doing and how long they can wait.

## Turning the dial from fast to thorough

```mermaid
%%{init: {'theme':'base','themeVariables':{'primaryColor':'#FFA726','primaryTextColor':'#111111','primaryBorderColor':'#111111','lineColor':'#111111','secondaryColor':'#FFF3E0','secondaryTextColor':'#111111','secondaryBorderColor':'#111111','tertiaryColor':'#FFFFFF','tertiaryTextColor':'#111111','tertiaryBorderColor':'#111111','fontFamily':'Inter, ui-sans-serif, system-ui, sans-serif','fontSize':'14px'}}}%%
flowchart LR
    A[Instant lookup] --> B[Everyday balance] --> C[Deep dive]
```
*Figure: Exa’s search modes arranged as a speed-depth spectrum from instant answers to thorough research.*


### The instant lookup (~250 ms)

At the instant end of the dial, results come back in roughly two hundred and fifty milliseconds. This is for moments when any delay breaks the experience. A user is chatting with your bot and asks a simple follow-up. "What version of Node.js is current?" or "When was this company founded?" You cannot ask them to wait ten seconds. The instant profile grabs the freshest information and returns it fast enough that the conversation flows naturally.

The trade-off is that this mode is built for discrete facts and straightforward queries. It is not trying to write a report or compare conflicting sources. It is fetching a specific needle from the haystack and handing it over immediately. If you ask it to analyze a broad trend, it will not have time to do the topic justice.

### The deep dive (12-40 seconds)

At the other end of the dial sits deep-reasoning search. This takes anywhere from twelve to forty seconds. It is for hard problems where the answer is scattered, nuanced, or requires synthesis. Imagine your AI is preparing a competitive brief, or researching a medical topic with conflicting studies, or debugging an obscure issue by gathering context from many different sources. Deep reasoning takes time because it does more work behind the scenes. It evaluates more pages, weighs contradictory claims, and assembles a thorough picture before it responds.

You would not use this in a live chat window. You use it when your application can work in the background, or when a user explicitly asks for a detailed report and is willing to wait. The trade-off is time, but the payoff is depth. You are essentially giving the search engine room to think.

### The everyday balance

Between those poles sits a balanced mode for everyday tasks. It is fast enough for most interfaces, but it digs deeper than an instant lookup. This is useful when a user asks something like "How do I implement OAuth2 in a React app?" The answer requires more than a single fact, but it does not need a full research project. This middle ground is often the default you reach for when you are unsure, because it offers a reasonable compromise between waiting and thoroughness.

## Three jobs that need different speeds

Choosing the right mode matters because the user experience changes completely based on your choice.

Consider a customer support chatbot. A user says their invoice looks wrong. The bot needs to check the company's latest pricing page. A two hundred fifty millisecond instant search pulls the current numbers. The user gets an answer while the conversation is still warm. The interaction feels instant and human. If the user then asks for a detailed comparison of enterprise plans across three years, the bot could schedule a deeper search or warn the user that a thorough answer will take longer. It does not force a forty-second wait for a simple lookup. The chatbot stays responsive by reserving deep reasoning for the questions that actually need it.

Now picture a coding assistant. A developer asks for the syntax of a Python function added last month. This is a quick lookup. Instant search is perfect. The developer gets the snippet and keeps working. But later the developer asks whether a new framework is production ready and what its known limitations are. That requires reading GitHub discussions, recent blog posts, and issue trackers. A deep-reasoning search can synthesize those scattered signals into a useful summary. The assistant might even run the deep search in the background while the developer reads the quick syntax answer. By using both modes, the assistant feels fast on the surface but remains deeply informed underneath.

Finally, imagine a research agent that writes daily briefs for a team. Every morning it scans news, papers, and press releases on a set of topics. It runs deep-reasoning searches overnight to build comprehensive summaries. Those summaries are stored and ready when the workday starts. Then during the day, when a user asks follow-up questions about those summaries, the agent uses instant searches to verify specific names, dates, or stock prices. The two modes complement each other. Deep reasoning builds the foundation. Instant search handles the spot checks.


<InlineQuiz
  id="quiz-s6-l1-search-mode-selection"
  question="You are building a research agent. During a live team meeting, a user asks for the closing stock price of Apple from yesterday. Later, the same user asks for a comprehensive analysis of Apple and its AI strategy drawn from recent news, academic papers, and earnings calls. Which approach correctly matches Exa search modes to these two requests?"
  options='["Use deep reasoning for the stock price and deep reasoning for the AI strategy.","Use instant lookup for the stock price and deep reasoning for the AI strategy.","Use everyday balance for both requests to keep the behavior consistent.","Use instant lookup for both requests because the user is in a hurry."]'
  correct="1"
  explanation="Instant lookup fits the stock price because it is a discrete fact needed immediately during a conversation, while deep reasoning fits the comprehensive strategy analysis because it must synthesize scattered and nuanced sources. Using deep reasoning for a simple stock price would force an unnecessary wait, while using instant lookup for the complex analysis would be too shallow and miss critical context. Defaulting to everyday balance for everything ignores the trade-offs and wastes either time or depth, and forcing instant lookup on a hard question just because the user is busy fails to respect the complexity of the request."
  courseSlug="exa-for-developers-beginner"
  lessonSlug="01-why-ai-needs-its-own-search-engine"
/>

## Picking the right tool

The mental model to keep is simple. Search is not a single tool that you apply uniformly to every problem. It is a spectrum from speed to thoroughness. Exa lets you place each query exactly where it belongs on that spectrum. You do not have to force every question into a fast but shallow box. You also do not have to accept slow answers for simple questions. You match the mode to the moment, and you respect the user's time by only asking them to wait when the complexity truly demands it.

Once you are comfortable choosing the right depth, the next challenge is shaping what actually comes back. Raw results can still contain more than your AI needs, and sending extra text wastes money and attention. In the next lesson, we will explore Highlights and the contents endpoint. They let you control precisely what information your AI receives, so you can feed it only the parts that matter.
