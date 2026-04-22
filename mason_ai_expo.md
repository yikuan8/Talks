# AI for Scarce Healthcare Resource Allocation

*A 10-minute TED-style talk — Mason AI Day*

---

## Outline

| # | Slide | Time |
|---|---|---|
| 1 | Hook — Who gets the ventilator? | ~50s |
| 2 | Every state had a different rulebook | ~55s |
| 3 | Why so different? And is any of them fair? | ~60s |
| 4 | Reframing triage as an AI problem | ~55s |
| 5 | Teaching an AI agent to make the call | ~60s |
| 6 | The hard part: everyone is connected | ~50s |
| 7 | An AI that sees everyone at once | ~60s |
| 8 | Building fairness into the AI | ~55s |
| 9 | Result 1: More lives saved | ~55s |
| 10 | Result 2: The gap disappears | ~65s |
| 11 | Take home | ~45s |

**Total ≈ 10m 10s**

---

## Slide 1 — Hook

**Slide content:**

- Who gets the ventilator?
  - COVID-19. Scarcity. A decision no one wanted to make.
- AI for Scarce Healthcare Resource Allocation — Mason AI Day
- [Picture: COVID-era U.S. news screenshot — e.g., NYT/CNN/AP headline like "Hospitals running out of ventilators" or "NY pleads for ventilators," March–April 2020]
- [Picture: news still or photo of overwhelmed ICU during COVID peak]

**Script:**

Pause before speaking. Let the title land.

Let me take you back to 2020. Two patients are wheeled into the ICU in the same minute. Both are in respiratory failure. Both need a ventilator to breathe. And there is only one ventilator left in the hospital.

This wasn't a thought experiment. During the peak of COVID, this was happening across the country — New York, Italy, Wuhan. Hospitals were literally running out of ventilators. The supply ran out.

And the math of this decision is brutal. A patient in respiratory failure who doesn't get a ventilator almost certainly dies. A patient who does get one has a real chance to survive — not a guarantee, but a chance. So whoever the doctor picks gets that chance. Whoever they don't pick, probably doesn't.

That is the hardest decision in medicine.

*Transition: "The first thing to understand is that nobody agreed on how to make this decision."*

---

## Slide 2 — Every state had a different rulebook

**Slide content:**

- No national standard. Only 26 of 50 U.S. states had a public guideline (May 2020).
- Three very different approaches:
  - **New York** — SOFA score only (current clinical severity)
  - **Maryland** — SOFA + age + comorbidities (favors younger, healthier)
  - **Pennsylvania** — SOFA + priority for healthcare workers
- Adjacent states, same patient, different outcome.
- [Picture: U.S. map shaded by protocol type]
- [Picture: screenshot of JAMA Network Open headline — "Variation in Ventilator Allocation Guidelines by US State" (Piscitello et al., 2020)]

**Script:**

Here's something most people don't realize. During COVID, there was no national standard for who gets a ventilator. When researchers looked in May 2020, only 26 of the 50 states had even published a guideline. The other 24 — nothing public. Individual hospitals figured it out on their own.

And the 26 that did have guidelines disagreed sharply on what mattered.

In New York, the rule was SOFA — purely clinical severity. How sick are you right now. Age doesn't matter. Pre-existing conditions don't matter. Just your current vitals.

Cross into Maryland, and the rule changes. They used a multi-principle protocol — SOFA plus your age plus your comorbidities. A younger, healthier patient gets priority over an older, sicker one, even with identical current vitals.

Pennsylvania was similar — but also gave priority to healthcare workers.

Think about what this means. Two patients in identical condition, in hospitals 50 miles apart, across a state line — one lives, one dies, because of which rulebook the hospital happened to be using. Same country. Same disease. Different outcomes based on geography.

*Transition: "So if every state has a different answer — which one is right? And is any of them actually fair?"*

---

## Slide 3 — Why so different? And is any of them fair?

**Slide content:**

- If states disagree this much, some must be wrong.
- **15 of the 26 states use SOFA** — the most common score.
- But SOFA has a problem:
  - Only moderately accurate.
  - Assigns **higher severity scores to Black patients** → lower priority → fewer ventilators.
- Two questions:
  - Can we do **better**?
  - Can we do **fair**?
- [Picture: screenshot of a headline on SOFA bias / racial disparities in ventilator allocation during COVID (Ashana et al. 2021 or Bhavani et al. 2021)]

**Script:**

If every state has a different answer to the same life-and-death question, at least some of those answers must be wrong. So the obvious question is — which one is best? And can we do better than all of them?

The most common choice across the country was SOFA. Out of the 26 states with public guidelines, 15 of them built their protocol around the SOFA score. It's the closest thing we have to a U.S. standard.

