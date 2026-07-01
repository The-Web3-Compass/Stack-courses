# Making Your AI Music Move at the Right Speed

## Why this exists

Imagine you have built a small app that generates background music for people. A user types "chill beats for studying" and your app sends the request off to Suno. A minute later, the music arrives. But instead of a relaxed groove, the track races ahead like an alarm clock. The user frowns and closes the app.

You try again with "slow ambient sleep music." This time the result is so sluggish it feels like it is moving through honey. Your prompt described a mood, but moods do not come with built-in speedometers. Words like "chill," "energetic," or "driving" mean different things to different people, and the AI has to guess.

That guesswork is the problem. When you rely only on text prompts, the speed of the music, what musicians call the tempo, is left to chance. Two requests with the same prompt can come back at totally different speeds. For some projects that is fine. For others, speed is everything. A workout app needs the beat to match a runner's footsteps. A meditation timer needs a pulse that slows the breath. A game needs action music that races when the player sprints.

You need a way to say exactly how fast the music should go. Not with more adjectives. With a number.

## Understanding the idea

This is what soundTempo does. It is a setting inside your Sounds Task that lets you pick the speed of the generated track using a real measurement musicians already understand: beats per minute, or BPM.

Think of BPM like the setting on a metronome. 60 BPM means one beat every second. That is slow, like a heartbeat at rest. Around 120 BPM is the bounce you hear in most pop songs. Push past 160 and you are in the territory of fast dance music or frantic rock. You can set soundTempo anywhere from 1 to 300, or you can leave it blank. When you leave it blank, Suno chooses automatically based on your prompt.

So soundTempo is simply your way of locking in the speed. When you leave it unset, you are saying "read my prompt and guess." When you enter a number, you are saying "ignore the guess, use this exact pulse."

It works alongside the other details you already know about. You have learned how callBackUrl tells Suno where to deliver the finished track, how soundLoop decides whether the music repeats, and how grabLyrics can pull the words out afterward. soundTempo is another lever inside that same request.

## A simple example

Picture a running coach who wants a playlist generator for her athletes. She does not want random songs. She wants the beat of the music to match the runner's cadence, the number of steps they take each minute.

A runner with a 150 step-per-minute stride needs music that hits 150 beats per minute. Without soundTempo, the coach sends a Sounds Task with the prompt "upbeat running music" and hopes. Maybe she gets 130 BPM. Maybe 170. The runner's feet fall out of sync.

With soundTempo, she sends the same prompt but adds the number 150. Now the generated track lands exactly on the runner's rhythm. The beat and the footsteps line up without the runner having to think. The music becomes a piece of gear, like a good pair of shoes, instead of a lucky draw.

The same idea works for a sleep aid app. The developer wants ambient tones that breathe at 60 BPM, roughly one beat per second, to guide slow breathing. Setting soundTempo to 60 removes the risk of a frantic middle section that jolts the user awake.

## How to think about it

soundTempo is the bridge between a vague feeling and a precise result. Prompts describe color and mood. soundTempo describes motion. If you are building something where the exact speed of the music changes the experience, this is the dial you reach for.

You will use it whenever your Sounds Task needs to feel controlled rather than exploratory. It does not change the instruments or the singer. It does not change the words. It only changes how fast the clock ticks inside the song. When speed matters, set the number. When speed does not matter, leaving it blank is perfectly fine.


<InlineQuiz
  id="quiz-s4-l6-soundtempo-purpose"
  question="You send a Sounds Task with a prompt asking for dreamy piano for studying and you set soundTempo to 70. What should you expect?"
  options='["The music keeps the dreamy piano mood and plays at a steady 70 beats per minute.","The music ignores the prompt and plays a generic track at exactly 70 BPM.","The music stays dreamy but the tempo drifts because the prompt overrides the number.","The music plays at 70 percent volume while keeping the dreamy piano sound."]'
  correct="0"
  explanation="soundTempo locks the speed without touching the mood or instruments. The prompt still shapes the style, so dreamy piano is preserved, and the number guarantees the exact pulse. Option B misreads the lesson; overriding the guess means overriding the speed guess, not the entire prompt. Option C is wrong because the explicit number takes priority over the prompt's implied speed. Option D confuses beats per minute with volume."
  courseSlug="suno-a-beginner-s-guide-to-prompt-beginner"
  lessonSlug="06-making-your-ai-music-move-at-the-right-speed"
/>

## Where you'll see this next

Now that you can control the speed of the music, the natural next step is to make sure the whole request lands safely and that the result comes back the way you expect. You know how to shape the sound inside a Sounds Task. Soon you will see how to verify your setup, how to handle the callback when the track is ready, and how to refine other qualities of the finished audio. The conversation is shifting from "what kind of music do I want" to "how do I reliably receive and refine it." You are ready for that.

---
[← Previous](./05-the-sentence-that-starts-every-music-request.md) · [Next →](./07-why-suno-makes-you-sing-a-secret-sentence.md) · [Course home](./README.md)
