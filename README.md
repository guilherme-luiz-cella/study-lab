# study-lab

A Claude Code skill that studies with you instead of summarizing at you.

Point it at your slides and it runs the session backwards from what you'd expect. It asks, you answer, and only then does it tell you anything. Say "I don't know" and it makes you guess anyway.

One rule holds the whole thing together:

> You produce the answer before Claude does.

## Why not just ask Claude to explain it

Because you'll nod along and remember nothing. I know because that's exactly what I was doing before I wrote this.

A good explanation feels like learning, and that feeling is the trap. What you get is fluency with the text, not access to the idea. The part that actually builds memory is the uncomfortable part: trying to produce the answer and finding out whether you can.

So the skill spends its effort on making you produce things, and on not letting you off the hook when producing gets unpleasant.

## How a session goes

It reads your material first. Slides for the skeleton, the book for depth, one section at a time. Never the whole discipline at once.

Then it opens with a question. No summary, no plan, no menu of options. Small enough to answer in a breath, because a session you can't bring yourself to start is a session that doesn't happen.

You commit to an answer. "I don't know" doesn't buy you a hint; it just gets you asked again with a "guess anyway". A wrong guess followed by the correction sticks better than reading the right answer cold. That's one of the more annoying findings in learning research, and this skill leans on it hard.

Then it climbs. State the definition. Apply it to a case. Tell two lookalike cases apart. Find where the rule breaks. Move it to a problem from outside the material. Explain it to someone who never took the course. It won't sit on the easy rung just because you keep getting those right.

At the end it asks you to say everything the section established, from memory, no scrolling. Then it writes the log.

## The hint rules

This is the part tutoring usually gets wrong, so it's written down:

**No autocompleting.** If you're groping for a word, it does not hand you the word. A half-answer gets a question back, never the missing half.

**One hint rung per message, then it stops.** No stacking three hints because the silence got long.

**Three real attempts before the answer.** Asking "what is it?" is not an attempt. Asking what a symbol means isn't either, but that one gets answered straight, because notation is vocabulary and not the answer. Then the original question comes back unchanged.

**"Got it" doesn't close a point.** Saying the rule back in your own words closes it.

Tutoring systems show a consistent negative association between unproductive hint use and learning. The hint button is the escape hatch. This one is narrow on purpose.

## The log

Each session writes `study-log/<topic>.md` next to your material:

```markdown
## Errou
- Θ vs caso médio: answered "Θ is the average case", correct is "Θ bounds whichever
  function you chose". Cause: fused the choice of case with the choice of notation.

## Firmou com dica
## Acertou limpo
## Próxima sessão
```

The Cause line is the whole point. "Confused Θ with the average case" is a fact you can fix. "Got question 3 wrong" is not. Next session on that topic reads the log and opens with the missed items, cold, before anything new.

## Install

```bash
git clone https://github.com/guilherme-luiz-cella/study-lab.git
cp -r study-lab/skills/study-lab ~/.claude/skills/
```

Then, in Claude Code:

```
/study-lab
```

Or just say "study this with me" or "quiz me" and point at the material. It runs in whatever language your material is in, so Portuguese slides get a Portuguese session.

## Design notes

The skill assumes a learner who does better with structure imposed from outside than with a study plan they have to maintain themselves, and who gets derailed by a high cost of entry faster than by a hard question.

In practice that means Claude picks the method instead of asking you to. The format never changes between sessions. Questions say what form the answer should take. The numbers you need are repeated in the question instead of sitting three messages up. A ten-minute session counts as a real session and gets logged like any other.

`SKILL.md` cites the research behind each of those at the bottom of the file.

## License

MIT
