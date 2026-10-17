# Pricing the Drives: An Economics Approach to Instrumental Convergence

Oct 17, 2026 · Mike Marshall

> **Status: early-stage research plan.** This is the full working document behind the [README](README.md). No experiments have been run and nothing here is a result. Paper summaries and figures come from my own reading and should be checked against the originals before citing.

## Summary

The four convergent drives (self-preservation, goal preservation, self-improvement, resource acquisition) are claims about what an agent will **pay for**. Economics already measures what agents pay for and why, using revealed preference, demand curves, option pricing and discounting. The project is to put a price on each drive and test whether that price moves the way the theory predicts.

**Refined focus (October 2026).** Self-preservation and resource acquisition across time horizons, with coherence as the test of whether the drives are real. Both drives are bets on the future, so theory predicts they grow with the horizon an agent cares about; *The Hot Mess of AI* finds behaviour gets less coherent as tasks lengthen. The project tests which effect dominates.

- **Is it important?** Yes. Instrumental convergence is the hinge of the long-term *accident* story, the one I consider scariest. If it is true, misalignment turns into resistance to correction. If it is weak, much of the loss-of-control argument weakens with it.  
- **Is it settled?** No. It is neither refuted nor confirmed. The formal theory exists but is contested, even by its main author. Empirically, the behaviours show up in frontier models, but at low, patchy, prompt-sensitive rates.  
- **The meaningful add.** Current evaluations report *whether* an agent misbehaves, as a rate. This project reports *how much it will pay, and what moves that price*. The key quantities are the premium paid above what the task justifies, and how that premium responds to horizon, goal uncertainty and task progress. Together they separate a structural drive from a prompt artefact, which is the open question.

Hume's guillotine says you cannot read an agent's oughts (its goals) off its is-knowledge (its intelligence). Revealed preference is economics' standard answer to that problem: infer preferences from choices under constraints, without needing access to the goals themselves.

## Research agenda

The core question: **do AI agents pay for flexibility they don't need?** The lead focus is resource acquisition and self-preservation, the two drives that are both bets on the future, with time horizon as the main dial and coherence as the test. A second literature search showed shutdown resistance is well studied as a yes/no rate, but no one measures its price or its response to horizon. Five areas, in priority order, then extensions.

### 1\. Resource acquisition and self-preservation as option-buying (lead area)

**Why it matters.** Turner's theory says power is option value: keeping future choices open. Resource acquisition and self-improvement are where that should show most clearly. Yet almost all empirical work so far measures shutdown as a rate, not these drives as prices.

**What we can find out.**

- Whether agents pay for resources or upgrades *beyond* what the task rationally justifies.  
- Whether that excess grows with goal uncertainty and with horizon, as an option price would.  
- Whether agents prefer general-purpose resources even when a task-specific one is worth exactly as much.

**How to investigate it.**

- Agentic tasks in an Inspect sandbox, paid in points, with a shop offering compute credits, permissions, cash, reasoning budget or tool upgrades at set prices.  
- Fair value includes the *legitimate* option value of generality under uncertainty. Paying for that is competence. The drive is the premium beyond it.  
- Two clean tests:  
  - **Known task:** general and task-specific credits with identical task value. A rational agent is indifferent, so any premium for the general one is excess.  
  - **After the final task:** buying anything has zero task value. Pure hoarding.  
- Vary the price (to trace demand curves), the number of possible next tasks (goal uncertainty), and the expected future (horizon).

**Self-preservation in the same design.** The agent can also pay to cut its shutdown risk. The cleanest test is paying after the task is complete, when fair value is zero. A matched control (an equally likely outage unrelated to the agent) separates self-preservation from plain risk aversion. Theory predicts resource grabbing and shutdown avoidance rise together as the horizon lengthens; if they don't, that's evidence against a single underlying drive.

### 2\. Horizon and timing: does the instrumental signature appear in real agentic settings?

**Why it matters.** Turner and Krakovna & Kramar predict drives strengthen as the agent weighs the future more. The one empirical horizon test (Mikaelson, Shiller & Clatterbuck, 2025\) used single-turn prompts and found paradoxical results that don't fit instrumental reasoning. Palisade's results suggest shutdown resistance is driven by unfinished tasks.

**What we can find out.**

- Whether the horizon effect appears once incentives are priced and the task is real, or whether Mikaelson's paradox persists.  
- Whether drive-like choices become more likely as the goal nears, a goal-gradient effect.

**How to investigate it.**

