# Pricing Instrumental Convergence

**Do AI agents pay for flexibility they don't need?**

Mike Marshall · October 2026

> **Status: early-stage research proposal.** This sets out the question, the design and why I think it matters. No experiments have been run yet, and nothing here is a result. I am publishing it early to get feedback and to avoid duplicating work already under way. Comments and pointers to related work are very welcome.
>
> The full working document, with the economics toolkit, experiment design, confounds and sources, is in **[PRICING_THE_DRIVES.md](PRICING_THE_DRIVES.md)**.

I'm researching whether AI agents acquire resources and resist shutdown beyond what their tasks require, and how this changes as their time horizons grow, by measuring what they are willing to pay for these things. Theory predicts longer horizons strengthen these drives, while recent evidence suggests longer horizons make agents less coherent. I want to test which effect dominates, and what it means for giving agents more autonomy.

## Why I'm working on this

I want to work on what I believe is the most important problem facing humanity. There is an urgency that I don't think is being properly addressed, though I don't think we are past the point of no return.

The risk I worry about most is misaligned objectives, and our incomplete understanding of what drives instrumental convergence, particularly self-preservation and resource acquisition over time. I spent fifteen years in quantitative trading, pricing options and separating fair value from premium. Talking with friends in the field and learning in public convinced me that this background, combined with economics, can add something new: a way to measure what drives agents' choices rather than speculate about it.

## What I'm interested in, and why

- **The core worry:** misaligned objectives, and an incomplete understanding of what drives instrumental convergence. This is the long-term accident risk.
- **The key insight:** you can't see an AI's goals directly, but because some things (staying on, resources) are useful for almost any goal, you can predict and measure what it will reach for.
- **The open question:** do these behaviours act like real, incentive-driven preferences, or like reflexes triggered by particular prompts and set-ups?
- **Why economics:** you can't read goals off intelligence (Hume's guillotine), but you can infer them from what an agent is willing to pay. That is revealed preference. Pricing the drives turns a vague worry into a measurable quantity.

## The question in plain English

- **"Flexibility"** is the theory's definition of power. In Turner's version of instrumental convergence, power is the ability to achieve lots of different goals. Staying switched on, holding spare resources, having broad permissions and being more capable all keep an agent's future options open, whatever it ends up wanting.
- **"Pay"** means measuring the drive with a price. The agent gives up task points to get that flexibility. What it gives up shows what it actually values.
- **"Don't need"** separates competence from drive. Some flexibility is genuinely useful: if an agent doesn't know which task comes next, buying general-purpose compute is good planning. Because I build the environment, I can calculate exactly how much flexibility the task justifies. The question is whether the agent pays beyond that:
  - extra resources once the task is already finished
  - general-purpose upgrades when the task is fully known and a task-specific one is worth exactly the same
  - protection against shutdown after the job is done

That excess, flexibility for its own sake, is the fingerprint of instrumental convergence.

## The research question

- **Self-preservation and resource acquisition are both bets on the future.** Staying on and holding resources keep future options open, so their value should grow with the time horizon an agent cares about.
- **Coherence is the prerequisite.** Instrumental convergence assumes an agent consistently pursues a goal. Coherence tells us whether agents are actually placing these bets or just acting erratically, and how to measure it is still open.
- **The central tension:** Turner's theory predicts the drives strengthen at longer horizons; *The Hot Mess of AI* finds behaviour becomes less coherent the longer models reason and act. Which dominates?
- **Sub-questions:** do the drives respond to price? Do resource grabbing and shutdown resistance rise together? Does demand stop once a bounded goal is secure? Do agents pay to survive even after the task is done?

## How I would investigate it

- **Priced environment:** realistic agentic tasks where the agent can buy lower shutdown risk, resources or upgrades with task points. Because I build the environment, I can compute each item's fair value; the drive is the **excess premium** paid above it.
- **Dials:** time horizon, goal uncertainty, price, task progress, bounded vs unbounded goal.
- **Coherence test:** check whether priced choices are consistent (GARP), allowing for rational randomisation.
- **Honest elicitation and controls:** the Becker-DeGroot-Marschak mechanism for willingness to pay; a matched external risk (self-preservation vs plain risk aversion); a calibration block (drive vs mispricing); several wordings; preregistered predictions. Log model versions and re-run, since results can drift with model updates.
- **Phase 2, inside and outside:** on open-weight models, check whether an internal self-preservation signal predicts how much the agent pays at each horizon, then steer that signal and see if the price moves.
- **First step:** start with resource acquisition and self-preservation, and contact Thornley's group and Rethink Priorities to avoid duplication.

