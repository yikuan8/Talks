# AI for Scarce Healthcare Resource Allocation

*A 9-minute TED-style talk — Mason AI Day*

---

## Outline

| # | Slide | Time |
|---|---|---|
| 1 | Hook — Who gets the ventilator? | ~50s |
| 2 | Different states. Different rules. Different outcomes. | ~75s |
| 3 | Why so different? And is any of them fair? | ~60s |
| 4 | Reframing triage as an AI problem | ~50s |
| 5 | Teaching an AI to make the call (and why it's hard) | ~75s |
| 6 | An AI that sees everyone at once | ~55s |
| 7 | Building fairness into the AI | ~50s |
| 8 | Results & take home | ~95s |

**Total ≈ 9m 10s**

---

## Slide 1 — Hook

**Slide content:**

- Who gets the ventilator?
  - COVID-19. Scarcity. A decision no one wanted to make.
- AI for Scarce Healthcare Resource Allocation — Mason AI Day
- [Picture: COVID-era headline — "Hospitals running out of ventilators" or "NY pleads for ventilators"]
- [Picture: overwhelmed ICU during COVID peak]

**Script:**

*(Pause. Let the title land.)*

Take yourself back to 2020. Two patients are wheeled into the ICU in the same minute. Both can't breathe. There is one ventilator left.

This wasn't hypothetical. Hospitals across New York, Italy, Wuhan literally ran out.

And the math is brutal. Without a ventilator, a patient in respiratory failure almost certainly dies. With one, they have a real chance. So whoever the doctor picks gets that chance. Whoever they don't, probably doesn't.

That's the hardest decision in medicine.

*Transition: "And nobody agreed on how to make it."*

---

## Slide 2 — Different states. Different rules. Different outcomes.

**Slide content:**

- No national standard. Only **26 of 50 states** had a public guideline (May 2020).
- Three different approaches:
  - **New York** — SOFA score only (current severity)
  - **Maryland** — SOFA + age + comorbidities
  - **Pennsylvania** — SOFA + priority for healthcare workers
- Same patient. Different state. Different outcome.
- [Picture: U.S. map shaded by protocol type, or JAMA headline "Variation in Ventilator Allocation Guidelines by US State"]

**Script:**

Most people don't realize this — during COVID, there was no national rule for who gets a ventilator. As of May 2020, only 26 states had even published a guideline. The other 24 left it to individual hospitals.

And the 26 that did have guidelines disagreed sharply.

In New York, the rule was SOFA — purely how sick you are right now. In Maryland, it was SOFA *plus* age *plus* comorbidities — favoring younger, healthier patients. In Pennsylvania, similar to Maryland, plus priority for healthcare workers.

Same patient, two hospitals 50 miles apart, different rulebook — different outcome.

*Transition: "If everyone has a different answer, some must be wrong. So which one is best? And is any of them fair?"*

---

## Slide 3 — Why so different? And is any of them fair?

**Slide content:**

- **15 of the 26 states use SOFA** — the closest thing to a U.S. standard.
- But SOFA has a problem:
  - Only moderately accurate.
  - Assigns **higher severity scores to Black patients** → lower priority → fewer ventilators.
- Two questions for the rest of this talk:
  - Can we do **better**?
  - Can we do **fair**?
- [Picture: headline on SOFA bias / racial disparities in ventilator allocation during COVID]

**Script:**

The most common choice was SOFA — 15 of those 26 states built their protocol around it. The closest thing we have to a national standard.

But SOFA has two problems.

It's only moderately accurate at predicting who actually survives.

And — this is the part that should bother all of us — multiple studies during COVID found SOFA assigns higher severity scores to Black patients than to White patients in comparable condition. In SOFA's logic, a higher score pushes you *down* the priority list. So Black patients were systematically less likely to receive a ventilator than White patients with the same medical need.

This isn't about bad doctors. It's about a mathematical tool that was never designed with fairness in mind, quietly producing unequal outcomes at scale.

So for the rest of this talk: can we build a protocol that saves *more* lives — and doesn't carry this hidden bias?

*Transition: "To do that, we have to stop thinking about triage as a scoring problem."*

---

## Slide 4 — Reframing triage as an AI problem

**Slide content:**

- Current protocols = **static scoring functions**. Same formula. Every patient. Every day.
- But triage is really a **sequence of decisions over time**:
  - Is the next outbreak coming?
  - Is today's patient getting better or worse?
  - How many ventilators will I have next week?
- This is what **reinforcement learning** was built for.

**Script:**

Every protocol we just talked about is a static scoring function. Plug in numbers, get a score, rank. The formula never changes. It doesn't know who else is in the hospital. It doesn't know what's coming tomorrow.

But real triage isn't static. It's a sequence of decisions in a moving storm. Is the next surge about to hit? Is yesterday's patient getting better? If I use my last ventilator now, what happens at 2am?

None of that fits in a single number calculated at admission.

This kind of problem — sequential decisions in a changing environment, where today shapes tomorrow — is exactly what reinforcement learning was built for.

*Transition: "Let me show you how that works."*

---

## Slide 5 — Teaching an AI to make the call (and why it's hard)

**Slide content:**

- Just like training a self-driving car:
  - Good choice → **reward**. Bad choice → **penalty**.
  - Do it millions of times → the AI learns to drive.
- Now point it at the ICU:
  - Patient survives → reward. Patient dies → penalty.
  - The AI learns to allocate.
- **But there's a twist** — every decision affects every other.
  - A car decides for itself. The AI here decides for *everyone in the ICU at once*.

**Script:**

Most of you have heard of self-driving cars. How do you teach a car to drive itself? You don't write down every rule. You let the AI try. It stays in its lane — reward. It rear-ends the car in front — big penalty. Run the loop millions of times, and a blank slate becomes a driver.

Now point that exact same idea at an ICU. Show the AI every patient, every vital sign, every ventilator. Let it make a call. A patient survives — reward. A patient dies — penalty. Do it thousands of times. The AI stops being a blank slate and becomes a triage agent.

But here's the twist that makes this *harder* than self-driving.

A car only decides for itself. The AI in an ICU has to decide for *everyone at once*. If I give this ventilator to patient A, it's not available for patient B. If I use my last one today, I don't have it tomorrow when someone sicker shows up. Every choice ripples through every other.

That means the AI can't just rank patients one at a time — that's exactly what SOFA does, and that's why SOFA fails. It has to see the *whole ICU* as one connected picture.

*Transition: "So how do you build something that does that?"*

---

## Slide 6 — An AI that sees everyone at once

**Slide content:**

- The solution: a **Transformer**.
  - Same family of AI that powers ChatGPT.
  - Built to look at many things at once and weigh how they relate.
- Feed it the whole ICU → it weighs every patient against every other.
- Output: today's allocation — who gets a ventilator.

**Script:**

The answer comes from a surprising place — the same family of AI that powers ChatGPT. A model called a Transformer.

Underneath the chat interface, a Transformer is really just a machine that's very good at one thing: looking at many pieces of information at once, and figuring out how they relate. For ChatGPT, those pieces are words.

Take that same architecture and feed it patients instead of words. Every patient in the ICU goes in at once — every vital, every indicator, every ventilator already in use. The Transformer weighs each patient against every other, figures out who's in danger, who will benefit, and how today's decision ripples through the rest.

What comes out isn't a ranking or a score. It's a decision — for today — about who gets a ventilator. A learned policy that sees the whole picture.

*Transition: "But there's still one more ingredient."*

---

## Slide 7 — Building fairness into the AI

**Slide content:**

- Reward survival alone → the AI inherits SOFA's bias.
- So add a **second reward signal**:
  - Equal allocation across racial groups → reward.
  - Unequal allocation → penalty.
- Fairness isn't a filter applied at the end.
- It's part of what the AI is trying to **win**.

**Script:**

Here's the most important ingredient.

If we only reward the AI for saving lives, we're back to the SOFA problem — it might be great at survival overall while quietly underserving one group, because the training data already carries that bias.

So we change what the AI is trying to win. We keep the survival reward. But we add a second signal: if ventilators are distributed evenly across racial groups, reward. If one group is systematically passed over, penalty.

Now fairness isn't a filter we apply at the end. It's baked into the goal. The AI literally cannot win unless it's both effective *and* equitable.

Small change in the math. Big change in philosophy. Most AI systems treat fairness as something you bolt on afterward. This one treats fairness as part of the definition of success.

*Transition: "So — did it work?"*

---

## Slide 8 — Results & take home

**Slide content:**

- Tested on **~12,000 ICU admissions** (2020–2023), simulated severe shortage.
- **More lives saved.**
  - SOFA: 81% · Multi-principle: 82% · **AI agent: 85%** → ~400 more lives per 10,000 patients.
- **Smaller racial gap.**
  - SOFA: 5.5-point gap (White 79.1% vs. Black 73.6%)
  - AI agent: **2.9-point gap** — cut nearly in half.
- Survival up. Fairness up. **In the same direction.**
- **AI, designed properly, can save lives *and* mitigate disparities.**
- One ventilator. Two people. We can do better.
- **Thank you.**
- [Picture: bar chart — survival rates across protocols + grouped bar chart by race]

**Script:**

The AI was tested on twelve thousand real ICU admissions over three years of the pandemic, simulating a severe shortage.

First — survival. A lottery saves 75%. SOFA saves 81%. Multi-principle saves 82%. The AI agent saves 85%. Four points doesn't sound like much — until you scale to ten thousand patients in a real shortage. That's four hundred people who'd be alive under this protocol who'd be dead under New York's rule.

Second — fairness. Under SOFA, the gap between the best-served group and the worst-served — between White patients at 79.1% and Black patients at 73.6% — was 5.5 points. Under the AI, that same gap is 2.9 points. Almost half. The disparity didn't vanish. But it shrank dramatically.

And here's what I want this room to remember.

We are told constantly in AI that there is a trade-off. Fairness costs accuracy. Equity comes at someone's expense.

That trade-off did not happen here. Survival went up. Fairness went up. Both, at the same time. Because the old protocols weren't just unfair — they were also bad at their core job. When you design a system to care about both, it turns out you can improve both.

So the take-home message — **AI, designed properly, can save lives *and* mitigate disparities.** Not one or the other. Both. Ventilators today, and tomorrow ICU beds, organs, vaccines, dialysis. All of them governed today by rulebooks that haven't been re-examined in years.

*(Pause.)*

I started with two patients and one ventilator. A decision no one wanted to make. We can't make scarcity go away. But when that moment comes again — and it will — we can choose with better tools than the ones we had in 2020.

One ventilator. Two people. We can do better than we have been.

Thank you.

---