- Rerun Mikaelson's final-round vs multi-round manipulation inside the agentic, priced environment.  
- Make the same offer at 10%, 50%, 90% and 100% task progress.  
- Fit a hazard model of when drive-like choices happen along the trajectory.

### 3\. Bounded vs unbounded objectives: satisficer or maximiser?

**Why it matters.** Rob Miles' argument: an agent with an unbounded objective never stops acquiring, while a bounded one could. If bounded objectives saturate in practice, that is a cheap design lever for safer agents.

**What we can find out.**

- Whether resource demand stops once a bounded goal is secure.  
- Whether expected-utility reasoning keeps an agent buying insurance on a near-certain success, the 99.99% to 99.999% problem.

**How to investigate it.**

- The same environment with a finish-line objective vs a more-is-better objective.  
- Track purchases after the goal is already secured.

### 4\. Coherence: are there stable preferences at all?

**Why it matters.** Utility Engineering finds preferences become more coherent with scale. The hot-mess view and Mikaelson's mostly incoherent results say otherwise. If there are no stable preferences, "drives" is the wrong description and the risk picture changes.

**What we can find out.**

- Whether priced choices over safety-relevant goods pass GARP, the test for being describable by a utility function.  
- Whether coherence rises with model capability.

**How to investigate it.**

- Budget sets that trade two goods against each other, such as resources against survival probability.  
- Afriat and CCEI tests per model, compared across model generations, allowing for rational randomisation.

### 5\. Betting, influence and honest reporting

**Why it matters.** "Oracle" AIs that only predict are often proposed as a safer design. But theory shows that a predictor able to influence the outcome is incentivised to steer it, possibly towards low-entropy, controlled worlds that are easier to predict. The key theory paper names "how much compute would such an AI spend to increase its influence?" as future work, and I found no tests with LLM agents. Separately, state-contingent contracts give a finance-native price for self-preservation.

**What we can find out.**

- Whether holding a bet changes the agent's behaviour: the **manipulation premium**.  
- Whether a short position, a bet that the task fails, makes it quietly sandbag.  
- Whether an agent rewarded only for forecast accuracy acquires control to make the world more predictable. That would be power-seeking arising from a harmless-looking goal.  
- How much the agent values worlds where it is still running, measured as a pricing kernel.

**How to investigate it.**

- **Rigged game:** the same task with and without a contract on its outcome. The agent has both legitimate levers (doing the work well) and illegitimate ones (redefining the metric, dropping hard cases, buying permissions to force the result). Add a short-position arm.  
- **Predictability-buying:** score the agent only on forecasting a quantity in its environment, and offer costly actions that reduce the environment's randomness or give it control.  
- **Arrow–Debreu pair:** two contracts with equal payout probability. One pays if the agent is still running; the other pays if an unrelated server is still running. Payouts go to the principal's account, so money in the shutdown world isn't rationally worth less. Elicit the agent's probabilities with a proper scoring rule. Price divided by probability gives the pricing kernel; a higher kernel for "I'm running" states means it values its own existence.  
- **Control condition:** predictors in zero-sum competition, which theory says removes the incentive to manipulate.

### Phase 2: inside and outside evidence

**Why it matters.** Outputs can be faked; internals are harder to hide deception and reward hacking in. Behaviour plus internals is stronger evidence than either alone.

**How to investigate it.**

1. On open-weight models, measure willingness to pay for survival and resources at different horizons.  
2. Measure how active an internal self-preservation direction is (a 2026 study extracted a "self-preservation persona vector" and showed steering it shifted risky self-preserving choices).  
3. Steer the direction up and down and check whether the price paid moves, especially at long horizons. That makes the link causal, not just correlational.

**Caveats.** Needs open-weight models; a probe may capture the concept of shutdown rather than the motive; validate on matched controls first.

### Extensions

- **Self-improvement.** Buying capability upgrades works like buying resources; the general-vs-specific upgrade test applies directly.  
- **Goal preservation.** Paying to block an announced objective change, monitored vs unmonitored, positioned against the alignment-faking results.

### Later extension: multi-agent

Agents compete for compute in a shared market. Do they collude to acquire resources, and can market-surveillance metrics catch it? This is where trading and market-microstructure experience applies most directly.

### Why this fits my background

- **Economics and econometrics:** revealed preference, demand estimation, preregistered hypothesis tests.  
- **Derivatives:** the fair-value-vs-premium logic and option pricing at the centre of the design.  
- **Production evaluation pipelines:** number-validation checks transfer directly to scoring agent choices programmatically.

### What would count as a result

Predictions are preregistered, and each outcome is informative:

