<![CDATA[# How Interviewers Actually Evaluate You

> **This is the rubric.** Knowing it changes how you prepare.

---

## The Evaluation Dimensions

After every interview, the interviewer fills out a scorecard. Here's what it looks like:

### 1. Problem Solving (Weight: 30%)

| Score | Description |
|---|---|
| ⭐⭐⭐⭐⭐ | Asks clarifying questions, breaks problem into sub-tasks, considers edge cases, proposes multiple approaches and discusses tradeoffs |
| ⭐⭐⭐ | Solves the problem but takes the first approach without exploring alternatives |
| ⭐ | Jumps into coding without understanding the problem, misses key requirements |

**What to do:** Always start by restating the problem. Ask 2-3 clarifying questions. Propose 2 approaches before coding.

### 2. Technical Depth (Weight: 25%)

| Score | Description |
|---|---|
| ⭐⭐⭐⭐⭐ | Explains concepts deeply with correct intuition, connects to real-world applications, knows tradeoffs |
| ⭐⭐⭐ | Correctly describes algorithms but lacks depth or can't explain WHY |
| ⭐ | Surface-level: recites definitions without understanding |

**What to do:** For every concept, know: (1) what it is, (2) why it works, (3) when to use it, (4) what are the alternatives.

### 3. Coding Quality (Weight: 20%)

| Score | Description |
|---|---|
| ⭐⭐⭐⭐⭐ | Clean, modular code. Good variable names. Handles edge cases. Tests the solution |
| ⭐⭐⭐ | Working code but messy structure or missing edge cases |
| ⭐ | Code doesn't run, or copy-pasted without understanding |

### 4. Communication (Weight: 15%)

| Score | Description |
|---|---|
| ⭐⭐⭐⭐⭐ | Thinks aloud clearly, explains decisions, listens to hints, summarizes at the end |
| ⭐⭐⭐ | Can explain what they're doing but not why |
| ⭐ | Silent, or talks too much without substance |

**What to do:** Narrate your thinking. "I'm choosing Random Forest because the data is tabular and I need feature importances. If accuracy isn't good enough, I'll try XGBoost."

### 5. ML Intuition (Weight: 10%)

| Score | Description |
|---|---|
| ⭐⭐⭐⭐⭐ | Demonstrates real-world awareness: data leakage, class imbalance, production constraints |
| ⭐⭐⭐ | Knows theory but hasn't applied it to real problems |
| ⭐ | No awareness of practical challenges |

---

## Red Flags That Kill Candidacies

1. **Can't explain bias-variance** — this is ML 101
2. **Uses accuracy on imbalanced data** — shows lack of practical experience
3. **Doesn't ask clarifying questions** — jumps straight to code
4. **Can't justify model choice** — "I just tried it"
5. **Ignores production concerns** — "I'd just use the best model"
6. **Over-engineers** — proposes transformers for a simple tabular classification
7. **Memorized answers** — can't handle follow-up questions

## What Strong Candidates Do

1. **Start with a baseline** — "I'd begin with logistic regression, then evaluate if we need more complexity"
2. **Think about data first** — "Before choosing a model, I need to understand the data distribution, class balance, and potential leakage"
3. **Quantify impact** — "This reduced churn by 8%, saving ~$200K annually"
4. **Connect theory to practice** — "I used L2 regularization because several features were correlated"
5. **Acknowledge uncertainty** — "I'm not sure about this, but my intuition is..."

---

## Mock Interview Plan

> A structured approach to practice until you're interview-ready.

### Phase 1: Self-Practice (Weeks 20–21)

| Week | Activity | Time |
|------|----------|------|
| 20 | Record yourself answering 10 theory questions from [`interview-questions.md`](interview-questions.md) | 3 hrs |
| 21 | Solve 10 ML coding problems from [`coding-questions.md`](../06-ml-coding/coding-questions.md) with timer | 3 hrs |

**How to self-practice:**
1. Set a timer for each question (2 min for theory, 25 min for coding)
2. Write your answer on paper or a whiteboard
3. Record yourself explaining
4. Review and identify gaps

### Phase 2: Peer Practice (Weeks 22–23)

| Week | Activity | Sessions |
|------|----------|----------|
| 22 | 2 mock interviews with peers (ML theory + ML coding) | 2 sessions |
| 23 | 2 mock interviews (system design + behavioral) | 2 sessions |

**Where to find peers:**
- Ask classmates or friends in ML
- Join ML interview prep Discord servers
- Use Pramp or Interviewing.io (free)

### Phase 3: Real Interviews (Week 24+)

- Start applying to 5–10 positions per week
- Treat real interviews as practice
- Ask for feedback after each interview

---

## Practice Resources

| Resource | What It Offers |
|----------|---------------|
| [Pramp](https://www.pramp.com/) | Free mock interviews |
| [Interviewing.io](https://interviewing.io/) | Free mock interviews with engineers |
| [LeetCode](https://leetcode.com/) | Coding practice |
| [HackerRank](https://www.hackerrank.com/) | SQL and ML coding |

---

## The Night Before

1. **Review your projects** — be ready to discuss any of your 4 projects in detail
2. **Quick review** — 5 key concepts you don't want to forget
3. **Rest** — 8 hours of sleep
4. **Logistics** — Test your camera, mic, internet
5. **Backup plan** — Have a phone number in case video fails

---

## The Interview Day

1. **30 min before:** Light stretch, water, bathroom
2. **10 min before:** Join the link, test audio/video
3. **During:** Think aloud, ask questions, stay calm
4. **At the end:** Ask thoughtful questions about the team
]]>