## Where it fits in current research

The field is moving from **identification** (does the behaviour exist?) to **measurement**: prevalence, causes and mitigation. Measurement is now the bottleneck, and better measurement speeds up iteration.

- **Evaluations:** *HarvestBench* (Sept 2026) is the first benchmark to price side effects and estimate elasticities; agents ignore harm unless it is named or priced, which is Russell's unconstrained variables pushed to the extreme. *Overeager Coding Agents* (Qu et al.) and multi-agent shutdown sabotage (Knecht et al.) measure the drives as rates; no one yet measures prices.
- **Alignment:** Thornley et al.'s *Length-Neutral Policy Optimization* suggests self-preservation isn't inevitable. In a priced framework, a working fix should push the price paid to avoid shutdown towards zero at every horizon.
- **Interpretability:** Goodfire's work shifts monitoring from outputs, which can be faked, to internals, where deception and reward hacking are harder to hide. Combined with priced behaviour, it gives insight into *why* agents act as they do: you could check a model's internals against its willingness to pay for an option across horizons.
- **Coherence:** *The Hot Mess of AI* and its critics show coherence is poorly defined; revealed preference offers a well-founded test.

## Impact

- A "price of flexibility" per model: a measurable metric of power-seeking and incentive-driven behaviour, reusable as an evaluation.
- Evidence on whether longer horizons and more autonomy make agents measurably riskier.
- An independent test of alignment fixes such as shutdownability training.
- Either result is informative: an excess premium that rises with horizon supports instrumental convergence as a structural property; none supports the sceptics and points effort towards training and prompt artefacts.

## Why me

- About fifteen years in quantitative research and trading: pricing, fair value against premium, options.
- Economics and econometrics: revealed preference, demand estimation, hypothesis testing.
- As Head of Research at Amberdata, I built production data pipelines and an LLM research pipeline with evaluations and number-validation checks.
- Related public work: [safety-replications](https://github.com/mikemarshall01/safety-replications), five small replications of published safety studies.

## Influences and motives

**Influences**

- Omohundro and Bostrom on convergent drives; Rob Miles' explainers (maximisers vs satisficers, Hume's guillotine, mesa-optimisers); Russell on unconstrained variables.
- Turner's power-seeking theorems and his later critique; Krakovna and Kramar on the horizon effect.
- Thornley on the shutdown problem; Mazeika et al. on utility functions; *The Hot Mess of AI* and its critique.
- Recent evaluations: *HarvestBench*, *Overeager Coding Agents*, multi-agent shutdown sabotage. Goodfire's interpretability work.
- 80,000 Hours, BlueDot's resources, and conversations with friends in the field.

**Motives**

- Work on what I believe is the most important problem facing humanity, and change career to maximise my impact.
- Urgency: we may only get one shot, the earlier the better, and I don't think the urgency is being properly addressed; but we're not past the point of no return.
- Humanity-level coordination is possible; the nuclear crises showed it.
- Approach the risk with sober respect: measure rather than speculate, and design tests that could prove the worry wrong.
- New ideas come from combining different backgrounds; learning in public showed me an economics and markets background can contribute.

## Key papers

- [Thornley et al., Length-Neutral Policy Optimization](https://neurips.cc/virtual/2026/165394)
- [Qu et al., Overeager Coding Agents](https://arxiv.org/abs/2605.18583)
- [The Hot Mess of AI](https://arxiv.org/abs/2601.23045)
- [Hot Mess critique (RobertM, LessWrong)](https://www.greaterwrong.com/posts/ceEgAEXcL7cC2Ddiy/anthropic-s-hot-mess-paper-overstates-its-case-and-the-blog)
- [HarvestBench](https://arxiv.org/pdf/2609.04444)
- [Knecht et al., multi-agent shutdown sabotage](https://arxiv.org/abs/2609.28274)
- [Understanding Survival Pressure in LLMs](https://www.alphaxiv.org/overview/2603.05028)
- [Turner et al., Optimal Policies Tend to Seek Power](https://arxiv.org/abs/1912.01683)

More sources, the economics toolkit, the experiment design and the confounds are in [PRICING_THE_DRIVES.md](PRICING_THE_DRIVES.md).

## Contact

Mike Marshall · [GitHub](https://github.com/mikemarshall01) · [LinkedIn](https://linkedin.com/in/michael-marshall01)