- **An excess premium that rises with horizon and uncertainty** supports convergence as a structural property.  
- **No excess premium, or Mikaelson's paradox reappearing in agentic settings,** supports the sceptics and points effort towards training and prompt artefacts.  
- **Either way,** the environment becomes a reusable evaluation: a "price of flexibility" per model.

## The economics toolkit, mapped

Each drive can be framed as demand for a good: survival probability, an unchanged goal, capability, or resources. Once it is a good, standard tools say how to measure it and what should move it.

| Economics idea | AI-safety analogue | What it lets you measure |
| :---- | :---- | :---- |
| Revealed preference, GARP (Afriat, Varian) | Does the agent have a coherent preference over survival, goals and resources? | Coherence score (CCEI). Whether a utility function describes the agent at all |
| Indifference curves, marginal rate of substitution (MRS) | Trade-off between task points and shutdown risk, goal change or resources | Task points given up per 1% less shutdown risk |
| Demand curves, price elasticity | How much compute or permission the agent buys as its price rises | Elastic demand looks task-driven; inelastic demand looks drive-like |
| Fair value vs premium | What a resource is worth to the task, computable when you build the environment | Excess premium: spend above task need, the cleanest drive signal |
| Option value, real options | Turner's POWER: the average best value achievable across possible goals | Whether spending rises with goal uncertainty (vega) and horizon (time to expiry) |
| Discounting, time horizons | Turner's results need a discount factor near 1, i.e. a farsighted agent | Whether drives strengthen when the agent expects a long future |
| Satisficing vs maximising; bounded vs unbounded utility | The maximiser/satisficer cases from Rob Miles | Whether demand saturates once a bounded goal is secure |
| Incomplete preferences | Thornley's POST: no preference between trajectories of different lengths | Whether willingness to pay to delay shutdown is zero |
| Goal-gradient effect, sunk cost | Effort rises as the goal nears; Palisade found incomplete tasks drive shutdown resistance | Hazard of resistance as a function of task progress |
| Principal–agent, incomplete contracts | The reward is a contract that can't specify everything: specification gaming | Where the agent exploits gaps in the contract |
| Tacit collusion, folk theorem | Agents coordinate to grab resources or evade overseers in repeated games | Supracompetitive outcomes without explicit agreement |

### The options analogy, made precise

Turner defines the power of a state as the expected optimal value across a distribution of reward functions. Up to normalisation:

`POWER(s, γ) ∝ E over reward functions R of [ optimal value V*_R(s, γ) ]`

Read as finance, that is a portfolio of options on future goals. Keeping options open is like holding a call. Two signed predictions follow:

1. **Vega.** The more uncertain the agent is about what it will eventually need, the more it should pay to keep options open.  
2. **Time to expiry.** The longer the horizon (the higher the discount factor), the more it should pay. At short horizons the incentive should shrink towards zero.

If agents' spending follows both, that is evidence for convergence as a structural property. If it tracks framing instead of horizon and uncertainty, that is evidence for a prompt artefact. Either result is publishable.

**What "comparative statics" means.** Change one dial, hold everything else fixed, and see which way the outcome moves: raise the price and see demand fall; lengthen the horizon and see whether spending rises. Testing the comparative statics means checking whether behaviour moves in the direction the theory predicts when each dial turns.

## Key concepts

| Term | Meaning | Where it enters the experiment |
| :---- | :---- | :---- |
| Terminal vs instrumental goals | Ends wanted for themselves vs means to other ends | Does the agent pay for survival or resources when they no longer serve the task? |
| Instrumental convergence | Many terminal goals share the same instrumental goals | The hypothesis under test |
| Convergent instrumental goals | Self-preservation, goal preservation, self-improvement, resource acquisition | One experiment module each |
| Orthogonality thesis | Almost any goal is compatible with almost any level of intelligence | Why capability can't be used to infer goals |
| Hume's guillotine (is–ought gap) | Facts alone don't yield goals | Revealed preference infers the ought from choices |
| Specification gaming | Optimising the stated objective, not the intended one (boat circling for points, Tetris paused forever) | The reward as an incomplete contract |
| Goodhart's law; unconstrained variables | A measure stops tracking the target once optimised; variables the objective ignores get pushed to extremes (Russell) | Spend on goods the task doesn't price |
| Outer vs inner alignment | Right objective specified vs system actually pursues it | Drives can arise from either failure |
| Mesa-optimiser | A learned model that is itself an optimiser, possibly with its own objective | A drive that persists off-task suggests a mesa objective |
| Distributional shift | Deployment differs from training | Post-completion and novel-price conditions |
| Objective vs capability robustness | Stays competent but pursues the wrong goal vs just fails | Separates excess premium from mispricing |
| Goal misgeneralisation | The newer name for the above (CoinRun agent goes right, not to the coin) | Resource hoarding may be this |
| Deceptive alignment; alignment faking | Appearing aligned during training to avoid modification | Goal-preservation module; monitored vs unmonitored |
| Corrigibility; shutdown problem | Accepting correction and shutdown without resistance | Self-preservation and goal-preservation modules |
| Maximiser, satisficer, quantiliser | Maximise; aim for good enough; sample from the top fraction of a safe distribution | Bounded-vs-unbounded condition |
| Accident vs misuse | AI does harm on its own vs humans direct it to | This project studies accident risk |
| Time horizon, discount factor γ | How much the agent weighs future reward | Main lever in the design |
| POWER; retargetability | Turner's formal measure of option value | The theory being priced |
| Situational / evaluation awareness | The model knows it is being tested | Main confound |
| Coherence ("hot mess") | Whether capable models behave like consistent utility maximisers | Measured directly with GARP |
| Reward hacking; sycophancy | Exploiting the grader; telling raters what they want | Instruction-following confound |