But SOFA has a problem. Two problems, actually.

First, it's only moderately accurate at predicting who actually survives on a ventilator. It's a rough tool, not a precise one.

Second, and this is the part that should bother all of us — multiple studies during COVID found that SOFA systematically assigns higher severity scores to Black patients than to White patients in comparable clinical condition. And in the SOFA world, a higher severity score pushes you down the priority list. So in hospital after hospital, Black patients were less likely to receive a ventilator than White patients with the same medical need.

This isn't a story about bad doctors. It's a story about a mathematical tool that was never designed with fairness in mind, quietly producing unequal outcomes at scale.

So for the rest of this talk, I want to ask two questions. Can we build a protocol that saves more lives than any of these state rules? And can we build one that doesn't carry this hidden bias?

*Transition: "To answer both questions, we have to stop thinking about triage as a scoring problem — and start thinking about it as something else."*

---

## Slide 4 — Reframing triage as an AI problem

**Slide content:**

- Current protocols = **static scoring functions**.
  - Same formula. Every patient. Every day.
- But triage is really a **sequence of decisions over time**:
  - Is the next outbreak coming?
  - Is today's patient getting better or worse?
  - How many ventilators will I still have next week?
- This is the kind of problem AI was built for — specifically, **reinforcement learning (RL)**.
  - An agent that learns to make sequential decisions.
  - Optimizes long-term outcomes, not just the next step.

**Script:**

Here's the shift I want to make. Every protocol we've talked about — SOFA, multi-principle, all of them — is a static scoring function. You plug in a patient's numbers, you get a score, you rank. The formula never changes. It doesn't know who else is in the hospital. It doesn't know how many ventilators are left. And it has no idea what's coming tomorrow.

But real triage isn't static. It's a sequence of decisions made over days and weeks, in the middle of a moving storm. Is the next outbreak about to hit? Is the patient I ventilated yesterday getting better, or getting worse? If I use my last ventilator on this patient today, what happens when five more show up at 2am?

Every one of those questions matters. And none of them fit into a single number calculated at admission.

This structure — making a sequence of decisions in a changing environment, where today's choice shapes tomorrow's options — is exactly what reinforcement learning was built for. It's the same family of AI that learned to play chess, to play Go, to control robots. An agent takes an action, the environment changes, it sees the result, and over many trials it learns which actions lead to the best long-term outcome.

So the question becomes: what if we stopped asking doctors to follow a static rulebook, and instead trained an AI agent to learn the best allocation policy directly?

*Transition: "That's exactly the question this work set out to answer."*

---

## Slide 5 — Teaching an AI agent to make the call

**Slide content:**

- Same idea as training a self-driving car:
  - Good choice → **reward**.
  - Bad choice → **penalty**.
  - Do it millions of times → the AI learns to drive.
- Now apply it to the ICU:
  - Patient survives → reward.
  - Patient dies → penalty.
  - Do it thousands of times → the AI learns to allocate.
- No formula. A learned policy.

**Script:**

You might not have heard of reinforcement learning before, but let me show you how it works with an example most of us have at least heard of — self-driving cars.

How do you teach a car to drive itself? You don't write down every rule. You let the AI try. It stays in its lane — reward. It drifts across the line — penalty. It brakes smoothly at a red light — reward. It rear-ends the car in front — big penalty. You run this loop millions of times, in simulation and in the real world, and slowly the AI stops being a blank slate and starts being a driver. Not because someone told it what to do. Because it learned, through reward and penalty, which choices lead to good outcomes.

Now take that exact same idea — and point it at an ICU.

You show the AI every patient, every vital sign, every ventilator in use. You let it make a call: who gets a ventilator today, who doesn't. And then you grade it. A patient survives — reward. A patient dies — penalty. A ventilator used wastefully — small penalty. Tomorrow, new patients, new decisions, new feedback.

You do this thousands of times, over thousands of simulated days. And slowly, the AI stops being a blank slate and starts being a triage agent. It isn't following a formula. It's developed a policy — a learned sense of which decisions, across the full arc of a crisis, save the most lives.

*Transition: "Okay — but there's one detail about this problem that makes it a lot harder than self-driving."*

---

## Slide 6 — The hard part: everyone is connected

**Slide content:**

- A self-driving car decides for **one** car.
- An ICU must decide for **many patients at once**.
- And every decision affects every other:
  - Ventilator to Patient A → not available for Patient B.
  - Hold back today → maybe save two tomorrow.
- The AI can't rank patients one by one.
  - It has to see the whole ICU at once.

**Script:**

Here's the detail that makes this problem genuinely hard — harder than self-driving, in one important way.

