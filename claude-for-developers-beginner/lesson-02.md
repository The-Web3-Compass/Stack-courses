# Sonnet and Haiku: Choosing the Right Claude Model

Anthropic does not offer just one Claude. When you look at the models available through the Anthropic API, you will see a list of names that all begin with "Claude" but end in different words. Two of the most important names on that list are Sonnet and Haiku. They are not different AIs from different companies. They are siblings in the same family, built by the same team and from the same foundations, but designed for different kinds of work.

If you are new to building with AI, this variety can feel confusing. You might wonder why there is not simply one best model to use every time. The answer is that the real world contains many different jobs, and no single engine is efficient at all of them.

Why does this menu have to exist? Because a single model cannot be the best at everything. If Anthropic gave you only one option, you would face an impossible choice. Either that one model would be small and fast, in which case it would stumble on hard jobs like writing complex code, analyzing long legal contracts, or running multi-step agents. Or it would be large and powerful, in which case you would waste money and patience every time you used it to sort emails, label short messages, or answer simple yes-or-no questions. You would be forced to haul freight with a bicycle or pick up groceries with a semi-truck. Sonnet and Haiku exist so you can match the tool to the task instead of forcing every task through the same funnel.

## Sonnet: The Capable All-Rounder

Sonnet sits in the middle of the lineup. It is not the absolute largest model Anthropic makes, but it is the one many developers reach for first. Anthropic positions Claude Sonnet as a model for everyday development use cases. Think of it as the workhorse. It can write and debug code, carry on long conversations without losing track of the topic, and handle reasoning tasks that require several steps. It is particularly strong at coding tasks. Developers use it to generate functions, refactor legacy code, and review pull requests because it grasps how different parts of a codebase connect.

If you look at the current versions available through the API, you will see names like **Claude Sonnet 4.6** and **AWS Claude Sonnet 4.5**. These are newer-generation models that replaced earlier third-generation versions. When you send a request through the Anthropic API, you must provide the exact model identifier. For example, the identifier for AWS Claude Sonnet 4.5 is `aws__claude_4_5_sonnet`. The API does not guess. If you want that specific version, you must spell the name exactly as the platform expects.

Sonnet can also generate very long responses. AWS Claude Sonnet 4.5, for instance, can produce up to 64,000 tokens (the small pieces of words the model processes) in a single reply. That is useful when you need a detailed report, a large block of code, or a thorough rewrite of a document. Because Sonnet balances capability with reasonable speed, it is the usual choice for building agents that need to make decisions, call tools, or work through development tasks where errors are expensive.

The trade-off is cost and latency. Sonnet is more expensive per request than Haiku, and it takes longer to finish a reply. You would not want to use it for a task that requires an instant response thousands of times per minute. It is built to be thoughtful, not instantaneous.

## Haiku: The Fast and Efficient Option

Haiku is the smaller, quicker sibling. Its job is to handle high-volume, simple work without draining your budget or making users wait. The current version you will encounter is **Claude Haiku 4.5**. It is accessed through the same Anthropic API as Sonnet, but it uses fewer computing resources per request. That means lower prices and faster responses.

Haiku is built for situations where you need a touch of language understanding at massive scale. When you need to classify a sentence, extract a date from an email, or answer a straightforward question, Haiku returns an answer almost instantly. It is also the model many teams use for internal tooling that does not face customers directly. A script that tags support tickets, a parser that pulls names and dates from form submissions, or a nightly job that summarizes server logs all fit Haiku comfortably. If you are running a customer support bot that needs to route thousands of incoming messages to the right department, Haiku can do that at a speed and cost that keeps the service affordable.

The obvious trade-off is depth. Haiku is not the right choice for writing a multi-file software feature or reasoning through a fuzzy, open-ended problem. It can still follow instructions well, and it understands language precisely, but its strength is breadth and speed rather than heavyweight analysis. It is the model you deploy when the volume of requests is high and the complexity of each request is low.

## Picking the Right Model for the Job