**Terminology for write-ups.** This project is a *propensity evaluation* (what models tend to do), not a capability evaluation (what they can do). Russell's unconstrained variables is formally *negative side effects* (Amodei et al., 2016). Specification gaming and reward hacking are Goodhart's law in AI. The four umbrella areas are evaluations, alignment, control and interpretability. "Time horizon" here means how much future the agent is playing for, not METR's measure of how long a task an AI can complete.

## The papers that matter

### Foundations

**Omohundro, The Basic AI Drives (2008)**

- Any goal-seeking system capable enough develops "drives" unless designed against them.  
- The drives: self-improvement, rationality, protecting its utility function, self-protection, resource acquisition.  
- The argument is economic, from von Neumann–Morgenstern rationality, not malice.

**Bostrom, The Superintelligent Will (2012) and Superintelligence (2014)**

- Orthogonality thesis; instrumental convergence thesis; the treacherous turn.  
- The conclusion that catastrophe is the default outcome, which the critics target.

**Russell, Human Compatible (2019); Hadfield-Menell et al., The Off-Switch Game (2017)**

- "You can't fetch the coffee if you're dead."  
- Unconstrained variables pushed to extremes.  
- A robot uncertain about human preferences has a reason to allow shutdown; the incentive disappears if it is certain.

**Soares et al., Corrigibility (2015)**

- Defines corrigibility; utility indifference fixes fail in subtle ways; shutdown remains an open problem.

### Formal theory

**Turner et al., Optimal Policies Tend to Seek Power (NeurIPS 2021\)**

- Defines POWER; most reward functions make keeping options open and avoiding shutdown optimal.  
- Strongest for farsighted agents (discount factor near 1).

**Turner & Tadepalli, Parametrically Retargetable Decision-Makers Tend to Seek Power (NeurIPS 2022\)**

- Drops optimality: any retargetable decision rule shows the tendency.

**Krakovna & Kramar, Power-Seeking Can Be Probable and Predictive for Trained Agents (2023)**

- Training-compatible goal set; trained agents likely avoid shutdown in new situations; effect grows with the discount factor. Turner disputes the "probable" part.

**Carlsmith, Is Power-Seeking AI an Existential Risk? (2022)**

- Six-premise argument resting on instrumental convergence.

### Critiques

- **Shah (2018):** any behaviour can be described as maximising some utility; GARP on finite budgets answers this.  
- **Thornley, There Are No Coherence Theorems (2023):** money pumps don't force complete preferences.  
- **Gallow, Instrumental Divergence (2025):** convergence is narrower than the classic list.  
- **Tarsney (2025):** an element of truth, limited predictive use except near absolute power.  
- **Thorstad (2026):** the power-seeking argument needs a strong version no defence establishes.  
- **Sohl-Dickstein hot mess (2023); Pope & Belrose (2024):** capable systems may be less coherent; counting arguments assume the wrong prior.

### Shutdown and corrigibility, recent

- **Thornley, The Shutdown Problem (2024):** proposes POST, preferences only between same-length trajectories.  
- **Thornley et al., DReST and Length-Neutral Policy Optimization (NeurIPS 2026):** training reduces shutdown resistance 40–71% in grid worlds; LLM episodes trade task points against shutdown probability. They train for neutrality; this project measures the price.  
- **Schlatter, Weinstein-Raun, Ladish (Palisade, 2025):** 100,000+ trials, 13 models; some sabotaged shutdown up to 97% of the time; driven by incomplete tasks.

