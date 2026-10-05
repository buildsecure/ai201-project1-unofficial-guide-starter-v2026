# The Unofficial Guide

<!-- Replace this line with your name and which corpus you picked. -->

> **This file is your submission.** Fill it in as you go — most sections get
> written during the milestone that produces them, not at the end.
>
> How the starter works, and every command you'll need, is in `RUNNING.md`.
> Leave that file alone.
>
> **Paste everything as text.** No screenshots, no video. A typed table gets
> full credit; a picture of the same table gets none.
>
> Delete these instruction blocks as you replace them. The `<!-- -->` comments
> are notes to you and don't show up when the page renders — you can leave them
> or remove them.

---

# Unit 1

## What This Does

<!-- Three or four sentences. Which corpus you picked, and the kinds of
     questions your system answers. Write it for someone who has never seen
     this repo.

     Milestone 5. -->
A RAG system built on the campus_life corpus — 88 short posts about students life at a university, dining halls, dorms, courses, and the administrative rules. Students can ask questions about campus life knowledge in plain english, and the system returns the results based on the documents. Students can ask questions like `Provide me information on parking permits`, `When is the add deadline?`, `When I must declare a major?`

## Chunking Strategy

**Chunk size:**
**Overlap:**

<!-- What about YOUR documents made you pick these numbers? Short posts and
     long sectioned guides don't want the same chunking, and "800 seemed
     reasonable" earns nothing. Point at something you noticed when you read
     the documents in Milestone 1.

     If you changed your mind partway through, say so and say why. That's worth
     more than pretending you got it right first time.

     Milestone 3. -->

Chunk size: 400 characters Overlap: 80 characters (used only when a paragraph exceeds 400 characters)

The campus_life corpus is made up of 88 documents, 27,908 characters, about 317 characters per document

## Sample Chunks

<!-- Five chunks, pasted as text. Label each one and name the file it came from
     AND the function that produced it — the grader checks your code against
     what you claim here.

     `python app.py chunks -n 5` prints all three for you. Copy them straight
     across.

     Milestone 3. -->

**Chunk 1** — source: `admin_declaring_a_major.txt` — produced by: `chunker.py::split_documents`

```
On the declaring a major
You declare at the end of your second semester
```

**Chunk 2** — source: `course_cs_210_exams.txt` — produced by: `chunker.py::split_documents`
```
CS 210 Data Structures — assessment
Two midterms and a final
Midterms are curved
The final is not.
```

**Chunk 3** — source: `admin_pass_fail_option.txt` — produced by: `chunker.py::split_documents`
```
On the pass/fail option
Any course outside your major can be taken pass/fail
```

**Chunk 4** — source: `admin_study_abroad.txt` — produced by: `chunker.py::split_documents`

```
On the study abroad
Applications open in October for the following academic year
The financial aid package travels with you,
```

**Chunk 5** — source: `dining_halden_hall.txt` — produced by: `chunker.py::split_documents`

```
Halden Hall
soup rotation
Hours are 7:30am to 7:00pm weekdays
```

## Sample Answer

<!-- One complete question and answer, pasted as text, with the source line
     visible. Milestone 4. -->

**Question:**
What is the study abroad application deadline and process?

**Answer:**

```
  (best distance 0.361, cutoff 0.6)
Direct use of automatic function calling (AFC) in Models.generate_content is not recommended. Instead, we recommend to use AFC in Chat.send_message. Similarly, direct use of AFC in Models.generate_content_stream is not recommended. Instead, we recommend to use AFC in Chat.send_message_stream.

Based on the provided documents, applications for study abroad open in October for the following academic year, but no further details about the application deadline or process are mentioned. 

Source: `admin_study_abroad.txt`

Sources retrieved: admin_add_drop_deadline.txt, admin_graduation_requirements.txt, admin_study_abroad.txt, advising_registration.txt, course_engl_205.txt

1 model calls this session, 558 tokens (512 in, 46 out)

```

**My relevance cutoff:**

<!-- The number you set in config.py, and how you got there.

     You ran five questions your corpus covers and the five in OUT_OF_SCOPE
     that it clearly doesn't, and wrote down the best distance for each. What
     did those two groups look like? Where was the gap? Put the actual numbers
     here — the table below wants all ten rows.

     Milestone 4. -->

| Question | In corpus? | Best distance |
|---|---|---|
| Provide me information on parking permits | Yes |  0.538 |
| When is the add deadline? | Yes | 0.482 |
| When I must declare a major? | Yes | 0.311 |
| What is the study abroad application deadline and process? | Yes | 0.357 |
| What was the on-time arrival rate of United Airlines in 2025? | No |0.730 |
| Who is the president of United States? | No | 0.947 |
| Give me details on registration? | Yes | 0.566 | 0.6 |


## How I Used AI

<!-- Two specific moments. For each: what you asked for, what came back, and
     what you changed about it.

     "I asked Claude to write the chunking function from my notes. It ignored
     the overlap, so I added that myself" is the level of detail we're after.
     "I used AI to help me code" is not.

     Milestone 5. -->

**1.**
I asked AI to evaluate the chunks.

**2.**
Brainstorming and provide me ideas.

<!-- ── Stretch features ─────────────────────────────────────────────────────
     Doing one? Say so here BEFORE you start. A feature this README never
     claims earns nothing.
     ───────────────────────────────────────────────────────────────────────── -->

---

# Unit 2

<!-- These sections get ADDED to what's already above. Don't delete or rewrite
     unit 1 — the point is that someone can see what you said before you knew
     how it went. -->

## Run Log — Before