Choosing between them is not a matter of loyalty or brand preference. It is a matter of reading the constraints of your project. Three questions usually decide it: How complex is the thinking? How fast must the answer arrive? How much are you willing to pay for every thousand requests?

Developers sometimes feel pressure to pick the most powerful model for every feature. That instinct comes from a good place. You want quality. But treating every request like a hard problem is like hiring a brain surgeon to put a bandage on a scraped knee. The bandage will go on straight, but you will pay far too much and wait far too long. The best way to understand the split is to walk through a few realistic situations.

Imagine you are building an invoice automation system. The software must read messy scanned documents, understand different formats, and then write structured data to your database. This is a complex task with room for costly errors. A single mistake could misrecord a payment amount or assign an invoice to the wrong vendor. Here, Sonnet is the clear choice. You pay more per invoice, and you wait slightly longer for each response, but you get the accuracy and reasoning power needed to handle variations in the documents. Using Haiku for this would save money on paper, but the error rate would likely be too high. You would spend more time fixing mistakes than you saved.

Now imagine you are building a content moderation filter for a busy social app. Every comment, post, and image caption needs a quick safety check before it goes live. You are processing millions of items per day. Latency matters because users hate waiting, and cost matters because millions of API calls add up fast. Haiku shines here. It can flag obvious violations in milliseconds for a fraction of a cent. You might still send borderline cases to Sonnet for a second look, but the bulk of the work belongs to Haiku. The trade-off is acceptable because most decisions are easy, and the rare hard case can be escalated.

Finally, consider a real-time writing assistant that suggests the next sentence as a user types inside a document. Speed is everything. If the suggestion takes even a second to appear, it feels broken. The user will ignore it or turn it off. Haiku is ideal for this. It can read the last few sentences and generate a short continuation instantly. Sonnet would produce richer suggestions, but the delay would ruin the experience. In this case, fast and good enough beats slow and perfect.


<InlineQuiz
  id="quiz-s3-l2-model-selection-workflow"
  question="You are building a customer support system that receives thousands of tickets per hour. Most are simple routing requests, but about five percent involve complex billing disputes that require detailed reasoning. According to the lesson, how should you assign models?"
  options='["Send every ticket to Sonnet so the complex billing disputes are handled correctly from the start.","Send every ticket to Haiku because it is the only model that can keep up with that volume.","Route the simple tickets to Haiku and escalate the complex billing disputes to Sonnet.","Use Sonnet for the simple tickets and Haiku for the billing disputes to balance cost and speed."]'
  correct="2"
  explanation="The correct approach is to match the tool to the task. The lesson explicitly warns against using Sonnet for everything, comparing it to hiring a brain surgeon for a scraped knee. It also warns against forcing a single model onto all high-volume work. Haiku is ideal for the simple routing because it is fast and cheap at scale, while Sonnet is reserved for the complex disputes where reasoning errors are costly. The last option reverses the roles: Sonnet is the capable all-rounder for hard problems, not simple ones, and Haiku lacks the depth for detailed billing reasoning."
  courseSlug="claude-for-developers-beginner"
  lessonSlug="02-sonnet-and-haiku-choosing-the-right-claude-model"
/>

## A Simple Rule

Do not ask "Which Claude model is the best?" Ask "What does this specific task demand?" If the task is hard, unusual, or requires long output, and you would gladly wait an extra second to get it right, reach for Sonnet. If the task is simple, repetitive, or needs to happen instantly and cheaply at scale, reach for Haiku.

These two models are not rivals. They are options on the same dial. Turning the dial toward Sonnet gives you more brainpower. Turning it toward Haiku gives you more speed and savings. Most production systems eventually use both, sending easy work to Haiku and reserving Sonnet for the moments that matter.

In the next lesson, we will look at the doorway you use to reach these models: the Anthropic API itself. We will also explore the context window, which is the amount of text a model can hold in its working memory at once. Understanding that limit will help you decide not only which model to use, but how much information you can feed it in a single conversation.