A self-driving car is making a decision for one car. Itself. When it picks a lane, it isn't also picking a lane for every other car on the highway.

An ICU is different. Every ventilator decision is entangled with every other. If I give this ventilator to patient A, it's not available for patient B. If I use my last one today, I don't have it tomorrow when someone sicker walks through the door. Every choice ripples.

So the AI can't just look at patients one at a time and rank them. That's what the old protocols did — that's what SOFA does — and that's exactly why they fail. A score calculated in isolation can't see the trade-offs.

The AI has to look at the *whole* ICU at once. All the patients. All their conditions. All the ventilators in play. And reason about them together, as one connected picture.

And that turns out to be the key technical challenge — and the key technical insight — of this work.

*Transition: "So how do you build an AI that can do that?"*

---

## Slide 7 — An AI that sees everyone at once

**Slide content:**

- The solution: a **Transformer**.
  - Same family of AI that powers ChatGPT.
  - Built to look at many things at once and understand how they relate.
- Feed it the whole ICU → every patient, every vital, every ventilator.
- It weighs everyone against everyone else.
- Output: today's allocation — who gets a ventilator.

**Script:**

The answer comes from a surprising place. The same family of AI that powers ChatGPT — a model called a Transformer.

You might think of ChatGPT as a text tool, but underneath, a Transformer is really just a machine that's very good at one thing: looking at many pieces of information at the same time, and figuring out how they relate to each other. In ChatGPT's case, those pieces are words. Every word gets compared against every other word, and the model decides which ones matter most for what comes next.

Now take that same architecture, and instead of feeding it words, feed it patients. Every patient in the ICU is one input. Every vital sign, every indicator of how sick they are, every ventilator already in use — all of it goes in at once. And the Transformer does what it's designed to do: it weighs each patient against every other patient, figures out who's in the most danger, who will benefit most, and how today's decision ripples through the rest of the ICU.

What comes out is an allocation. Not a ranking. Not a score. A decision — for today — about who gets a ventilator.

No formula hand-written by a committee. A learned policy that sees the whole picture.

*Transition: "And there's one more ingredient. Because saving lives isn't the only thing we care about."*

---

## Slide 8 — Building fairness into the AI

**Slide content:**

- Saving lives is not the only goal.
- Remember the SOFA problem: Black patients got fewer ventilators.
- So add a **second reward signal**:
  - Survival → reward.
  - Equal allocation across racial groups → reward.
  - Unequal allocation → penalty.
- Fairness is no longer an afterthought.
- It's part of what the AI is trying to win.

**Script:**

Here's the last ingredient — and for me, the most important one.

If we only reward the AI for saving lives, we're back to the same problem we had with SOFA. The system might get very good at survival overall, while still quietly underserving one group of patients. Because the numbers in the training data already carry that bias.

So we do something different. We change what the AI is trying to win.

We keep the original reward — a patient survives, that's a reward. A patient dies, that's a penalty. But we add a second signal on top. If the ventilators are being distributed evenly across racial groups — reward. If one group is being systematically passed over — penalty.

Now fairness isn't something we check at the end and hope for the best. It's not a filter we apply after the AI has made its decisions. It's baked directly into the goal. The agent literally cannot "win" unless it is both effective and equitable — at the same time.

This is a small change in the math. But it's a big change in philosophy. Most AI systems treat fairness as a constraint we bolt on afterwards. This one treats fairness as part of the definition of success.

*Transition: "So we built it. Did it actually work?"*

---

## Slide 9 — Result 1: More lives saved

**Slide content:**

