### xixi

I build small world models and write down the parts that fail.

---

**The arc so far.** I started by encoding the I Ching as a differentiable
state-space model — 64 hexagrams as vertices of a signed 6-cube, the King Wen
permutation and 错/综/互 relations hard-coded, only the continuous parts
learning. It solved no real problem. On the one test designed to be
falsifiable — change-point detection against a tuned PELT baseline — it lost by
2×.

One methodological result survived: a representation trained to serve a
*controller* is not good enough to *plan* with. Learn it from the dynamics
directly, with an anti-collapse regulariser, and action-sensitivity goes up
~16×. Reproduced across 5 seeds with an ablation.

But every environment there was one I had written myself — a tautology engine,
where the model learns to invert a generator I control. So I pointed the same
pipeline at dynamics nobody designed and asked whether the latent transition
earns its place at all. Six regimes later:

| regime | what actually carries the load |
|---|---|
| observation = state | plain MLP in observation space |
| observation < state | delay embedding (Takens), not a learned latent |
| high-D pixels | reconstruction-trained encoder — for rollout *stability* only |
| stochastic dynamics | heteroscedastic output head (not a latent, not an ensemble) |
| planning | dynamics that transfer across task instances |
| long-term memory | recurrence **+ a dense predictive objective** |

The learned latent transition is the active ingredient in zero of the six.

---

**Repos**

- [lorenz-world-model](https://github.com/xiayu23123/lorenz-world-model) — the six-regime control study. Lorenz-63 and friends, 32 tests, every claim seeded and ablated.
- [yi-world-model](https://github.com/xiayu23123/yi-world-model) — the I Ching prototype it grew out of, including the negatives.
- [learning-in-loops](https://github.com/xiayu23123/learning-in-loops) — essays, speculative fiction, and the writeups for both of the above.

**Writing** — [learning-in-loops.pages.dev](https://learning-in-loops.pages.dev)

Negative results, reproduced and ablated. They are the part that saves the next
person the weeks.
