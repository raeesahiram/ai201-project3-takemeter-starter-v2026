# TakeMeter

> ### 👋 Start here
>
> **New to this repo? Read [RUNNING.md](RUNNING.md) first** — setup, the
> notebook, the baseline, and what to do when something breaks.
>
> Once `python test.py` passes:
>
> ```bash
> head -5 data/practice_labels.csv     # the shape your labels.csv needs
> ```
>
> Then open `takemeter.ipynb` **in this folder** — in VS Code, or with
> `jupyter notebook` if you prefer. Pick the kernel: the `.venv` inside this
> project. Run section 1, which reports the hardware you'll be training on.
> Everything else waits until you have data.
>
> Nothing to upload, nothing to connect, no accounts and no keys. The notebook
> runs on your machine and writes next to your code.
>
> **The rest of this file is your submission.** Fill it in as you go.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     HOW TO USE THIS FILE

     Unit 5 asks for the first five sections. Unit 6 adds the five below them.

     Everything is pasted as TEXT. No screenshots, no images.

     ⚠️ The confusion matrix especially. The notebook prints one as a markdown
     table, ready to copy. A screenshot of a matrix earns nothing. Paste the
     table.
     ───────────────────────────────────────────────────────────────────────── -->

<!-- ═══════════════════════ UNIT 5 — THE BUILD ═══════════════════════ -->

## What This Does

<!-- Your community, and what your classifier sorts posts into. Three or four
     sentences. -->

This project classifies public comments from r/LivestreamFail. The clip thread provides context, but labels are based on the comment text, not on watching the clip.


---

## Label Taxonomy

<!-- Each label: a one-sentence definition and two real examples from your
     reading. Then your decision rule for the hardest boundary.

     The decision rule is worth a point on its own and it's the thing most
     people leave out. Every taxonomy has a hardest boundary. Name yours. -->

### `analysis`

**Definition:** Makes a claim and supports it with a specific, independently checkable fact, source, or quote.

