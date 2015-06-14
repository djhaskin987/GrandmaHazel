# GrandmaHazel

A collection of geneology algorithms

Right now this is in its infancy, but I've wanted to codify how I determine if a record is genuine evidence
that that person existed for a long time. To automatically reconcile records, not just provide hints, is what
I'm after here. I seek to answer the question: Given this record, and this person, does this record match (or
could it possibly match) this person?

## Names / Place Names

When I answer this question manually, place names and names follow these rules:

1. A name is divided into space-separated terms. For each term:

 1. If it's an abbreviation of the name on the record, consistency is not abridged.
 2. If it's an exact match or small edit as the name on the record, confidence is increased.

So, we basicaly have an edit distance algorithm with these facts:

1. deletion doesn't cost any consistency, but it does cost specificity
2. Substitution costs little consistency at first, and not specificity, but lots the larger it is. This 
is because it is easy to mistake a character, evenstring of characters, when digitizing a record; but after a 
while it's a whole different word.
3. Heuristic: The first letter is rarely mistaken in a record. if this doesn't match, it's a huge blow.
4. insertion costs a lot. it is generally easier to mistake the reading of a character than its presence at
all. After about three characters, this should sink the proposition.
 
Proposal: For confidence, where 0 confidence is "I don't know" and 100 confidence is "that's the person":

    (1 - d) .5 * (.5 * )^2