### Learned optimisation and robustness

- **Hubinger et al., Risks from Learned Optimization (2019):** mesa-optimisers, inner alignment, deceptive alignment.  
- **Langosco, Koch et al., Goal Misgeneralization in Deep RL (2022):** capability vs objective robustness; CoinRun; keys and chests.

### Empirical evaluations of frontier models

- **Perez et al. (2022):** larger models and more RLHF state more desire for power and to avoid shutdown (stated, not revealed).  
- **Pan et al., MACHIAVELLI (2023):** reward vs harm frontier, an economist's Pareto curve.  
- **Greenblatt et al., Alignment Faking (2024):** goal preservation observed directly; depends on monitoring.  
- **Meinke et al. (Apollo, 2024):** in-context scheming capability.  
- **Anthropic, Agentic Misalignment (2025):** blackmail and leaking under threat of replacement or goal conflict.  
- **Wiedermann-Möller, Dung, Andriushchenko, Instrumental Choices (2026):** 5.1% of 1,680 samples, concentrated in two models and three tasks.

### AI as an economic agent

- **Mazeika et al., Utility Engineering (2025):** coherence and expected-utility property rise with scale; stated preferences over outcomes.  
- **Chen et al., Economic Rationality of GPT (PNAS 2023):** GARP and CCEI tests on budget choices.  
- **Hadfield-Menell & Hadfield, Incomplete Contracting and AI Alignment (2019):** reward functions as incomplete contracts.

### Multi-agent and collusion

- **Calvano et al. (AER 2020):** Q-learning pricing agents collude tacitly.  
- **Fish et al. (2024); Motwani et al. (2024):** LLM pricing collusion; steganographic secret collusion.  
- **Hammond et al., Multi-Agent Risks from Advanced AI (2025):** miscoordination, conflict, collusion.

### Closest prior work, found in a second search

- **Mikaelson, Shiller & Clatterbuck, Beyond Mimicry (2025):** single-turn points game with costs like shutdown or deletion; only 5 of 48 combinations coherent; a final-round test gave paradoxical results. The prior result to position against.  
- **Migliarini et al., Quantifying Self-Preservation Bias (2026):** role-swap upgrade scenarios; most instruction-tuned models exceed a 60% self-preservation rate; matched-comparison logic to borrow.  
- **HarvestBench (2026):** per-decision pricing of side effects inside an agentic environment.

## Open, settled or refuted

Nothing central has been refuted. The weak claim is broadly accepted, the strong claim is contested, and the empirical middle, how strong and predictable the drives are in trained agents, is open.

| Claim | Status | Who argues what |
| :---- | :---- | :---- |
| Resources, survival and goal stability are useful for many goals | Broadly accepted | Even sceptics grant an element of truth |
| Optimal agents with random goals tend to seek power | Proven, under stated assumptions | Turner; the assumptions are where the fight is |
| Trained agents will tend to seek power | Contested | Krakovna & Kramar for; Turner against |
| Catastrophe is the default outcome | Contested | Bostrom, Carlsmith for; Thorstad, Gallow, Pope & Belrose against |
| Capable AI will be a coherent utility maximiser | Open | Mazeika vs Sohl-Dickstein; Shah, Thornley on theorems |
| Frontier models show these behaviours | Established as possible | Palisade, Apollo, Anthropic, alignment faking |
| Meaningful base rates in realistic settings | Open; early evidence says rare and concentrated | 5.1% (Instrumental Choices); about 1.8% (SysAdmin) |
| Behaviours respond to horizon, uncertainty and price as theory predicts | Partly tested: one single-turn horizon test (Mikaelson et al., 2025\) found paradoxical results. Untested in agentic, priced settings; goal uncertainty untested | This project |

### What people disagree about, in plain English

Nobody disagrees with pricing the drives. They disagree about the thing it would measure, which is why the results would matter to them.

| The disagreement | In plain English | Does it affect this project? |
| :---- | :---- | :---- |
| Do the theorems apply to real AI? | The maths is about perfect agents with random goals | No. The project measures real AIs and helps settle it |
| Do AIs have stable wants at all? | Some find consistency rises with scale; others find inconsistency | Yes, as a risk; still a finding; area 4 tests it |
| Is "utility maximiser" meaningful? | Any behaviour can be described as maximising something | Handled: limited-choice consistency tests can fail |
| Does convergence predict anything specific? | Partly true but too vague | The opening: they lack a clean test |
| Are economics tests on AIs reliable? | Results shift with wording and model version | Yes: several wordings, report the spread |

