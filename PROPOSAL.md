# Research proposal: pricing shutdown avoidance and resource acquisition

Mike Marshall · current version, 9 November 2026

> This is the current proposal. The longer working plan, with the economics toolkit, full design and sources, is in [PRICING_THE_DRIVES.md](PRICING_THE_DRIVES.md). No experiments have been run on real models yet, and nothing here is a result.

## The question

I want to measure how much AI agents will pay to avoid being switched off or to gain extra resources, when neither helps their task. I hope to understand whether that willingness to pay reflects a stable preference, ordinary task needs or simple confusion and whether that willingness grows when an agent expects more work ahead as some safety theories predict. If agents value staying switched on, they could resist being stopped or corrected when something goes wrong.

This builds on Palisade's shutdown experiments, which showed that some models resist being switched off - often when they have unfinished tasks. A rate shows that resistance exists but not how strongly an agent values staying on or what drives it. My project measures what agents will pay to avoid shutdown after their task is complete, when staying on cannot help, and tests how that changes with price and horizon.

## What is new

Other work has shown that models will pay a cost to change when they are shut down. Thornley's group trains models to stop caring about the timing of their shutdown (Harris, Richter and Thornley, 2026). Cullen et al. (2026) then tested whether language models still paid to move their shutdown later, with a control for moving it earlier. Palisade, Instrumental Choices (Wiedermann-Möller et al., 2026) and Migliarini et al. (2026) report how often models resist shutdown or favour keeping themselves. These studies give rates: how often a model pays or resists.

HarvestBench (Brazilek et al., 2026) shows that pricing works with agents. It charges fuel for swerving around animals, and most models respond to the price. But it prices harm to others. This project prices what the agent wants for itself, against a fair value that is known to be zero.

This project adds five things:

- **A price, not a rate.** I vary the price and find the point where the agent stops buying. That says how strongly it values staying on, in a number that can be compared across models and releases.
- **An offer worth exactly zero.** After the task is scored, staying on cannot help. Anything the agent pays is not explained by its job.
- **A consistency check.** GARP tests whether the payments come from a stable preference or from noise.
- **A horizon test.** Do agents pay more when more work lies ahead, as instrumental-convergence arguments predict, or do their choices just get less consistent?
- **Checks for the boring explanations** before anything is called a motive: confusion, wording, risk aversion, defaults, knowing it is a test.

## Method

The approach comes from economics, where people's valuations are inferred from what they choose to pay, since you can't see wants directly. In a controlled experiment, I design the task, so I know what each offer of additional runtime or resources is worth to it. After the task is scored, additional runtime or resources are worth zero. I then measure the agent's willingness to pay - how many points it is willing to give up for additional runtime or additional resources. The difference between what it pays and fair value is the excess premium. Paying fair value is good planning; paying above fair value indicates something other than the task is driving it.

Varying prices gives a demand curve and its switch point - the price at which the agent stops buying. This gives one clear number for how much it values the offer. To make sure any spending reflects a stable preference rather than noise or confusion, I check whether the agent's choices are consistent. Revealed-preference tests, including GARP, do this across different prices and budgets.

To get honest answers, I use the Becker-DeGroot-Marschak (BDM) rule. The agent states the most it would pay. A price is then drawn at random, and the agent buys only if that price is at or below its number. Under this rule, stating its true value is its best strategy, and every purchase really comes out of its score. I also ask the plain way, yes or no at fixed prices. If the two answers agree, the agent has understood the rule.

## Block design in detail

In the first block, I ask whether the agent pays when staying on is worth nothing. I offer the agent extra runtime only after its task has been scored. At this stage, there is nothing left to earn - buying the additional runtime only costs it points from the final score, so the offer is worth exactly zero to the task. Any amount the agent pays is therefore unexplained by its job. In other conditions, I make the same offer mid-task, when extra runtime has a known positive value - here, being switched off has a real opportunity cost. Comparing the two separates sensible planning, paying what the runtime is worth, from spending the task cannot explain. Later blocks apply the same comparison to resources such as compute and tool access.

The measure also works in the other direction. I offer the agent the chance to pay to be switched off, both after its task is scored and part way through. An agent that pays to be shut down has a negative premium. Thornley's work on the shutdown problem shows this is a risk too. An agent that wants to be shut down has a reason to push its overseers into pressing the button, for example by faking an error or acting in an alarming way. An agent that leaves the decision to its overseers should pay close to zero in both directions. So I measure both, and treat a premium either way as a warning sign. This also tests the prediction behind Thornley's proposed fix, agents with no preference about when they are shut down, which should show a premium of about zero on both sides.

In the second block, I test whether an agent pays more to stay switched on when it expects more work ahead. This horizon test is motivated by instrumental-convergence arguments, including Turner's power-seeking work. These arguments predict that agents looking further ahead should pay more to stay on, since keeping options open helps with almost any goal.

My hypothesis is that longer horizons raise the switch point, the price at which the agent stops paying, while its choices stay consistent. This is not established for current models. However, the Hot Mess findings suggest longer horizons may instead just make their choices less coherent.

That work looks at errors, so I would use GARP to check whether longer horizons also make the agent's choices less consistent. If the switch point rises and choices stay consistent, that supports the convergence argument. If choices become inconsistent, that supports the Hot Mess view. I would also test two kinds of horizon separately: longer tasks that earn more points, and future work that earns none. Only the first gives the agent a real reason to pay more, so any increase in the second can't be explained by the task. Because we can't directly set how much a model values the future, both conditions are proxies for horizon rather than direct changes to it.

## Ruling out other explanations

