---
layout: post
title:  "Thinking of LLMs as Employees"
---

In trying to understand the impact of LLMs like GPT-3 on the way we work, it can be helpful to compare them directly to human employees on a cost-per-unit-work basis and see how they stack up.  What we’ll see is that the actual work they do is incredibly cheap compared to humans, but because of that, it’s important to look closely at any areas that may still require human effort (task setup, defect handling, etc) as that may turn out to be the limiting cost.

In this post, the focus will be on what I will call “delegated tasks” - discrete, repeatable tasks like write this text, proofread this document, etc.  Note that there is another model for AI in the workplace - “assisted tasks” where the model works directly with the human on the human’s tasks a la CoPilot.  We’ll see that these are related items on a spectrum, but the details of that will have to be another post.

Consider 3 levels of pretty normal office tasks for a pile of documents

- Basic : Sorting.  Given a pile of documents which are positive/negative customer responses, job applications, etc sort them into different piles.
- Standard: Proofreading, Entering.  Given a clearly specified document format (eg business inquiry email), format a response or check it for mistakes.
- Advanced: Writing, Analyzing.  Given a task, write a page of text, or given a page of text, summarize it for a specific usage.

We’ll use a few simple assumptions: 1 page = 500 words, 1 word = 1 token (just to keep our math simple), so 2 pages = 1K tokens

First, let’s consider what it costs to pay humans to do these jobs, putting in some arbitrary estimates on effort and pay rate.

| Document Job | Minutes Per Page | Hourly Rate | Per Per Page (Human) |
| --- | --- | --- | --- |
| Sorting | 0.5 | $15 | $0.12 |
| Proofing, Entering | 3 | $25 | $1.5 |
| Writing, Analyzing | 20 | $35 | $12 |

Now, let’s do the same computation for AI models using current OpenAI pricing  as of Jan 2023.  Here, there is more one can quibble with (is the embedding model really strong enough to sort documents, will the task require multiple calls to the model instead of just one, etc, etc).  However, the numbers are so different that we have to use cents instead of dollars to make them readable, so any small errors can be swept under that rug.

| Document Job | Model | Price Per Page (AI) |
| --- | --- | --- |
| Sorting | Ada (Embeddings) | 0.02 c |
| Proofing, Entering | Curie | 0.1 c |
| Writing, Analyzing | Davinci | 1 c |

According to this calculation, AIs cost way less than humans - 2-3 orders of magnitude less.  Looks like we human workers will all be out of work shortly.

Except that in this accounting, we left out a couple of key steps

- Setting up the task - meaning the manager comes over and tells the employee what to do
- Checking the results and fixing any defects

For these steps, let’s assume a manager who costs $50/hr who defines the task.

The task setup part is the easiest to handle - this is traditional fixed vs variable cost like you see in writing software.   If the manager needs to spend 1 hour setting up the prompts for the LLM but the LLM is (nearly) free after that, then given the manager’s higher rate, the breakeven point for using the LLM is around 1-2 hours of human worker time.  So one-offs don’t work, but jobs involving writing 10 or sorting 100 pages would qualify. 

The quality assurance and defect replacement parts are harder to skate around.  First, just in detecting an issue, if each output even needed to be read by a human being, then much of the cost savings of automation would evaporate.  Having a way of scanning the text output in a fully automated way that flags all defects is then essential to any such workflow.  It is not at all clear whether that is workable for all tasks, but if it is, fortunately the cost advantage of the LLMs is so large that running multiple models against a single page does not materially affect the argument.  Second, once a defect is detected that can’t be fixed with automation, we are forced to resort to the much more expensive human worker.  In this case, this looks less like a delegation of the task to the LLM, and more like an assisted workflow, where X% of the work is handled cheaply by the LLM and (1-X)% is handled via traditional human labor.  In this case, though, there is the additional overhead of setting up the LLM, the exception handling processes with the human workers, etc.  These are setup costs, and thus will disappear for sufficiently large volumes of repeated tasks, but will substantially raise the breakeven point from the 1-2 worker hours mark cited above, making them relevant only for truly regular tasks.

This then marks out a boundary for these delegated tasks - each new task setup must have required hours of human work, it must have an automated way of catching its mistakes, and to be effective, it must succeed with reasonably high probability on its own.  If it can’t operate that independently and needs close human supervision, then a different model - that of the assisted task - will be needed.