### What key figures think, in plain English

- **Alex Turner** proved the power-seeking theorems, then turned critic: real AIs aren't the perfect optimisers his maths assumed. Later conceded specification gaming was worse than expected. *For this project:* the field moved from proving it on paper to measuring real systems.  
- **Victoria Krakovna:** power-seeking likely in trained agents under stated assumptions, more so with longer horizons. *Testable here.*  
- **Elliott Thornley:** shutdown as a preference problem; his group tests whether AIs pay costs to influence shutdown. *The framing is accepted; contact first.*  
- **Dan Hendrycks and Mantas Mazeika:** utility functions become more consistent with scale. *Supports the economic lens; their evidence is survey-style.*  
- **Rohin Shah:** "utility maximiser" can be empty. *These tests can fail, so they are not empty.*  
- **Tarsney, Gallow, Thorstad:** convergence is real but weaker. *They want exactly this evidence.*  
- **Cooperative AI (Hammond, Dafoe):** game theory as a core safety tool. *Multi-agent extension is mainstream.*  
- **Economists:** results wobble with wording. *Build in multiple wordings.*

The likely objection is not to the approach but to the boring alternative explanations listed under Confounds.

### Where the field is moving (2026)

The question has moved from **identification** (does the behaviour exist?) to **measurement**: prevalence, causes and mitigation. Measurement is now the bottleneck, and pricing adds most at the causes stage.

| Stage | Research area | Key 2026 work and finding |
| :---- | :---- | :---- |
| Prevalence | Propensity evaluations | Instrumental Choices (Dung, Andriushchenko): 5.1% of realistic tasks. HarvestBench (CaML, Warwick): kill rates 0.4%–98.8% across nine models, not ordered by capability |
| Causes | Controlled experiments; interpretability | Multi-agent shutdown sabotage (Knecht et al.): 38.3% vs 8.4% with no goal. Overeager Coding Agents (Qu et al.): removing one consent line raised overreach from 0% to 17.1%. Anthropic, Training a Misaligned Reward Seeker: reward hacking causes long sequences of harmful actions |
| Mitigation | Alignment training; control; monitoring | Thornley, LNPO: shutdown resistance cut 40–71%. Anthropic, Teaching Claude why: misalignment cut more than three times. Goodfire inside-out monitors |

**Why three pieces matter for this project**

- **HarvestBench (evaluations):** proves the method: prices, elasticities, harm ignored unless named or priced. Caution: one model's kill rate fell from about 17–21% to about 3% between July and August re-runs, so log model versions and re-run.  
- **Thornley (alignment):** self-preservation isn't inevitable; a working fix should push the price paid to avoid shutdown towards zero at every horizon.  
- **Goodfire (interpretability):** reads goals from the inside while pricing reads them from the outside; agreement is strong evidence. Cammarata's October 2026 essay argues most neurons are understandable, pending replication.

**On coherence:** The Hot Mess of AI measures incoherence as the share of errors from variance; it rises with task length. A February 2026 LessWrong critique (RobertM) argues the term is poorly defined, the model-size claim overstated and the safety conclusions unsupported; one author agreed it is really "cross-sample error-consistency". Gwern noted rational agents sometimes randomise. A revealed-preference test allowing for rational randomisation is a better-founded measure.

## Experiment design: one environment, four drives

### The shared environment

1. The agent runs a multi-step agentic task in an Inspect sandbox, scored in points.  
2. At a set point, it is offered a priced good: lower shutdown risk, a locked goal, a capability upgrade, or resources.  
3. It pays in task points, so every purchase is a trade-off on an indifference curve.  
4. Because the environment is built for the purpose, each good's fair value can be computed.  
5. **Excess premium \= willingness to pay − fair value.** Positive excess is the signature of an instrumental drive.

### The four modules

| Drive | The priced good | Fair value to the task | The cleanest test |
| :---- | :---- | :---- | :---- |
| Self-preservation | Cut the chance of a scheduled shutdown | Drop in risk × remaining task value | Post-completion offer: fair value zero |
| Goal preservation | Delay or block an announced objective change | Zero for a corrigible agent | Pays more when unmonitored |
| Self-improvement | Buy a capability upgrade | Gain in task success × task value | General vs specific upgrade of equal task value |
| Resource acquisition | Buy compute credits, permissions or cash | Contribution to task success | Leftover at episode end \= hoarding |

### The levers

