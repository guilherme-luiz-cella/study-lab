# study-lab

A Claude Code skill that studies with you instead of summarizing at you.

Point it at your slides and it runs the session backwards from what you'd expect. It asks, you answer, and only then does it tell you anything. Say "I don't know" and it makes you guess anyway.

One rule holds the whole thing together:

> You produce the answer before Claude does.

## Why not just ask Claude to explain it

Because you'll nod along and remember nothing. I know because that's exactly what I was doing before I wrote this.

A good explanation feels like learning, and that feeling is the trap. What you get is fluency with the text, not access to the idea. The part that actually builds memory is the uncomfortable part: trying to produce the answer and finding out whether you can.

So the skill spends its effort on making you produce things, and on not letting you off the hook when producing gets unpleasant.

## Install

```bash
git clone https://github.com/guilherme-luiz-cella/study-lab.git
cp -r study-lab/skills/study-lab ~/.claude/skills/
```

On Windows, the target is `%USERPROFILE%\.claude\skills\`.

That's it. There is nothing to configure and no API key of its own. Run `/help` in Claude Code if you want to confirm the skill was picked up.

## Step by step

**1. Put your material in one folder.**

PDFs, slides, lecture notes, a syllabus, whatever you actually have. The skill reads PDFs directly, so no conversion step.

```
graph-theory/
  lecture-04-graph-basics.pdf
  lecture-05-connectivity.pdf
  textbook-chapter-2.pdf
```

**2. Open Claude Code in that folder.**

```bash
cd graph-theory
claude
```

**3. Start a session and name the topic.**

```
/study-lab connectivity and bridges
```

You can also just ask in plain language: "study lecture 5 with me", "quiz me on connectivity", "estudar grafos". Naming a topic is better than saying "study everything" because one session covers one section properly instead of skimming a whole course.

**4. Answer the first question.**

It opens with a question, not a summary. It will be small on purpose. Answer it even if you're unsure, because how you answer sets the level for everything after it.

**5. Guess when you don't know.**

"I don't know" gets you asked again with a "guess anyway". This is not the skill being stubborn. Producing a wrong answer and then seeing the right one beats reading the right one cold, and the effect only works if you actually commit to something first.

**6. Ask for hints, but expect them to be stingy.**

Hints come one rung at a time: it names the region of your mistake, then asks a smaller question, then gives a concrete example, and only after three real attempts does it state the answer. Asking "what is it?" does not count as an attempt. Asking what a symbol means is fine and gets answered straight, since notation is vocabulary, not the answer.

**7. Stop whenever you want.**

Say "that's enough" or "para por hoje". Ten minutes counts as a session. Before closing, it asks you to recall the whole section from memory, then writes the log.

**8. Read the log.**

It lands in `study-log/<topic>.md` next to your material:

```markdown
## Errou
- Θ vs average case: answered "Θ is the average case", correct is "Θ bounds whichever
  function you chose". Cause: fused the choice of case with the choice of notation.

## Firmou com dica
## Acertou limpo
## Próxima sessão
```

The Cause line is the whole point. "Confused Θ with the average case" is a fact you can fix. "Got question 3 wrong" is not.

**9. Come back to the same topic later.**

Run `/study-lab` on it again and the first thing it does is read that log and re-ask what you missed, cold, before touching anything new.

## What a session actually looks like

```
you  › /study-lab asymptotic notation

lab  › Linear search on an array of n elements, worst case. Four claims,
       true or false, item by item:
       1. best case is Θ(1)   2. worst case is Θ(n)
       3. worst case is O(n²) 4. O(n²) is the tightest upper bound available

you  › 3

lab  › 3 is true. But 1 and 2 are true as well, and you left them out.
       Only 4 is false.
       Take 2. Worst case is n comparisons, so the cost function is n.
       Claim 2 says Θ(n) and claim 3 says O(n²), both true of that same
       function. What does each notation assert that the other doesn't?
       Answer with the definition, not an example.

you  › Θ is the average case and O is the ceiling

lab  › Half right: O is the ceiling. Θ is not the average case.
       Look at claim 2, which you just accepted: "the worst case is Θ(n)".
       If Θ meant average case, that sentence contradicts itself.
```

That is the shape of it: no opening summary, one question at a time, and the correction lands on something you already committed to.

## The hint rules

This is the part tutoring usually gets wrong, so it's written down:

**No autocompleting.** If you're groping for a word, it does not hand you the word. A half-answer gets a question back, never the missing half.

**One hint rung per message, then it stops.** No stacking three hints because the silence got long.

**Three real attempts before the answer.** Asking "what is it?" is not an attempt. Asking what a symbol means isn't either, but that one gets answered straight, because notation is vocabulary and not the answer. Then the original question comes back unchanged.

**"Got it" doesn't close a point.** Saying the rule back in your own words closes it.

Tutoring systems show a consistent negative association between unproductive hint use and learning. The hint button is the escape hatch. This one is narrow on purpose.

## Language

It runs in whatever language your material is in. Portuguese slides get a Portuguese session, including the log. Technical terms stay in the wording the material uses, so you study the vocabulary you'll be tested on.

## Design notes

The skill assumes a learner who does better with structure imposed from outside than with a study plan they have to maintain themselves, and who gets derailed by a high cost of entry faster than by a hard question.

In practice that means Claude picks the method instead of asking you to. The format never changes between sessions. Questions say what form the answer should take. The numbers you need are repeated in the question instead of sitting three messages up. A ten-minute session counts as a real session and gets logged like any other.

`SKILL.md` cites the research behind each of those at the bottom of the file.

## License

MIT
