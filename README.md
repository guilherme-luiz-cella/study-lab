# study-lab

A Claude Code skill that studies *with* you instead of summarizing *at* you.

Point it at your course material and it runs the session as an experiment: it asks first, makes you commit to an answer before it reveals anything, gives the smallest hint that could unstick you — one step at a time — and writes down what you missed so the next session opens there.

One rule holds the whole thing together:

> **You produce the answer before Claude does.** Explaining first feels helpful and teaches almost nothing. Recognition is not recall.

## Why not just ask Claude to explain it

Because you will nod along and remember nothing. Reading a good explanation feels like learning, and the feeling is the problem: it is fluency with the *text*, not access to the *idea*. The moment that actually builds memory is the one where you try to produce the answer and find out whether you can.

So this skill spends its effort on making you produce things, and on not letting you off the hook when producing is uncomfortable.

## How a session goes

1. **It reads your material.** Slides for the skeleton, the book for depth, one section at a time. Never the whole discipline at once.
2. **It opens with a question.** No summary, no plan, no menu of options. Small enough to answer in a breath, so the session costs almost nothing to start.
3. **You commit.** "I don't know" is not an answer and does not earn a hint — it asks you to guess anyway. A wrong guess followed by the correction sticks better than reading the right answer cold.
4. **It climbs.** Recall → apply → discriminate two lookalike cases → find where the rule breaks → transfer to something outside the material → explain it in your own words. It will not park on easy questions because they go well.
5. **It rations hints.** Four rungs — locate, decompose, concrete example, answer — one rung per message, and the answer only after three real attempts.
6. **It closes with free recall**, then writes a log.

## The hint rules

This is the part most tutoring gets wrong, so it is written down explicitly:

- **No autocompleting.** If you are groping for a word, it does not hand you the word. A half-answer gets a question back, not the missing half.
- **One hint rung per message, then it stops.** No stacking hints because the silence got long.
- **Three genuine attempts before the answer.** Asking "what is it?", asking what a symbol means, or restating the question do not count as attempts. Notation questions get answered straight — that is vocabulary, not the answer — and then the original question comes back unchanged.
- **Nothing passes on a nod.** "Got it" does not close a point. Restating the rule in your own words closes it.

Tutoring systems show a consistent negative association between unproductive hint use and learning. The hint button is the escape hatch, so this skill makes it narrow on purpose.

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

The **Cause** line is the point. "Confused Θ with average case" is a fixable fact; "got question 3 wrong" is not. The next session on that topic reads the log and opens with the missed items, cold, before any new material.

## Install

```bash
git clone https://github.com/<you>/study-lab.git
cp -r study-lab/skills/study-lab ~/.claude/skills/
```

Then, in Claude Code:

```
/study-lab
```

Or just say "study this with me" / "estudar" / "quiz me" and point at the material. It runs in the language of your material — Portuguese slides mean a Portuguese session.

## Design notes

The skill is tuned for learners who do better with externally enforced structure than with self-directed study, and who are more easily derailed by a high cost of entry than by a hard question. That shows up as: Claude picks the method instead of asking you to, the format never changes between sessions, questions state the form of the answer they want, the numbers you need are repeated in the question instead of three messages up, and a ten-minute session counts as a real session.

`SKILL.md` cites the research behind each of those choices at the bottom of the file.

## License

MIT
