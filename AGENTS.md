# Slide Deck Guidance

This repo is a work-in-progress Beamer slide deck for the talk:

> What online advertising reveals about the limits of standard machine learning theory

Use these notes when editing `main.tex`, adding figures, or writing new slides.

## Talk Intent

The deck is not just an introduction to bid optimization. It uses online
advertising, especially real-time bid optimization, as a case study for a
broader claim:

Standard ML theory and methodology usually frame learning as fixed-dimensional
prediction or risk minimization. Deployed advertising systems do not fit that
clean frame. Prediction is embedded inside auction-based decision-making, the
parameter space can grow continually as advertisers/campaigns/ads are created,
and practical models are shaped by economic goals, latency, computational
constraints, automated retraining, stability under downstream optimization, and
structural requirements such as monotonicity.

The main message: these constraints are not secondary implementation details.
They change the mathematical learning problem itself. Online advertising is the
lens; the target is the gap between standard ML formulations and deployed
systems.

## Intended Narrative

When adding or reordering slides, preserve this arc:

1. Start from the familiar clean ML framing: training, generalization,
   convergence, and the standard recommender-system loop.
2. Introduce online advertising concretely: properties, SSPs, DSPs, bid
   requests, candidate ads, auctions, and winners.
3. Formulate bid optimization: a DSP must choose both an ad and a bid, in a few
   milliseconds.
4. Show that prediction is only a component inside a decision process:
   value/purchase probability and win probability feed utility and surplus
   maximization.
5. Expose production constraints: huge catalogues, phased ranking, latency,
   freshness, training speed, continual tuning, and deployment feedback.
6. Explain the data/model setting: sparse ad/context features, entity-specific
   parameters, and potentially growing feature/model spaces.
7. Discuss compact structured models: factorization machines, field-weighted
   variants, win-rate models, bid-shading models, and table/nonparametric
   alternatives such as MEOW.
8. Turn explicitly to theory gaps: fixed-dimensional train/test/convergence
   stories give only partial guidance for growing, structured,
   latency-constrained, decision-coupled systems.
9. Motivate further study of learning with growing models and of simple,
   structured models that perform well under real-world constraints.

The presentation is incomplete. Treat the current deck as a partial
implementation of this narrative, with the final theory-gap argument still to be
developed.

## Core Messages To Preserve

- Bid optimization is not just prediction; it is prediction inside an
  auction-based decision process.
- The operational target is utility, not merely prediction loss.
- Practical model design is shaped by economics, latency, training speed,
  model freshness, stability, automation, and structural constraints.
- Compact and structured models are not merely old-fashioned baselines; they
  can be the right tool because they are fast, trainable, interpretable,
  stable under optimization, and amenable to constraints such as monotonicity.
- Standard ML theory is useful as a starting point, but it misses important
  deployed-system phenomena: growing dimensions, feedback loops, continual
  entity creation, decision-coupled objectives, and strict serving constraints.

## Visual Theme

The existing style is clean, academic, and diagram-first:

- White Beamer pages with blue headings and lots of whitespace.
- Sparse text; prefer one point plus a diagram over dense paragraphs.
- TikZ diagrams with rounded boxes, black outlines, light pastel fills, arrows,
  callouts, dashed boundaries, and drop shadows.
- Animated builds using `\pause`, `\only`, and overlay-aware TikZ styles.
- Concrete screenshots/figures when grounding the story, then abstract diagrams
  when explaining the mechanism.
- Formulas should act as anchors, not as full derivations.

Recurring colors and roles:

- Green: DSP/ad-side actions, selected or active elements.
- Blue/purple: model, data, system, or context objects.
- Orange: constraints, business pressure, or speed/training tradeoffs.
- Red: warnings, impossibility, contrast, or crossed-out standard assumptions.

## Visual Motifs

Reuse and extend these motifs when possible:

- Actor-flow diagrams: property -> SSP -> DSP -> auction -> winning ad.
- Pipeline diagrams: catalogue -> features -> optimal bids -> utilities.
- Constraint diagrams: model design pulled between quality, inference speed,
  and training speed.
- Timeline diagrams: logged events, training windows, configs, processors,
  deployments, and feedback.
- Sparse feature illustrations: logged events split into `x_ad` and `x_ctx`,
  then represented as sparse field vectors.
- Contrast slides: ideal vs practice, pros vs cons, standard RecSys flow vs
  crossed-out RecSys flow.
- Callouts that label which quantities are machine learned inside the utility
  function.

Prefer layout-driven TikZ structure: matrices, loops, coordinate grids, named
nodes, and reusable styles. Avoid fragile manual placement when a structured
layout would be clearer.

## Language Patterns

Use direct, didactic slide language. Good patterns already present:

- Question titles: "How are bids chosen?", "What kind of data?"
- Problem titles: "Challenge - ranking a huge catalogue in milliseconds"
- Contrast titles: "DSP ad choice - ideal vs practice"
- Short operational claims: "in a few milliseconds", "fast-to-compute",
  "fast updates", "fresh model"
- Explicit bridge sentences from ideal math to production practice.
- Pros/cons framing for model choices.

Keep text plain and concrete. Prefer "every N events" style phrasing over
jargon. Avoid paper-like compression when the slide is meant to guide the
audience through a mechanism.

## Slide-Writing Guidelines

- Each new slide should answer one of these questions:
  - What clean ML assumption are we starting from?
  - What advertising mechanism complicates it?
  - What production constraint changes the model or objective?
  - What structured/simple model response does this motivate?
  - What theory gap does this reveal?
- Make the bridge from prediction to decision explicit. Do not let a slide read
  as if the task is only CTR/CVR/win-rate prediction.
- When introducing a practical constraint, show how it changes the mathematical
  or modeling problem.
- If adding a model example, state why it is useful under constraints, not only
  what its formula is.
- If adding a theory slide, connect it back to the concrete ad-system example.
- Keep "simple models are useful" tied to speed, stability, automation,
  interpretability, structure, and downstream optimization.

## Known Cautions

- The title and abstract are the source of intent. If the current deck and the
  abstract diverge, revise the deck toward the abstract.
- Do not treat the current ending as final; the "ML Theory gaps" section is only
  a placeholder for the argument that still needs to be built.
