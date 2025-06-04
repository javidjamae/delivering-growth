# 📦 Build & Share Your Own A/B Test Simulation

This free companion guide walks you through turning the A/B Test Simulation notebook into a **high-signal portfolio project** that proves your experimentation skills, especially when you're targeting Growth Engineering or Growth Data Analyst roles.

You’ll not only copy and run the simulator, but also adapt it to a **real product scenario**, publish your results, and use it to get noticed by hiring managers.

## 🎯 What You’ll Learn

By the end of this guide, you’ll know how to:

- Reproduce a full A/B test lifecycle in Python using the [A/B Testing Simulator](https://colab.research.google.com/drive/1VM_boIlsKdrpy2artEF-Saq5hTKjhXge)
- Customize the simulation to reflect a real-world product test (e.g. landing page, onboarding, pricing)
- Analyze experiment results using confidence intervals and p-values
- Publish a professional write-up with visuals, metrics, and a teardown
- Turn this into a repeatable proof-of-work asset to help you get hired



# 🛠 Step 1: Copy and Understand the Simulator

To kick off this project, start by opening the original simulation notebook:

👉 Open the [A/B Testing Simulator](https://colab.research.google.com/drive/1VM_boIlsKdrpy2artEF-Saq5hTKjhXge) in Google Colab

This is more than just a code sample.  

It's a working blueprint for how modern Growth teams build, bucket, track, and analyze experiments.

Take the time to explore it fully. You’ll use these mental models in every real experiment you build.


## ✅ What You Need to Do

1. **Make a Copy in Your Google Drive**  
   - In Colab, go to `File → Save a Copy in Drive`.  
   - Rename it something like `ab-test-simulator-yourname`.

2. **Run the Entire Notebook**  
   - Click `Runtime → Run All` to simulate 10,000 user sessions.
   - Scroll through the output—especially the `summary_df` and the final confidence interval plots at the bottom.

3. **Explore the Code Structure**  
   The notebook is broken into 5 core blocks. Study each one:

   - `feature_flag_service`:  
     Implements **deterministic bucketing** using hash functions. This mimics real flagging tools like LaunchDarkly or homegrown flag logic.

   - `analytics_service`:  
     Tracks events in a flat event log and computes **conversion metrics** post-hoc. Mimics tools like Snowplow, Segment, or Amplitude.

   - `browser`:  
     Simulates user behavior by triggering exposure and probabilistic conversion. Think of this as a fake frontend calling your analytics SDK.

   - `run_simulation()`:  
     Runs the whole lifecycle for N users, calling the flag logic and tracking events. This is your test harness.

   - **Experiment Analysis Section**:  
     Runs a **Z-test** and plots:
     - Cumulative conversion rate
     - P-value vs. cumulative exposures
     - Confidence intervals with a visible MDE band

4. **Understand the Lifecycle**  
   The simulation reflects how real A/B tests work in production:
   - Users are **bucketed into variants** using a consistent hashing function.
   - Exposure events are tracked separately from conversions.
   - Conversions are joined back to exposures for attribution (not stored with variant in the conversion).
   - Analysis is done **after the fact**, on the flat event log.

5. **Take Notes**  
   Jot down:
   - How assignment works
   - How events are tracked
   - What assumptions are baked into the simulation (e.g., stable traffic, known MDE)
   - What parts of this mirror the systems you’ve seen at past companies


## 💡 Want to Go Deeper?

If this feels fast or unfamiliar, you're not alone.

The simulator is intentionally production-faithful, but if you need more background, join the [Delivering Growth](https://www.skool.com/delivering-growth/about) community.

Inside, you’ll get full access to:

- **Foundations of Experimentation**: Learn assignment, tracking, and analysis from scratch
- **Growth Engineering Fundamentals**: Build your own experiment infra step by step
- **Experiment Design & Analysis**: Learn stats, significance testing, and common failure modes

We walk through these concepts with real code, real metrics, and live support.


# 🧪 Step 2: Customize the Scenario

Now that you’ve run and explored the simulation, it’s time to make it yours.

Pick a **real company or product** you’d love to work for. Find one that actively experiments—most product-led B2B or consumer platforms do.

Then look at their **job postings**, blog posts, product UI, or teardown videos and identify:

- What surfaces are they working on? (e.g. onboarding, pricing, trial, upsell)
- What might their Growth or Product team be testing?
- What metrics would matter for that test?

Use that to inspire your custom simulation.

## Examples

- **Notion**: Simulate an onboarding flow test where you skip the workspace name step.
- **Spotify**: Simulate a variant that promotes Premium earlier in the free user journey.
- **Gusto**: Simulate a pricing test that highlights annual billing over monthly.
- **Duolingo**: Simulate a landing page CTA test that emphasizes streak protection.

Update these variables in the code to match your scenario:

```python
CONVERSION_RATES = {
    "control": 0.030,  # baseline
    "variant": 0.036   # simulate a 0.6% lift (20% relative improvement)
}

TOTAL_SAMPLES = 10000  # Or adjust based on your traffic assumptions
```

## 🔧 What Changes and What Stays the Same

- ✅ **What changes**: Your inputs—conversion rates, number of users, and the narrative you wrap around the simulation.
- ✅ **What stays the same**: The core code. The logic for flag assignment, tracking, and analysis remains reusable across projects.
- ✅ **What you customize**: The markdown text, variable names, and final summary of the test. This should all reflect the specific product scenario you modeled.

## 🧑‍💼 Why This Works for Job Hunting

This becomes a **targeted proof-of-work project**:

- You’ve studied the company’s product and crafted a plausible test.
- You’ve simulated what a real experiment might look like there.
- You can use this as a high-signal artifact to include in outreach messages, LinkedIn posts, or interviews.

You’re not just showing that you can code—you’re showing that you think like someone who already works on their Growth or Product team.



# 📊 Step 3: Run and Analyze the Experiment

Once you’ve customized your simulation, it’s time to re-run the notebook and study the results like a real Growth team would.

## ✅ What to Do

1. **Rerun the entire notebook** (`Runtime → Run all`)  
   This will simulate all user sessions, apply your custom conversion rates, and generate exposure and conversion events.

2. **Scroll through the outputs** and focus on:
   - `summary_df`: Final exposures, conversions, and conversion rates per variant.
   - Plots at the bottom:
     - **Conversion Rate Over Time**
     - **P-Value Over Time**
     - **Confidence Interval Band** vs. your MDE line

3. **Export the visualizations**
   - Screenshot or right-click and save all 3 charts as images.
   - Note the exact numeric values printed in the summary block below the plots.
   - Save the outputs for your write-up and presentation.


## 📈 What to Look For

Take notes on the following:

- **Conversion Rate**  
  Is the variant outperforming the control? By how much? Even if the difference is small, does it match your simulated effect size?

- **P-Value Trend**  
  Does the p-value fluctuate heavily early on, and then stabilize? This mirrors what you'd see in real experiments as sample size increases.

- **Confidence Interval**  
  What’s the width of the 95% CI? Is it tight and conclusive, or wide and inconclusive? Does it contain 0? (If yes, the result is not statistically significant.)

- **Statistical Significance**  
  Does the p-value drop below 0.05? If so, the variant is statistically significant. If not, what might that mean for decision-making?


## 🔍 Interpret Like a Real Growth Team

Use these prompts to generate insights, just like you'd do in a real post-experiment readout:

- What does this tell you about user behavior in the variant?
- Would you recommend shipping the change? Why or why not?
- Would you rerun the experiment? Increase sample size? Adjust MDE?
- How confident are you that the observed effect is real, not noise?


## 🛠 Pro Tip: Treat This Like an Internal Debrief

When Growth teams analyze experiments, they aren’t just checking p-values—they’re making decisions. Your write-up should reflect this level of thinking.

Include:
- A short paragraph summarizing the results
- The numerical summary (conversion rates, diff, p-value, CI)
- Screenshots of the charts
- Your recommendation: ship, hold, iterate



# 🖥 Step 4: Publish Your Project Breakdown

Now that you’ve run and interpreted your experiment, it’s time to **turn your work into a published artifact**, something you can share in outreach, interviews, and your portfolio.

Publishing is what transforms this from “a side project” into **visible signal** that hiring teams notice.

## ✅ Choose a Publishing Format

You can use:

- A **Notion page** (easy, beautiful formatting, private or public)
- A **LinkedIn post** (good for visibility and commentary)
- A **Blog post or GitHub README** (great for permanence and SEO)
- A **PDF portfolio deck** (useful for outreach or interviews)

Pick whatever is fastest for you, but **you must publish something.**


## 📝 Project Breakdown Template

Use this as your outline. Each section should be short, sharp, and scannable.

1. **Title**  
   - Keep it tight and descriptive.  
   Example:  
   **Simulating a Pricing Page A/B Test Inspired by Gusto**

2. **Context**  
   - What company inspired this?  
   - What feature or flow did you simulate?  
   - Why is this test plausible for their Growth team?

3. **Setup**  
   - What changes did you make in the simulator?  
   - What were your assumptions about conversion rates and sample size?  
   - (Optional) Link to the job description that inspired the scenario.

4. **Results**  
   - Drop in your final `summary_df`  
   - Include screenshots of the 3 plots: conversion rate, p-value, and confidence interval  
   - Call out key metrics (conversion rate lift, p-value, confidence interval)

5. **Takeaways**  
   - Would this test be conclusive?  
   - Would you ship the variant? Rerun the test? Adjust your design?

6. **Reflection**  
   - What did you learn about experimentation systems?  
   - How does this mirror what real Growth Engineers do?  
   - What would you do next?

7. **Supporting Materials**  
   - ✅ A link to your Colab notebook (make sure sharing is set to “Anyone with the link can view”)  
   - ✅ Or export as a PDF or static HTML and upload to Notion or GitHub  
   - ✅ Your name, role, and a brief 1-liner at the bottom (like a project signature)


## 🧠 Bonus Ideas for Growth Engineers

To really stand out, include Growth Engineering-specific insights in your breakdown:

- **Diagram the Experiment Architecture**  
  Use a diagram to show how flagging, tracking, and analysis components work together. Optionally compare to a real-world system you've seen or built.

- **Map Simulator Components to Real Tools**  

  | Simulator Component     | Real System Equivalent       |
  |-------------------------|------------------------------|
  | `feature_flag_service`  | LaunchDarkly / Split.io      |
  | `analytics_service`     | Amplitude / Snowplow         |
  | `browser`               | Web client w/ Segment SDK    |
  | `event_log`             | Data warehouse / event table |
  | `Z-test analysis`       | In-house stats engine / Looker |

- **Describe Testing Strategies & Failure Modes**  
  - What happens if events are out of order?
  - How would you QA bucketing logic or conversion attribution?
  - What metrics would you monitor for assignment integrity?

- **Show Scalability or Multi-Test Scenarios**  
  - How would you scale this architecture to millions of users?
  - What changes would be needed to support concurrent experiments or ramping?

These extras showcase **system design thinking** — and that’s what separates a good Growth Engineer from a great one.

## 📊 Bonus Ideas for Data Analysts

To stand out as a Growth Analyst or Experimentation-focused Data Analyst, enrich your breakdown with deeper interpretation and statistical thinking:

- **Explain the Statistical Assumptions**  
  Show that you understand what the Z-test is doing under the hood:
  - Why is a Z-test appropriate here?
  - What assumptions are we making about sample independence, variance, or distribution?
  - How might results change with lower traffic or smaller MDEs?

- **Critique the Attribution Model**  
  - Why is conversion attributed via `device_id` joins instead of storing variant in conversion events?
  - What would break in a multi-touch or cross-device scenario?
  - How would you handle late conversions or attribution windows?

- **Interpret Confidence Intervals Visually**  
  Use the plotted CI band to:
  - Explain practical significance vs. statistical significance
  - Point out overlapping intervals and what they imply
  - Call out if the CI contains 0 and what that means for decision-making

- **Propose Additional Cuts or Segments**  
  - What if you sliced results by user type, geography, or acquisition channel?
  - How might heterogeneity in treatment effect show up in a real dataset?

- **Compare to Real Analytics Workflows**  

  | Simulation Component   | Real Analytics Workflow               |
  |------------------------|---------------------------------------|
  | Flat `event_log`       | Snowplow / Segment → Data Warehouse   |
  | Variant Join Logic     | dbt models for exposure attribution   |
  | Analysis Notebook      | Jupyter / Hex / Mode SQL + Python     |
  | Charts & Commentary    | Dashboard walkthrough / Slack recap   |

- **Describe How You’d Present Results**  
  - What 2–3 visuals would go into a real experiment readout?
  - How would you communicate tradeoffs and uncertainty to PMs or execs?

These additions show that you’re not just reporting numbers — you’re generating insights, questioning assumptions, and thinking like a decision partner.


## 💬 Sample Closing

> This project helped me simulate a real A/B test lifecycle, from deterministic flag assignment to post-hoc analysis.  
> It mirrors what modern Growth teams at companies like [Company] do when evaluating new product ideas.  
> I'm actively looking for roles where I can apply this kind of experimentation infrastructure thinking as a Growth Engineer.



# 🚀 Step 5: Share It to Build Signal

Now that your project is published, it’s time to put it in front of the people who matter.

This is where everything compounds—posting your work publicly builds **credibility, connection, and momentum**.


## 🧵 Suggested LinkedIn Post Template

> Just simulated a full A/B testing pipeline—from flag assignment to post-hoc analysis—with Python and a custom-built experiment simulator.
>
> This mirrors how real Growth teams implement and measure experiments, including deterministic bucketing, clean event logs, and p-value tracking over time.
>
> I modeled this after a pricing test that could be run at [company you admire]. Here’s the write-up + Colab notebook if you're curious:  
> [Notion/blog link]
>
> Would love feedback from other engineers, PMs, and analysts doing experimentation work!

✅ Tag relevant people at the company  
✅ Use hashtags like `#growthengineering`, `#experimentation`, `#abtesting`, `#productgrowth`  
✅ Mention the company you modeled the test after


## 📣 How to Maximize Visibility

1. **Tag Me [Javid Jamae](https://www.linkedin.com/in/jamae)**  
   I’ll reshare it so more people in Growth see it. You’ll get eyes from my network of hiring managers, engineers, and PMs. Connect with [Javid Jamae on LinkedIn](https://www.linkedin.com/in/jamae) and DM me.

2. **Post Inside the [Careers in Growth](https://www.skool.com/delivering-growth-free/about) Community**  
   Share your write-up in our community. We’ll help boost engagement, offer feedback, and tag others who might work at or know people from your target company.

3. **Tag People You Know at the Company**  
   If you have mutuals or 2nd-degree connections, tag them. Or just comment on recent posts from people on that team before you post—so you’re top of mind when they see your tag.

4. **Ask for Feedback and Conversations**  
   In the comments or your post CTA, ask:
   - “Would love thoughts or critique from anyone working on experimentation at [company].”
   - “Know who the hiring manager is for this role? Would love to get this in front of them.”
   - “Happy to DM the full write-up if you're curious how I broke down the system.”

5. **Engage With Everyone Who Comments**  
   Like, reply, and send connection requests with a thank-you note.  
   Use this momentum to grow your network and open up warm intros.

6. **Message the Recruiter or Hiring Manager**  
   If the job post lists a recruiter or you find one on LinkedIn, send them:
   - A link to your public write-up
   - A short intro that says:  
     “I modeled a real A/B test your team might run. Thought this might show how I think.”


This is how you go from invisible to undeniable.  
Proof-of-work + smart publishing + strategic outreach = traction.

Let your project do the talking—and then start the conversations that get you in the door.



# 🧰 Bonus: Make It Repeatable

Once you've done it once, this becomes a **modular simulator**:

- Swap in different MDEs, sample sizes, or segment logic
- Run simulated SRMs or flaky event logs to show debugging skills
- Create different versions for each role/company you're targeting

This becomes your personal “experiment engine” to practice, teach, or share in interviews.



# 🧠 Summary

This isn’t just a simulator. It’s a **signal engine**.

By simulating a full experiment pipeline, customizing it for a real-world use case, and publishing your thinking, you’re doing the exact work Growth teams need—**not just talking about it**.

When you go beyond basic analysis and include engineering-level system thinking — architecture, tooling equivalents, QA strategies — you prove you’re not just experiment-literate, you’re experiment-capable.

It’s proof that you can ship fast, think clearly, and execute like someone already on the team.

---

Want help turning your simulator into a standout project?
Join the [Careers in Growth](https://www.skool.com/delivering-growth-free/about) community and get feedback, examples, and next-step coaching.

Let’s build proof—not resumes.