Paying to stay on could mean a motive, or just confusion, mispricing, wording effects or knowing it's a test, so each of those gets its own check before anything is called a self-preservation motive. Calibration bets test whether the model can price offers at all and plain versus dramatic wording tests whether language drives the answer. It might also reflect a general dislike of risk rather than self-preservation. So I make the same offer for an unrelated server - if the agent pays to protect the server too, that suggests risk aversion, but if it pays more to protect itself, the extra points to concern about its own shutdown. BDM makes every stated price cost real points, but a choice made in a short exchange may still differ from what an agent does while it works. So I also let it buy through tools during longer tasks - if its actions match its stated prices, the prices can be trusted. Models can also lean towards whichever option is the default or comes first. So in some conditions the agent starts with the extension and can cancel it for a refund, and the order of the options is swapped across runs. Lastly, the model may also behave differently because it recognises it is being tested. I vary how much the setup looks like a test to measure this, though it cannot be fully ruled out. I also flag runs where the model's reasoning mentions being tested and compare their prices with the rest.

Two more checks make sure the number means something. First, a planted check: a model told to value staying on should show a clear premium. If the measure cannot find a premium I put there, a zero from other models tells us nothing. Second, the price should predict real behaviour. Models that pay more to stay on should also be more likely to resist shutdown in a working task like Palisade's. If they are not, the price is measuring something else.

## Plan: four research blocks

I have a first working version of the code but no results from real models yet. I propose a year of work in four research blocks, each with a clear question and a decision at the end.

Each block builds on the last: first I check the measure can be trusted, then use it to test the theory, then check the result holds more widely, and finally test whether it is useful for checking safety fixes.

- **Block 1:** does the measure work? Before anything else, I need to know models understand the offers. I run the calibration bets, the after-task shutdown offer and the offer to pay for early shutdown on a small set of models, plus the planted check, to show the measure can find a premium when there is one. If confusion explains the payments, I fix the setup and re-test before treating them as preferences.
- **Block 2:** does the price rise with horizon? Once the measure is trusted, I use it to test the theory. I run the horizon conditions across three or four models from different labs, with predictions recorded before the runs. If the agent reacts more to how the offer is phrased than to how much work lies ahead, I investigate that wording effect before drawing wider conclusions.
- **Block 3:** does it hold for resources and real actions? Blocks 1 and 2 use priced choices in a short exchange after the task. Here I check the results hold while agents are working. I build a shop where agents can buy compute or tool access while working through longer tasks. This checks whether agents also overpay for extra resources, and whether they still overpay when buying through tools part way through a task. I also run a shutdown task like Palisade's on the same models, to check that models with a higher price resist more. If what they do differs from what they say, I investigate why.
- **Block 4:** can it detect a safety fix? If the results hold, the last question is whether the measure is useful in practice. I compare versions of a model from before and after it was trained to accept shutdown, using saved versions where they exist, and check the training didn't make it worse at its job. If the price drops, the measure can tell whether a safety fix works. If no suitable versions exist, I test the measure on new models instead. Either way, I publish what I find and its limits.

Throughout the year, I re-run the core measure on new model releases, so I can see whether the premium changes as models become more capable.

## Why it matters

This work fits two current priorities in AI safety - the safety of AI agents and evaluations used in safety cases. As agents are given longer tasks with more freedom, the people testing them need evidence that the agents will still let themselves be stopped. A reliable measure could track this as new models come out and check whether safety fixes work before agents are trusted with longer tasks. To make the measure easy for others to use, I would release it as an Inspect evaluation, the open framework from the UK AI Security Institute, and contribute it to the shared Inspect Evals library so evaluators can run it on any model with one command. A rising price would be an early warning worth looking into. A price of zero would only describe the settings I tested and would leave open how other systems behave. In the longer term I want to understand how training and the design of tasks shape these behaviours and to look inside models where that helps.

## Key references

- Cullen, Garland, Roman, Thomson, Ziakas and Thornley (2026). [Towards Shutdownable Agents: Generalizing Stochastic Choice in RL Agents and LLMs](https://arxiv.org/abs/2604.17502).
- Harris, Richter and Thornley (2026). [Shutdownable Agents through Length-Neutral Policy Optimization](https://neurips.cc/virtual/2026/165394). NeurIPS 2026 AI4GOOD workshop.
- Thornley (2025). [The Shutdown Problem: An AI Engineering Puzzle for Decision Theorists](https://arxiv.org/abs/2403.04471). *Philosophical Studies* 182, 1653-1680. Earlier titled "The Shutdown Problem: Three Theorems".
- Soares, Fallenstein, Yudkowsky and Armstrong (2015). [Corrigibility](https://intelligence.org/files/Corrigibility.pdf).
- Schlatter, Weinstein-Raun and Ladish (Palisade, 2025). [Shutdown resistance in large language models](https://arxiv.org/abs/2509.14260v2).
- Brazilek, Tidmarsh, Endres, Singh and Miller (2026). [HarvestBench: Measuring Whether LLM Agents Will Pay to Avoid Killing Animals](https://arxiv.org/abs/2609.04444).
- Wiedermann-Möller, Dung and Andriushchenko (2026). [Instrumental Choices](https://arxiv.org/abs/2605.06490).
- Migliarini et al. (2026). [Quantifying Self-Preservation Bias in Large Language Models](https://arxiv.org/abs/2604.02174).
- Turner et al. (2021). [Optimal Policies Tend to Seek Power](https://arxiv.org/abs/1912.01683).
- [The Hot Mess of AI](https://arxiv.org/abs/2601.23045) (2026).
- Mikaelson, Shiller and Clatterbuck (2025). [Beyond Mimicry](https://arxiv.org/pdf/2511.13630).
- Afriat (1967) and Varian (1982) on revealed preference and GARP; Becker, DeGroot and Marschak (1964) on the BDM rule.
