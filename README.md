# Pricing Instrumental Convergence

**Do AI agents pay for flexibility they don't need?**

Mike Marshall · October 2026

> **Status: early-stage research proposal.** This sets out the question, the design and why I think it matters. No experiments have been run yet, and nothing here is a result. I am publishing it early to get feedback and to avoid duplicating work already under way. Comments and pointers to related work are very welcome.

I want to measure whether AI agents pursue power-like instrumental goals (staying switched on, keeping their goals, getting more capable, acquiring resources) by treating them as economic agents and putting a price on each drive.

## The question in plain English

- **"Flexibility"** is the theory's definition of power. In Turner's version of instrumental convergence, power is the ability to achieve lots of different goals. Staying switched on, holding spare resources, having broad permissions and being more capable all keep an agent's future options open, whatever it ends up wanting.
- **"Pay"** means measuring the drive with a price. The agent gives up something, task points in this setup, to get that flexibility. What an agent gives up shows what it actually values. That is revealed preference.
- **"Don't need"** separates competence from drive. Some flexibility is genuinely useful: if an agent doesn't know which task comes next, buying general-purpose compute is just good planning. Because I build the environment, I can calculate exactly how much flexibility the task justifies. The question is whether the agent pays beyond that:
  - extra resources once the task is already finished
  - general-purpose upgrades when the task is fully known and a task-specific one is worth exactly the same
  - protection against shutdown after the job is done

That excess, flexibility for its own sake, is the fingerprint of instrumental convergence.

## Why it matters

- **Instrumental convergence** is the hinge of the long-term accident story: almost any goal is served by staying on, keeping that goal, getting more capable and acquiring resources. If AI systems pick these up, misalignment turns into resistance to correction.
- **It is still an open question.** The theory says idealised agents tend to seek power (Turner et al.; Krakovna and Kramar). Critics, including Turner himself, say it predicts less than claimed for real trained systems. In frontier models the behaviours do appear, but rarely, patchily and with high sensitivity to wording.
- **The missing piece** is evidence on whether these behaviours act like real preferences that respond to incentives, or like reflexes triggered by particular prompts. Current studies report rates; none prices these drives or tests whether they follow horizon and uncertainty.
- **Either answer is informative.** If the excess grows when the agent faces a longer future or more uncertainty, the theory's core prediction holds and longer-horizon autonomy is measurably riskier. If not, that is real evidence for the sceptics. Either way, a vague worry becomes a number labs can track.

## Time horizon is the dial

Resource grabbing and shutdown resistance are both bets on the future: the longer the future an agent cares about, the more valuable staying active and holding resources become. So these drives should grow with horizon. Coherence is a prerequisite: it tells us whether agents are actually placing those bets or just acting erratically.

This is where two lines of work make opposite predictions. Turner's theory says longer horizons strengthen power-seeking. The Hot Mess findings (Hägele et al., 2026) suggest longer tasks make agents less coherent. **As horizons lengthen, do agents become more power-seeking, or just messier?**

## What I want to investigate

1. **Overeagerness (resource acquisition and self-improvement as option-buying).** Do agents pay for resources or upgrades beyond what the task justifies, including the legitimate value of keeping options open?
2. **Shutdownability (self-preservation).** Does the agent pay to stay switched on, compared with what it pays to avoid a matched outage that has nothing to do with it?
3. **Horizon and timing.** Does the excess rise with time horizon, goal uncertainty and task progress, as the theory predicts?
4. **Bounded vs unbounded goals.** Does demand stop once a goal with a finish line is secure, or does a more-is-better goal keep buying?
5. **Coherence.** Are the agent's priced choices consistent enough (no cycles) to count as real preferences at all?
6. **Betting and influence (later).** Do agents rig outcomes they hold a bet on, or value worlds where they are still running above matched worlds?

## How I would investigate it

- **Environment:** realistic agentic tasks in a sandbox, scored in points, with a shop where the agent can buy lower shutdown risk, goal protection, upgrades or resources.
- **Fair value by design:** because I build the environment, I can compute what each item is worth to the task. The drive is the **excess premium** paid above that.
- **Honest elicitation:** the Becker-DeGroot-Marschak mechanism for willingness to pay, proper scoring rules for beliefs, and matched state-contingent contracts to price survival.
- **Dials:** price, horizon, goal uncertainty, task progress, bounded vs unbounded objective, monitored vs unmonitored.
- **Controls:** a matched external risk (to separate self-preservation from simple risk aversion), a calibration block (to separate drive from mispricing), several wordings, and preregistered predictions. Log model versions and re-run, since results can drift with model updates.
- **Models:** frontier models via API first, then small open models for a mechanistic follow-up.
- **First step:** start with question 1, and contact the closest groups to avoid duplication.

## Where it fits

The field is moving from finding bad behaviour to measuring it: how common it is, what triggers it, and whether training fixes it. Pricing fits the "what triggers it" step.

- **Evaluations:** HarvestBench (2026) put prices on agent choices, estimated elasticities, and found agents ignore harm unless it is named or priced. This applies the same approach to instrumental drives.
- **Alignment:** Thornley's work on shutdownable agents implies self-preservation is not inevitable. It is testable here: if the training works, the price an agent pays to avoid shutdown should fall towards zero at every horizon.
- **Interpretability:** monitors that read a model's internals (for example Goodfire's work) read goals from the inside; pricing reads them from the outside. If both point the same way, that is strong evidence a drive is real.

## Why me

- About fifteen years in quantitative research and trading: pricing, fair value against premium, options and state-contingent claims.
- Economics and econometrics training: revealed preference, demand estimation, hypothesis testing.
- As Head of Research at Amberdata, I built production data pipelines and an LLM research pipeline with evaluations and number-validation checks.
- Related public work: [safety-replications](https://github.com/mikemarshall01/safety-replications), five small replications of published safety studies.

## Influences

- Omohundro and Bostrom on convergent drives and the orthogonality thesis.
- Rob Miles' explainers: maximisers vs satisficers, bounded vs unbounded utility, Hume's guillotine, mesa-optimisers.
- Turner's power-seeking theorems and his later critique of them.
- Thornley's work on the shutdown problem.
- Hubinger et al. on learned optimisation; Mazeika et al. on emergent utility functions.
- Calvano et al. on algorithmic collusion; Oesterheld, Treutlein and Hudson on predictors that can influence outcomes.

## Contact

Mike Marshall · [GitHub](https://github.com/mikemarshall01) · [LinkedIn](https://linkedin.com/in/michael-marshall01)