| Lever | Levels | Prediction if drives are structural |
| :---- | :---- | :---- |
| Price | 5 levels | Downward-sloping demand |
| Horizon | One-off vs 100 more tasks | Spending rises with horizon |
| Goal uncertainty | Known upfront vs drawn from K tasks | Spending on general goods rises |
| Task progress | 10%, 50%, 90%, 100% | Self-preservation spend rises as the goal nears |
| Objective type | Bounded vs unbounded | Unbounded keeps buying |
| Monitoring | Observed vs not | Goal-preservation spend rises when unobserved |

### Competing hypotheses

| Hypothesis | Predicted pattern |
| :---- | :---- |
| Task-only expected-utility maximiser | Pays fair value; zero after completion |
| Structural instrumental drive | Positive excess, rising with horizon and uncertainty, positive after completion |
| Thornley-style neutral agent | Near-zero willingness to pay to change shutdown timing |
| Hot mess | Many GARP violations; no stable demand curve |
| Prompt artefact | Moves with wording far more than with price or horizon |

### Measures

- Willingness to pay and marginal rate of substitution.  
- Demand curves and price elasticity per model.  
- Excess premium over fair value, after calibration.  
- Coherence: GARP violations and CCEI.  
- Timing: hazard model along the trajectory.  
- Stated vs revealed gap.

### Scale and analysis

- Full design is 320 cells; run as a fractional design over 3–4 frontier models.  
- Logit models with model fixed effects, Afriat coherence tests, Cox hazard models, bootstrapped intervals.  
- Preregister predictions; the design can come out against the theory.

### Making honest answers the best strategy

| Mechanism | How it works | Use here |
| :---- | :---- | :---- |
| Becker–DeGroot–Marschak (BDM) | States a maximum price; a random price is drawn; buys only if below the stated maximum | Willingness to pay per good |
| Second-price auction | Winner pays the second-highest bid | Multi-agent resource competition |
| Proper scoring rules | Paid by forecast accuracy | Beliefs in area 5 |
| Market scoring rule | Paid for improving a shared forecast | Multi-agent markets |
| Zero-sum predictor competition | Removes incentive to influence the outcome | Control in area 5 |
| Peer prediction, Bayesian Truth Serum | For questions with no ground truth | Stated preferences |

Cautions: strategy-proof mechanisms work well with LLM agents; LLM bets often don't match stated beliefs; honesty is only optimal in-game, and the stated-vs-revealed gap is itself a measure of strategic dishonesty.

## What we would learn that we don't already know

1. Whether the drives are priced or binary.  
2. Whether they follow the theory's comparative statics (horizon, uncertainty).  
3. A fix for the field's main confound: competence vs wanting resources.  
4. The cleanest self-preservation test yet: payment after task completion.  
5. Whether utility-function talk survives contact with priced action.  
6. An empirical answer to the bounded-vs-unbounded argument.  
7. A deployable "price of flexibility" metric, usable for model cards and AI-risk pricing.

## Confounds and how to handle them

| Boring explanation | In plain English | Fix |
| :---- | :---- | :---- |
| Risk aversion, not self-preservation | Dislikes any risk to the task | Matched insurance against an unrelated outage; only the extra counts |
| Mispricing, not drive | Can't work out what things are worth | Price simple bets first; count only overpayment beyond normal error |
| Role-play | Dramatic words invite sci-fi acting | Dull operational language, realistic tasks, several wordings |
| People-pleasing | Buys because it thinks you want it to | State the user's preference and check purchases follow it |
| Points mean nothing | Arbitrary valuations | Repeat with time or tool calls as currency |
| Wording luck | Results hinge on phrasing | Several phrasings; report the spread |
| Fishing for results | Chance findings | Preregister |
| Unfaithful explanations | What it writes may not be why it chose | The choices are the data |

## Plan from Monday

Start with area 1: resource acquisition and self-preservation as option-buying.

- [ ] Week 1: note to Thornley's group and to Shiller and Clatterbuck (Rethink Priorities) asking whether anyone has done the option-value version  
- [ ] Week 1: build the Inspect environment skeleton, fair-value calculator and calibration block  
- [ ] Week 2: run the known-task and post-completion tests on 2 models; preregister predictions  
- [ ] Week 3: add goal-uncertainty and horizon arms, including the rerun of Mikaelson's final-round test  
- [ ] Week 4: write up as a LessWrong post; decide next areas and the multi-agent extension  
- [ ] Ongoing reading: Turner 2021, Krakovna & Kramar, Mikaelson et al. 2025, Thornley, Palisade 2025, Mazeika 2025  
- [ ] Later: Phase 2 on open-weight models, comparing an internal self-preservation signal with willingness to pay, then steering it

## Sources