**Example 1:**
> "There's a national hotline and opt in program to ban yourself from gambling..." ([comment](https://www.reddit.com/r/LivestreamFail/comments/1x3d7sl/comment/pfa0mzi/))

**Example 2:**
> "at least hes not like train going full gaslight mode saying hes an anti-gambling streamer" ([comment](https://www.reddit.com/r/LivestreamFail/comments/1x3d7sl/comment/pfaw6f9/))

### `hot_take`

**Definition:** Makes a confident judgment or claim without offering specific, checkable support; it might be true, but no evidence is given.

**Example 1:**
> "They've gone broke and need attention." ([comment](https://www.reddit.com/r/LivestreamFail/comments/1x3ne9l/comment/pfcq1cd/))

**Example 2:**
> "People still give this guy relevancy?" ([comment](https://www.reddit.com/r/LivestreamFail/comments/1x3d7sl/comment/pfa25ve/))

### `reaction`

**Definition:** Gives an immediate feeling, joke, or expression about the clip or discussion without making a supported argument.

**Example 1:**
> "standard Ronnie always enjoyable" ([comment](https://www.reddit.com/r/LivestreamFail/comments/1x3ne9l/comment/pfcmvxp/))

**Example 2:**
> "Guy has a jawline of a reverse letter c though." ([comment](https://www.reddit.com/r/LivestreamFail/comments/1x3ne9l/comment/pfcorr6/))

### The hardest boundary

**Which two labels:** `analysis` and `hot_take`

**The decision rule I used every time:**
The boundary case is a comment claiming "90% of Redditors would take a 250K deal..." ([comment](https://www.reddit.com/r/LivestreamFail/comments/1x3d7sl/comment/pfa3v3d/)). A number alone is not evidence: use `analysis` only when a concrete fact, source, or quote can be checked. If the support is missing, use `hot_take`, even when the claim sounds plausible or the tone is heated.



---

## The Dataset

<!-- Where you collected from, how you labelled, your counts, and three hard
     cases. -->

**Where the posts came from:**

Collected 200 public comments from the r/LivestreamFail comment feed. Each row
keeps the full comment text and its direct Reddit permalink in `note`. One
removed-comment placeholder was replaced with another public comment.

**How I labelled them:** <!-- Cold first? Pre-labelled with AI and corrected?
Say so plainly — the disclosure is required, not penalised. -->

I labelled the first 20 comments cold. The remaining 180 received AI-generated
first-pass labels, and I reviewed every comment against the taxonomy and
corrected labels where needed.

**Counts per label:**

| Label | Count | Share |
|---|---|---|
| `analysis` | 47 | 23.5% |
| `hot_take` | 94 | 47.0% |
| `reaction` | 59 | 29.5% |
| **Total** | **200** | **100%** |

**Three hard cases**

<!-- Any post that made you pause: what it was, which two labels it could have
     been, and what you chose. These are worth more than the easy 190. -->

**1.**
> *The post:* “Statistically, black people are less likely to be literate. But
> even more important: THEY ARE THE SAME RATES AS POOR PEOPLE OF ANY RACE.”
> ([comment](https://www.reddit.com/r/LivestreamFail/comments/1x3lkm6/kai_tries_to_read/pfcwn4o/))
>
> *Could have been:* `analysis` or `hot_take`
>
> *I chose `analysis` because* the comparison between literacy rates and
> poverty is offered as evidence for the post's argument about race and
> literacy. The heated closing does not erase that support.

**2.**
> *The post:* “She was uncomfortable, he pulled back, and was rightfully
> called out for the strange behavior.” ([comment](https://www.reddit.com/r/LivestreamFail/comments/1x0fl5t/noarmswhatley_makes_another_girl_uncomfortable/pfcuzt2/))
>
> *Could have been:* `analysis` or `hot_take`
>
> *I chose `analysis` because* the comment grounds its judgment in specific
> details about what happened in the clip and uses them to support its point
> about boundaries, rather than relying only on a general opinion.

**3.**
> *The post:* “Well the important context is all that is chill had the girl
> been of age. That is the question here, when in fact was he aware he was
> speaking to a 15 year old?” ([comment](https://www.reddit.com/r/LivestreamFail/comments/1x0pp1r/former_twitch_exec_calls_secrecy_over_dr/pfctt3o/))
>
> *Could have been:* `analysis` or `hot_take`
>
> *I chose `hot_take` because* it raises a pointed question about what someone
> knew, but gives no evidence about their awareness. The specific age alone
> does not support an argument about what they knew.

---

## The Training Run

<!-- Your starting model, your settings, and anything you changed and why. -->

**Base model:**

**Settings:** <!-- epochs, learning rate, batch size, seed -->

**Anything I changed from the defaults, and why:**

**Split sizes:** <!-- train / val / test, and per-label counts in the test
split. If a label had fewer than about 8 in test, say so — it explains a lot
of next unit's variance. -->



---

## How I Used AI

<!-- Two specific moments — what you asked, what came back, what you changed.

     ⚠️ Plus disclosure of any pre-labelling. If you had a model pre-label a
     batch and then read and corrected every one, say that. It's an allowed
     workflow and disclosing it costs you nothing. Not disclosing it is the
     problem. -->

**Moment 1**

- *What I asked for:*
- *What came back:*
- *What I changed:*

**Moment 2**

- *What I asked for:*
- *What came back:*
- *What I changed:*

**Pre-labelling disclosure:**

An AI generated first-pass labels for the 180 rows marked
`pre-labelled, checked` in `labels.csv`. I went back through every one against
the written taxonomy and corrected 10 labels. The first 20 rows were labelled
cold before that pre-labelling pass.

<!-- ═══════════════════════ UNIT 6 — THE TEST ═══════════════════════

     Don't fill these in during unit 5.
     ═══════════════════════════════════════════════════════════════════ -->

---

## Baseline vs. Trained

<!-- Both models on the same posts. `python baseline.py --trained results.json`
     prints this table for you. -->

| Measure | Baseline | Trained | Difference |
|---|---|---|---|
| Overall accuracy |  |  |  |
| Macro F1 |  |  |  |
| F1 — `label_one` |  |  |  |
| F1 — `label_two` |  |  |  |

**What I predicted before I looked:**
<!-- Milestone 1 asks you to write this BEFORE seeing the trained numbers. A
     prediction made afterwards isn't one. -->

**What the gap actually means:**
<!-- If the baseline matched your trained model, your fine-tuning added
     nothing — and that is a real finding, not a failure. Say it plainly. -->



---

## Run Log — Before

<!-- Five criteria across three seeds. The notebook's section 6 prints the
     spread table; the Target and Verdict columns are yours. -->

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1.  |  |  |  |  |  |
| 2.  |  |  |  |  |  |
| 3.  |  |  |  |  |  |
| 4.  |  |  |  |  |  |
| 5.  |  |  |  |  |  |

### Confusion matrix

<!-- ⚠️ TYPED AS A MARKDOWN TABLE. The notebook prints one ready to paste.
     An image of a matrix earns nothing. -->

| true \ predicted |  |  |  |
|---|---|---|---|
| **** |  |  |  |
| **** |  |  |  |
| **** |  |  |  |

**My biggest off-diagonal number, and what it means:**
<!-- Not "the model made mistakes" — WHICH boundary it didn't learn, and which
     direction. "7 real analysis posts were called hot_take and only 3 went the
     other way" is a direction, not just an error rate. -->



---

## Verdicts and Diagnoses

<!-- MET or MISSED against LAST UNIT's target. The target has to hold across
     all three seeds, not turn up sometimes. -->

| # | Criterion | Target | Verdict | How I decided |
|---|---|---|---|---|
| 1 |  |  |  |  |
| 2 |  |  |  |  |
| 3 |  |  |  |  |
| 4 |  |  |  |  |
| 5 |  |  |  |  |

**Diagnoses**

<!-- For each miss: the cause, and how you know. The four common causes are:
     too few examples for a label, a boundary you applied inconsistently, a
     genuinely hard label pair, and a task the model can't reach from this
     much data.

     ⚠️ Use your agreement report as evidence. It is the only instrument you
     have that can tell a LABELLING problem from a MODEL problem, and this
     section is graded on whether you used it that way. -->



---

## Agreement Report

<!-- Your rate against the staff set, and every disagreement adjudicated.

     Remember you labelled these 30 under the STAFF taxonomy in
     data/staff_taxonomy.md, not your own — so every argument below is made
     from those definitions and those decision rules. -->

**Agreement rate:** ___ / 30 = ___%

<!-- Nobody grades this number. A 60% who argues every disagreement from the
     stated rules beats a 95% who wrote "staff was right" nine times. Several
     of the 30 were chosen because they're genuinely ambiguous — you should be
     winning some of these. -->

**Disagreements**

<!-- Three lines each: the post, both labels, and who you think is right and
     why — grounded in the staff definitions you were both applying.

     Then sort each into one of three piles:
       (a) the rule covered it and I applied it loosely → a consistency problem
       (b) the rule genuinely doesn't say               → a gap in the definitions
       (c) the rule is ambiguous here and my reading is defensible → argue it.
           This is a legitimate win.

     Pile (a) is the one that matters most for your diagnosis: if you applied a
     written rule two different ways on 30 posts, that is direct evidence about
     what you did across your own 200. -->

**1.**
> *The post:*
>
> *Staff said / I said:*
>
> *My call, and why:*
>
> *Which pile:*

**2.**
> *The post:*
>
> *Staff said / I said:*
>
> *My call, and why:*
>
> *Which pile:*

**What the pattern in my disagreements tells me:**



---

## The Improvement

**What I changed:**

**Which diagnosis pointed at it:**

### Run Log — After

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1.  |  |  |  |  |  |
| 2.  |  |  |  |  |  |
| 3.  |  |  |  |  |  |
| 4.  |  |  |  |  |  |
| 5.  |  |  |  |  |  |

**Did it help, and how do I know:**

<!-- If it didn't, say so. Relabelling that didn't help is a genuinely
     interesting result and earns full credit. -->



---

## What's Still Broken

<!-- For each criterion still missed: what you'd do, and why you stopped. -->



**The gap between what I meant my labels to capture and what the model
learned:**
<!-- Two sentences. Your confusion matrix is the evidence. -->



<!-- ═════════════════════════════════════════════════════════════════════

     SUBMISSION CHECKLIST — unit 5

       [ ] criteria.md has five numbered criteria, each naming a NUMBER
       [ ] Each has a reason underneath tied to your data or taxonomy
       [ ] labels.csv: at least 150 rows, text/label/note, ONE file not split
       [ ] No label above 70%
       [ ] All five unit 5 sections have real content
       [ ] Label Taxonomy includes the decision rule for your hardest boundary
       [ ] The Dataset includes three hard cases
       [ ] results.json and test_split.csv committed (the notebook does this)
       [ ] At least four new commits
       [ ] Repository URL submitted — WRITE IT DOWN

     SUBMISSION CHECKLIST — unit 6

       [ ] Baseline vs. Trained table, with your prediction written beforehand
       [ ] Run Log — Before, five criteria across three seeds
       [ ] Confusion matrix TYPED AS A MARKDOWN TABLE
       [ ] A verdict on every criterion
       [ ] A diagnosis for every miss, using the agreement report as evidence
       [ ] Agreement Report with every disagreement adjudicated
       [ ] One improvement, with Run Log — After
       [ ] What's Still Broken
       [ ] results_three_seeds_before.json, results_three_seeds_after.json,
           baseline_results.json and
           agreement_results.json committed
       [ ] At least four new commits
       [ ] The SAME repository URL as last unit

     Do not delete and recreate this repository.
     ═════════════════════════════════════════════════════════════════════ -->

---

📖 **How to run this project: [RUNNING.md](RUNNING.md)**
