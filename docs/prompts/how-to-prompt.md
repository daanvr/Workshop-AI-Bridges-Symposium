# How to prompt

Before you reach for a template, the most important thing to know is
this: **prompts are not holy**. They are not magic spells. You can
change them, mash them together, leave half the sentence out, throw
the structure away. Many different prompts can get you the same good
result, and the same prompt can give you different results every time
you run it. There is no single best wording, and there is no wrong
move that costs more than one extra message.

This page is a short tour of a few patterns worth trying, and one big
idea that sits underneath all of them: just try things.

## Same prompt, different results. Different prompts, same result.

Two facts that look like contradictions and are both true:

1. **The same prompt produces different results.** AI is non
   deterministic. Run a prompt twice and you can get two different
   answers. Neither one is "right". One might happen to be more
   useful for what you need right now.
2. **Different prompts produce the same good result.** A clear messy
   prompt often beats a tidy vague one. There is no perfect wording
   waiting to be discovered.

What this means in practice: stop looking for the right way to ask.
Ask. If the answer is not what you wanted, change one thing and ask
again. The cost of trying is one message.

## Patterns worth trying

### Roast me

Hand the AI your work and ask it to find what is wrong with it. Treat
it like a tough interview, a code review, a sceptical colleague.

```
You are reviewing the draft below as a sceptical senior colleague.
Find five things that are weak, unclear, or wrong. Be specific. Do
not soften your feedback.

[paste your work]
```

Why it works: AI defaults to being nice. Asking explicitly for
criticism cuts through the politeness and gets you something
actually useful.

### Review what you (or it) just did

Do a thing. Then ask the AI to step back and review it. The review
pass often catches things the first pass missed.

```
Here is what we built / wrote / decided in the previous step. Before
we go further, review it. What is good, what is weak, what would you
change, what is missing entirely?
```

You can do this whether the previous step was the AI's work or yours.
A second look from a fresh angle is the cheapest improvement
available.

### Suggest improvements as a numbered list, I'll pick

Ask for improvements as a numbered list, then choose which ones to
apply. This keeps you in control instead of accepting a full rewrite.

```
Suggest 8 specific improvements to this draft, as a numbered list.
For each, give a one line description. Do not rewrite anything yet.
I will tell you which numbers to apply.
```

Then reply with: "apply 2, 5, and 7." You get exactly the changes you
chose and nothing else.

Why it works: it separates ideas from implementation. You see a menu,
you pick, you keep what you want.

### Babble (the voice prompt)

Talk into the box the way you would talk to a colleague at the coffee
machine. Do not punctuate. Run sentences together. Loop back on
yourself. Use the wrong word and correct it mid thought. This works.

```
ok so i need a thing that takes those museum csvs i have not the
clean ones the messy ones with the comma in the title field and
makes them into a json that i can put on a webpage but also actually
maybe i want a script because then i can rerun it later you know
what just suggest both options
```

Why it works: the model fills in the structure. You do not have to.
You think out loud and the AI takes it from there. A lot of the very
useful prompts in the rest of this folder started life as a babble.

## Be messy. Try things.

The single best way to get better at prompting is to do more of it,
not to read about it.

Copy a prompt from one of the other files in this folder. Change one
word. See what happens. Then change a different word. Then mash two
prompts together. Then throw both away and just babble into the box
about what you actually want. There is no wrong move. The cost of
trying something is one message; the cost of overthinking is the page
you never wrote.

Prompts are not holy. The results are not holy either. The only
thing that matters is whether the thing you got back is useful for
what you are doing today. If yes, keep going. If no, change one
thing and ask again.

---

Related: [index of prompts](./index.md), [index of exercises](../exercises/index.md).
