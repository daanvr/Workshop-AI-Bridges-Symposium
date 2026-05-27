# Prompts: Wikipedia to QuickStatements

Companion to the [Wikipedia to QuickStatements](../exercises/wikipedia-to-quickstatements.md)
exercise. These cover the two main directions (article body to QS,
reference list to QS), plus verification, date formatting, working in
the sandbox, and going back the other way (Wikidata item to prose).

Anything in `[square brackets]` is a slot for you to fill in.
Default target is the sandbox item Q4115189.

## Article body to QuickStatements

The default workhorse.

```
Below is text from the Wikipedia article about [subject]. I want to
add statements about it to the Wikidata Sandbox item Q4115189 (for
testing). Extract every factual claim you are confident about and
output it as QuickStatements v2 commands, one per line, tab separated,
target item Q4115189. Use real Wikidata property IDs (P31, P569, etc.).
For dates use the format +YYYY-MM-DDT00:00:00Z/11 (or /10 for month
precision, /9 for year). For items use Q identifiers. If you are not
sure of a property or Q ID, leave a placeholder in square brackets and
a comment line starting with #. Do not invent facts that are not in
the source text.

[paste article text]
```

Same prompt, scoped to a specific kind of claim.

```
From the text below, extract only QuickStatements lines for these
property types: P569 (date of birth), P570 (date of death), P19
(place of birth), P20 (place of death), P106 (occupation), P27
(country of citizenship). Skip anything else. Target Q4115189.

[paste article text]
```

## Reference list to QuickStatements

```
Below is the reference list from the Wikipedia article about [subject].
For each reference, output a QuickStatements v2 line that adds it as a
reference to a statement on Q4115189. Use the reference properties:
S248 (stated in) when the source has a Wikidata item, S854 (reference
URL), S1476 (title), S577 (publication date), S813 (retrieved), S407
(language), S1433 (published in). Skip any reference you cannot parse
cleanly. Do not invent URLs or dates.

[paste references]
```

## Verification

Use AI to check AI. Slightly unusual, very useful.

```
Below is a block of QuickStatements v2 you produced earlier. For each
line, do three checks and report in a small table:
1. Is the property ID a real Wikidata property, and is it the right
   one for the claim?
2. Is the Q ID, if any, plausibly the right entity? (You cannot be
   sure without browsing; flag your confidence.)
3. Is the date format valid? (+YYYY-MM-DDT00:00:00Z/precision)

Do not rewrite the lines. Just produce the table with one row per
input line and a column "verdict": OK / suspicious / wrong.

[paste your QS lines]
```

## Date formatting on its own

For when you have dates as text and just want them normalised.

```
Convert each of the following dates into Wikidata's date format
(+YYYY-MM-DDT00:00:00Z) with the correct precision suffix: /11 for
day, /10 for month, /9 for year, /8 for decade, /7 for century. For
ambiguous dates flag them and pick the most defensible precision.

[paste dates, one per line]
```

## Suggesting property IDs

When you know the claim but not the property.

```
Below are short English sentences about a person. For each, suggest
the most likely Wikidata property to use. Output a table: sentence,
property ID, property label, one line justification, confidence (low /
medium / high).

[paste sentences, one per line]
```

## Sandbox to real item

When you are happy with the sandbox run and want to do it for real.

```
Below is the QuickStatements batch I ran successfully against Q4115189
(the Wikidata Sandbox). I want to run the same statements against
[real Q ID, e.g. Q12345]. Rewrite each line with the new target. Also
flag any line that I should probably double check before running it
on a real item (claims that overwrite existing values, claims that
add a date when one already exists, etc.).

[paste your QS lines]
```

## Reverse direction: Wikidata item to prose

For the "Going further" section of the exercise.

```
Here is the Wikidata item [Q ID] as a JSON export. Write one English
paragraph suitable for the opening of a Wikipedia article about it.
Stick strictly to claims that are sourced (have at least one reference)
and ignore the rest. Do not invent context. After the paragraph, list
the claims you used.

[paste the item JSON, or a few key claims by hand]
```

## Going further

Batch a Wikipedia category.

```
Below is a list of Wikipedia article titles in the category [British
women physicists]. For each title, list the three highest value
statements you would extract for QuickStatements (without actually
extracting them yet), with the property ID and the kind of value
expected. We will then go article by article.

[paste titles]
```

Asking AI to flag risk before you run anything.

```
Read these QuickStatements lines for the real item [Q ID]. Tell me,
honestly, which of them carry the highest risk if they are wrong: a
factual error that affects downstream Wikidata reusers, not just an
ugly edit. Rank them from highest to lowest risk and explain why in
one sentence each.

[paste lines]
```

---

Related: [exercise file](../exercises/wikipedia-to-quickstatements.md),
[index of prompts](./index.md), [index of exercises](../exercises/index.md).
