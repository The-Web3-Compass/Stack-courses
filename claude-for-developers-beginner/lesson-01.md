# The Claude Family and When to Use Opus

You finish your API sign-up. You copy your key, open your editor, and write your first call to Anthropic. Then you pause. The documentation asks you to pick a model. You see a list of names. `claude-opus-4-8`. `claude-sonnet-4-6`. `claude-haiku-4-5`. You pick the first one because it sounds like the flagship. Everything works. But over the next week your application slows down. Your dashboard shows costs climbing on simple requests that should be nearly free. A user complains that a basic greeting took three seconds. You are using a racehorse to pull a cart.

This is the first trap of working with large language models. The newest or most capable name is not the right name for every job. Anthropic builds the Claude models as a family on purpose. The family gives you a dial, not a switch. If you learn to read that dial, you can keep your application fast and your budget under control while still solving genuinely hard problems.

## One Family, Three Seats on the Bench

The Claude model family is Anthropic’s lineup of AI models served through the Anthropic API. Think of it as a single bench with three seats. Each seat belongs to a different model tier, and each tier is tuned for a different balance of three things: capability, speed, and cost.

At one end sits Claude Opus. It is the strongest reasoner in the group. In the middle sits Claude Sonnet, built for everyday production work. At the far end sits Claude Haiku, designed to answer simple questions with minimal delay and minimal cost. The version identifiers you see in the documentation, like `claude-opus-4-8`, `claude-sonnet-4-6`, and `claude-haiku-4-5`, are the exact names you pass in your API call to choose your seat. The version numbers change as Anthropic releases improvements, but the three tiers stay constant. Learning the tiers matters more than memorizing the current version number.

These models are not ranked from bad to good. They are ranked from lean to deep. A pocket knife and a chef’s knife are both knives. You choose based on what you are cutting. The same logic applies here. If you treat the family like a single tool, you will blunt your budget and frustrate your users.

Why not just build one perfect model? Because capability, speed, and cost are locked together. A model that reasons through thousands of lines of code cannot also be the cheapest, fastest option for a one-sentence reply. By offering a family, Anthropic lets you match the tool to the task instead of forcing every request through the same expensive funnel.

## Opus: The Heavy Lifter

Opus is the deepest thinker in the Claude family. When Anthropic releases a new generation, Opus carries the most advanced reasoning and the largest capacity for complex work. As of this writing, that means models such as Claude Opus 4.8.

What does "more capable" actually mean? It means Opus can hold more concepts in its head at once. It can trace a bug through a sprawling codebase where the cause and the symptom live in different directories. It can plan a multi-step agentic workflow, decide what tool to call next, and remember why it made that choice ten steps later. It can read a dense technical specification and spot the subtle contradiction on page forty that a lighter model might skim past.

That depth has a direct cost in two currencies. The first is time. Opus generates its response more deliberately. It is not stalling. It is running a longer internal reasoning process to reduce errors. The second currency is money. API pricing is based on tokens, which are roughly pieces of words. Opus costs more for every token it reads and every token it writes than the other tiers. You are paying for the extra compute and the deeper search through possibilities.

This is a feature, not a bug. Anthropic gives you Opus so you have a place to send the hardest problems. The mistake is sending every problem there.

## When Opus Earns Its Keep

Picture a real scenario. You inherit a massive codebase. Thousands of files. Outdated dependencies. A critical bug is crashing production, and the error message points to a single line that looks fine on its own. You paste the stack trace, the surrounding modules, and the dependency graph into a prompt. A lighter model might suggest adding a null check because that is the surface symptom. Opus can reason across the architecture, notice that a recent refactor changed an interface contract three layers away, and generate a patch that fixes the root cause. For a crisis like that, the extra seconds of latency and the higher token cost are trivial compared to the downtime you avoid.

Or imagine you are building an autonomous research agent. The agent must search documents, decide which ones matter, extract claims, compare them against each other, and decide whether the question is fully answered. Each step depends on the last. If the model takes a shortcut, the agent might loop forever or confidently report a wrong conclusion. Opus was built for these long-horizon tasks. It keeps its eye on the original goal even after many turns.

Now flip the scenario. You are building a customer support bot. A user asks, "What are your business hours?" The answer is a single sentence stored in a database. If you route that question through Opus, you are burning expensive tokens and making the user wait for a deep reasoning process that adds no value. A lighter model from the same family can return that answer in a fraction of a second for a fraction of the cost. The family exists so you can make a different choice for that request.


<InlineQuiz
  id="quiz-s3-l1-opus-task-routing"
  question="Your application can route incoming requests to different Claude model tiers. Which request should you send to Claude Opus?"
  options='["A user asks for your business hours, and the answer is one sentence stored in a database.","A production crash in a massive codebase where the stack trace points to a line that looks fine and the root cause likely sits layers away.","A user sends a simple greeting that needs an immediate acknowledgment to keep the UI responsive.","A production error that points to a specific line and only requires a null check to stop the surface symptom."]'
  correct="1"
  explanation="The correct choice is B because Opus is designed for deep reasoning across wide contexts, such as tracing a bug through a sprawling codebase where the cause and symptom are separated by many layers; the extra latency and cost are justified by the accuracy gained. Option A is a predictable factual lookup that the lesson explicitly warns against routing through Opus, since it would burn expensive tokens and make the user wait for unnecessary reasoning. Option C demands minimal delay, which is the opposite of Opus's deliberate generation pace; the lesson uses the example of a basic greeting taking three seconds to show the mismatch. Option D describes a shallow surface fix that a lighter model can handle; the lesson contrasts this exact scenario with Opus's ability to find root causes hidden deep in the architecture, so sending it to Opus would be overkill."
  courseSlug="claude-for-developers-beginner"
  lessonSlug="01-the-claude-family-and-when-to-use-opus"
/>

## A Simple Rule for Choosing

The mental model is straightforward. Before you send a prompt, ask how much unseen reasoning the answer requires.

If the task demands deep analysis, multi-step planning, or creative problem solving across a wide context, reach for Opus. Accept the slower response and the higher price as the fair cost of accuracy.

If the answer is predictable, short, or drawn from a narrow set of facts, Opus is overkill. You would be renting a warehouse to store a single shoebox.

Over the next two lessons we will fill out the rest of the bench. We will look at Claude Sonnet, the workhorse that handles most coding and business tasks without Opus's price tag. Then we will look at Claude Haiku, the sprinter built for high-volume, simple jobs. Once you know all three, you can route each request to the right seat instead of guessing.