- Tested on **real patient data** — ~12,000 ICU admissions, 2020–2023.
- Simulated a severe ventilator shortage (about half the patients who need one get one).
- Survival rates:
  - Lottery: **75%**
  - SOFA (New York's rule): **81%**
  - Multi-principle (Maryland, PA): **82%**
  - AI agent: **85%**
- A 4-point gap sounds small.
- On 10,000 patients, that's **400 lives**.
- [Picture: bar chart of survival rates across protocols, AI bar highlighted]

**Script:**

The AI was tested on real patient data — about twelve thousand ICU admissions collected over three years of the pandemic. Then they simulated what would have happened under a severe shortage, where only about half the patients who needed a ventilator could actually get one.

Here's what came out.

A lottery — pure chance — saves about 75% of patients. New York's rule, SOFA, saves 81%. Maryland and Pennsylvania's multi-principle protocol saves 82%. Those are the state-of-the-art protocols actually used in American hospitals during COVID.

The AI agent saves 85%.

Four points. You might think, four points isn't much. Let me translate.

Scale that out to ten thousand patients in a severe shortage, and that four-point gap is four hundred people. Four hundred people who would be dead under New York's rule, who would be alive under this one.

That is not a rounding error. That is a small town.

And remember — the AI wasn't told any medical rules. It wasn't handed SOFA or any other formula. It just watched thousands of patient trajectories, got rewarded for saving lives, and learned a better policy on its own.

*Transition: "But remember — saving lives was only half of what we asked the AI to do."*

---

## Slide 10 — Result 2: The gap disappears

**Slide content:**

- **SOFA** — largest racial gap: **5.5 points** (White 79.1% vs. Black 73.6%).
- **AI agent** — gap cut nearly in half: **2.9 points**.
- And overall survival went **up**, not down.
- Fairness and effectiveness moved **in the same direction**.
- [Picture: grouped bar chart — allocation rate by race, SOFA vs. AI agent]

**Script:**

Here is, for me, the most important slide in this talk.

Under SOFA — the protocol used most widely in the United States — who was the most likely to get a ventilator? White patients, at 79.1%. Who was the least likely? Black patients, at 73.6%. A gap of 5.5 points between the group at the top and the group at the bottom. That is the disparity researchers have been documenting for years. That is the bias hiding inside a mathematical formula.

Now look at the AI agent, with fairness baked into its reward.

The highest group is still White, at 82.8%. The lowest is still Black, at 79.9%. But the gap between them is 2.9 points. Almost half of what it was. And every group in between — Asian, Hispanic — sits comfortably inside that range.

The disparity didn't vanish completely. We should be honest about that. But the gap between the best-served and the worst-served group was cut nearly in half.

And here is the part I want everyone in this room to take home.

In AI, we are told constantly that there is a trade-off. That you can have performance, or you can have fairness, but not both. Make the model fairer, accuracy goes down. Make it more accurate, some group pays the price.

That trade-off did not happen here.

Overall survival went up, not down. Fairness went up, not down. Both numbers moved in the same direction, at the same time. Because the old protocols weren't just unfair — they were also bad at their core job. When you design the system to care about both dimensions at once, it turns out you can improve both at once. The so-called trade-off was a feature of bad math. Not a law of nature.

*Transition: "So what does this mean beyond ventilators?"*

---

## Slide 11 — Take home

**Slide content:**

- **AI, designed properly, can save lives *and* mitigate disparities.**
- Ventilators today. Tomorrow: ICU beds, organs, vaccines, dialysis.
- Fairness and effectiveness are **not** opposites.
- One ventilator. Two people. We can do better.
- **Thank you.**

**Script:**

*(Slow down. Let the pace drop.)*

So here is the take-home message I want to leave you with.

**AI, designed properly, can save lives and mitigate disparities — at the same time.**

Not one or the other. Both.

Ventilators were the example today, but this is not only about ventilators. The same kind of AI — one that learns from outcomes, one that sees the whole picture, one that is rewarded for fairness as well as performance — can help us allocate ICU beds, donated organs, vaccines, dialysis slots, emergency care. Every one of these is a scarce resource being handed out, every day, by a rulebook that probably hasn't been re-examined in years.

And the lesson underneath all of it is this. We are told, constantly, that fairness is a cost. That equity comes at the expense of performance. That to help the people at the bottom, we have to accept less for everyone else.

Today I've tried to show you that is not a law of nature. It is a consequence of how we design our systems. When we build AI that cares about both outcomes and equity from the very beginning, we don't have to choose between them.

*(Pause.)*

I started with two patients and one ventilator. A decision no one wanted to make. We can't make scarcity go away. Pandemics will come again. Disasters will strain hospitals again. But when that moment comes, we can choose with better tools than the ones we had in 2020.

One ventilator. Two people. We can do better than we have been.

Thank you.

---

## Q&A — stuff to have in your pocket

- **"Is this already deployed in hospitals?"**
  No — it's research, not a clinical system. Real deployment requires prospective trials, ethics review, and regulatory approval.

- **"Couldn't AI make this worse? We've seen AI carry bias."**
  Absolutely — if you train it on biased data with no fairness objective, it will amplify that bias. That's exactly the point of this work. *How* you design it matters. Fairness has to be in the reward from day one.

- **"Who decides what 'fair' means?"**
  Ethicists, clinicians, patients, affected communities. Not engineers alone. This approach actually makes that conversation *easier* — because fairness becomes something you write down and negotiate, not something hidden inside a formula.

- **"Does the AI replace doctors?"**
  No. The doctor still decides whether a patient needs a ventilator at all. The AI only helps with the harder question that comes *after* that — when multiple patients need one and there aren't enough to go around.

- **"What about the tiny remaining gap?"**
  Honest answer: a 2.9-point gap is much better than 5.5, but it isn't zero. This is a proof of concept, not a finished product. More work is needed before anyone should trust it with a real ICU.
