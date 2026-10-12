# Milestone 1: Community Notes

Community: r/LivestreamFail

I reviewed 40 recent public feed entries. Most are clip links with a short title or caption. I also read comments in two public threads; comment text, not the clip title or video, is the intended classification unit.

## Candidate Distinctions

- **Context-rich vs. bare-moment titles:** Some explain who is involved and what is happening (for example, Kai Cenat's detailed Outlast setup); others give only a moment such as "Lirik presses a button."
- **Concrete specifics vs. general wording:** Some include measurable details, such as "28 days" and "745,000 purchased blinks"; others rely on broad wording like "mindblowing gameplay."
- **Cause or consequence vs. event alone:** Some explain what led to or followed an event (Payo ending stream after a duel); others state only a general reaction, such as "Erobb just can't win."
- **Attributed or qualified claims vs. direct framing:** Some signal a source or uncertainty with wording like "alleges" or "allegedly"; others present the event directly without qualification.

These title-level patterns were exploratory, not final labels. The comments provide more useful variation for the text classification task.

## AI Stress Test

I generated eight synthetic comments and classified them with the draft rules:

1. `The clip's poll at 9:14 shows 82% chose "stop the ads."` - `analysis`
2. `In the May VOD, he said, "I don't take casino sponsors."` - `analysis`
3. `He's a greedy liar.` - `hot_take`
4. `Anyone promoting this is a bad person.` - `hot_take`
5. `Lmao, his face when the screen changed.` - `reaction`
6. `That jump scare got me, lmao.` - `reaction`
7. `82% of viewers hate these ads.` - `hot_take`
8. `The poll screenshot shows 82% chose "stop the ads" out of 2,100 votes.` - `analysis`

The number-only claim in item 7 stays `hot_take`; item 8 is `analysis` because the poll and count are identified as checkable evidence. That distinction made the test cases consistently classifiable.
