Idea -&#x20;

use this well-known hand evaluator [http://www.rpbridge.net/8j19.htm](http://www.rpbridge.net/8j19.htm)

This is a rule that calculates how good a hand is. However in practice, humans can't use this because there are 26 steps.&#x20;

Might we run an experiment to devise a procedure with less steps that mimicks this procedure?&#x20;

You could enumerate over all subsets of steps and do feature selection. We'd just need random steps of 13 cards and value according to this rule

* Think of the 26 steps as **features** f1…f26​ computed from a 13-card hand.
* The RPBridge score yyy is a deterministic function of these features.
* We want a **compressed surrogate** y^\=g(fS)\hat{y}\=g(f\_{S})y^​\=g(fS​) using only a small subset SSS (|S| ≤ k), with simple arithmetic, that minimizes error to yyy.

# Experiment Ideas

## Core Experiments

1. **Experiment Name**
   * Objective: What you aim to prove
   * Method: Your approach and methodology
   * Success: Target metric and threshold
2. **Experiment Name**
   * Objective: What you aim to prove
   * Method: Your approach and methodology
   * Success: Target metric and threshold

## Ablations

* Remove component: Expected impact on results
* Modify parameter: Expected change in behavior

## Baselines

* Baseline method 1: Expected performance level
* State-of-the-art method: How we compare

## Priority

**Must have:** Critical experiments for validation
**Nice to have:** Additional experiments for robustness