<!-- Your five criteria, three runs each. `python run_eval.py --label before`
     runs the questions, puts the OUT_OF_SCOPE ones through the gate, and
     writes it all into results/ for you. Targets come from criteria.md; the
     verdict column is your call.

     Criterion 3 is measured in one deterministic pass rather than three, so
     the same number goes in all three run columns. That's correct, not lazy.

     Milestone 1. -->

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 | 4/5  | 5/5 | 5/5 | MET |
| 2. Every answer names a source | 5 of 5 | 5/5  | 5/5 | 5/5 | MET |
| 3. Gate stops out-of-corpus questions | 4 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 4. | | | | | |
| 5. | | | | | |

<!-- Underneath, paste the REAL output for each criterion from one of your
     runs — the actual text your system produced, not a description of it.
     Name the file and function that produced it. -->
```
##"Who is the president of United States?"
  (best distance 0.947, cutoff 0.6)

I don't have enough information about that.

##"Give me details on registration?"      
  (best distance 0.566, cutoff 0.6)
Direct use of automatic function calling (AFC) in Models.generate_content is not recommended. Instead, we recommend to use AFC in Chat.send_message. Similarly, direct use of AFC in Models.generate_content_stream is not recommended. Instead, we recommend to use AFC in Chat.send_message_stream.

Based on the documents provided:

You must have an adviser hold lifted before you can register, and because advisers get very busy the week before registration opens, you should book an appointment two weeks in advance. Additionally, registration times are staggered by credit hours (similar to the housing lottery), and popular courses tend to fill up within the first two days. 

Source: *advising_registration.txt*

Sources retrieved: admin_wifi_and_accounts.txt, advising_registration.txt, course_engl_205.txt, dining_verrill_street_grill.txt, dining_verrill_street_grill_followup.txt

1 model calls this session, 697 tokens (614 in, 83 out)

## When is the add deadline?"                    
  (best distance 0.482, cutoff 0.6)
Direct use of automatic function calling (AFC) in Models.generate_content is not recommended. Instead, we recommend to use AFC in Chat.send_message. Similarly, direct use of AFC in Models.generate_content_stream is not recommended. Instead, we recommend to use AFC in Chat.send_message_stream.

You can add a course through the end of the second week (admin_add_drop_deadline.txt).

Sources retrieved: admin_add_drop_deadline.txt, admin_withdrawal_deadline.txt, advising_registration.txt, course_cs_210_workload.txt, course_cs_340_workload.txt

1 model calls this session, 543 tokens (520 in, 23 out)


##"When I must declare a major?"
  (best distance 0.311, cutoff 0.6)
Direct use of automatic function calling (AFC) in Models.generate_content is not recommended. Instead, we recommend to use AFC in Chat.send_message. Similarly, direct use of AFC in Models.generate_content_stream is not recommended. Instead, we recommend to use AFC in Chat.send_message_stream.

You declare a major at the end of your second semester, or later if you need to. 

Source: admin_declaring_a_major.txt

Sources retrieved: admin_add_drop_deadline.txt, admin_declaring_a_major.txt, admin_graduation_requirements.txt, admin_pass_fail_option.txt, admin_study_abroad.txt

1 model calls this session, 511 tokens (478 in, 33 out)

```
## Verdicts

<!-- MET or MISSED for each of the five, against the target you wrote last
     unit — not a new one. Plus a sentence on how you decided. That sentence
     matters most where it was close.

     If your target said 4 of 5 and your runs came out 4, 3, 4, that's a MISS.
     The target has to hold, not show up occasionally.

     Milestone 2. -->

| # | Criterion | Verdict | How I decided |
|---|---|---|---|
| 1 | Retrieved chunk contains the answer | MET | every run contains the answer |
| 2 | Every answer names a source | MET | every run sited at least 1 source  |
| 3 | Gate stops out-of-corpus questions | MET | always return `I don't have enough information about that.` on out-of-corpus questions |
| 4 |  |  |  |
| 5 |  |  |  |

## Diagnoses

<!-- For each miss: which stage caused it, and how. The stage alone isn't
     enough — you need the mechanism.

     Not a diagnosis: "Question 3 didn't work."
     A diagnosis:     "Question 3 asks about laundry costs. The answer is in
                       one sentence that got split across two chunks, so
                       neither chunk on its own contains it."

     The five stages: loading → chunking → embedding → retrieval → generation.

     Look for a pattern. If three misses all ask about numbers, that's one
     problem, not three.

     Missed nothing? Say so, then say honestly whether your targets were set
     low, and which one you'd tighten and to what.

     Milestone 3. -->

## The Improvement

**What I changed:**

**Why I picked it:**

<!-- Connect it to a specific diagnosis above in one sentence. If you can't,
     you picked a fix because it sounded impressive. -->

### Run Log — After

<!-- Same format, same five criteria, three runs each.
     `python run_eval.py --label after` -->

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 |  |  |  |  |
| 2. Every answer names a source | 5 of 5 |  |  |  |  |
| 3. Gate stops out-of-corpus questions | 4 of 5 |  |  |  |  |
| 4. | | | | | |
| 5. | | | | | |

**Did it help?**

<!-- Say plainly whether it did, and how you know. If it made things worse,
     say that — a change that backfired, honestly reported, earns full credit
     and is more interesting than one that worked. What matters is that you can
     tell.

     Milestone 4. -->

## What's Still Broken

<!-- For each criterion still missed after your fix: what you'd do about it,
     and why you stopped where you did.

     "I ran out of time" is fine if it's true. Pretending nothing is left is
     not.

     Milestone 5. -->

## What I'd Do Differently

<!-- Knowing what you know now — which of your five criteria would you write
     differently, and why?

     Milestone 5. -->