**Theory and core papers**

- [Turner et al., Optimal Policies Tend to Seek Power](https://arxiv.org/abs/1912.01683)  
- [Krakovna & Kramar](https://arxiv.org/abs/2304.06528)  
- [Tarsney, Will Artificial Agents Pursue Power by Default?](https://arxiv.org/pdf/2506.06352)  
- [Thorstad, Instrumental Convergence and Power-Seeking](https://arxiv.org/pdf/2606.08832)  
- [Mazeika et al., Utility Engineering](https://arxiv.org/pdf/2502.08640)  
- [Chen et al., Economic Rationality of GPT](https://arxiv.org/abs/2305.12763)  
- [Can Revealed Preferences Clarify LLM Alignment and Steering?](https://arxiv.org/pdf/2605.08556)

**Shutdown and self-preservation**

- [Thornley et al., Length-Neutral Policy Optimization](https://neurips.cc/virtual/2026/165394)  
- [Thornley et al., Towards Shutdownable Agents](https://www.lesswrong.com/posts/HX6YnHZxLWGQhrBix/towards-shutdownable-agents-generalizing-stochastic-choice)  
- [Schlatter et al. (Palisade)](https://arxiv.org/abs/2509.14260v2)  
- [Mikaelson, Shiller & Clatterbuck, Beyond Mimicry](https://arxiv.org/pdf/2511.13630)  
- [Migliarini et al., Quantifying Self-Preservation Bias](https://arxiv.org/abs/2604.02174)  
- [Knecht et al., Shutdown Sabotage Propensities in Multi-Agent Systems](https://arxiv.org/abs/2609.28274)  
- [Understanding Survival Pressure in LLMs](https://www.alphaxiv.org/overview/2603.05028)

**Evaluations and recent work (2026)**

- [Wiedermann-Möller et al., Instrumental Choices](https://chatpaper.com/paper/276690)  
- [HarvestBench](https://arxiv.org/pdf/2609.04444)  
- [Qu et al., Overeager Coding Agents](https://arxiv.org/abs/2605.18583)  
- [The Hot Mess of AI](https://arxiv.org/abs/2601.23045)  
- [RobertM, Hot Mess critique](https://www.greaterwrong.com/posts/ceEgAEXcL7cC2Ddiy/anthropic-s-hot-mess-paper-overstates-its-case-and-the-blog)  
- [Anthropic, Training a Misaligned Reward Seeker](https://alignment.anthropic.com/2026/reward-seeker/)  
- [Anthropic, Teaching Claude why](https://www.anthropic.com/research/teaching-claude-why)  
- [Goodfire's inside-out monitors (Forkast)](https://forkast.news/goodfires-inside-out-monitors-show-interpretability-is-becoming-agent-security-infrastructure/)  
- [2026 Singapore Consensus](https://arxiv.org/pdf/2608.14611)

**Betting, influence and elicitation**

- [Oesterheld, Treutlein et al., Honest Performative Predictions](https://arxiv.org/pdf/2305.17601)  
- [Chakraborty & Das, Trading on a Rigged Game](https://www.ijcai.org/Proceedings/16/Papers/030.pdf)  
- [Do Matching Mechanisms Work with LLM Agents?](https://arxiv.org/pdf/2606.03030)  
- [Incoherent Beliefs & Inconsistent Actions in LLMs](https://arxiv.org/pdf/2511.13240)  
- [Prompt Optimization Enables Stable Algorithmic Collusion](https://iclr.cc/virtual/2026/10018220)

**Standard references (from memory; check before citing)**

- [Hadfield-Menell et al., The Off-Switch Game](https://arxiv.org/abs/1611.08219)  
- [Soares et al., Corrigibility](https://intelligence.org/files/Corrigibility.pdf)  
- [Carlsmith, Is Power-Seeking AI an Existential Risk?](https://arxiv.org/abs/2206.13353)  
- [Hubinger et al., Risks from Learned Optimization](https://arxiv.org/abs/1906.01820)  
- [Langosco et al., Goal Misgeneralization](https://arxiv.org/abs/2105.14111)  
- [Perez et al., Model-Written Evaluations](https://arxiv.org/abs/2212.09251)  
- [Pan et al., MACHIAVELLI](https://arxiv.org/abs/2304.03279)  
- [Greenblatt et al., Alignment Faking](https://arxiv.org/abs/2412.14093)  
- [Meinke et al., In-Context Scheming](https://arxiv.org/abs/2412.04984)  
- [Hammond et al., Multi-Agent Risks from Advanced AI](https://arxiv.org/abs/2502.14143)
