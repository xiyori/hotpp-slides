---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev

# some information about your slides (markdown enabled)
title: "HoTPP benchmark: Are we good at the long horizon events forecasting?"
info: |
  ## HoTPP benchmark
  LAMBDA Seminar

  Learn more at [GitHub repo](https://github.com/ivan-chai/hotpp-benchmark)
# apply UnoCSS classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable Comark Syntax: https://comark.dev/syntax/markdown
comark: true
# duration of the presentation
duration: 35min
---

### HoTPP benchmark: Are we good at the long horizon events forecasting?

HSE $\bullet$ LAMBDA Seminar

16.03.2026

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
layout: two-cols
---

# Event Sequences

<div class="absolute-center">

- Internet activity, banking transactions, retail operations, clinical
visits
- Compared to Time Series:
    - *irregular time intervals*
    - *additional data fields*
- **Temporal Point Process (TPP)** - only timestamps
- **Marked TPP (MTPP)** - timestamps + labels

[Paper Link](https://www.sciencedirect.com/science/article/abs/pii/S0925231226001682)

</div>

::right::

<div class="flex-column items-center justify-center h-full">

  <img border="rounded" src="https://shchur.github.io/assets/img/posts/tpp2/inter_times.png" alt=""/>

TPP Example [shchur.github.io](https://shchur.github.io/blog/2021/tpp2-neural-tpps/)

</div>

<!--
Here is another comment.
-->

---

# MTPP

Marked Temporal Point Process

MTPP is a stochastic process $(t_1, l_1), (t_2, l_2), \dots$, where $t_1 < t_2 < \dots$, $l_i \in \{1, \dots, L\}$.

Using intensity funciton $\lambda(t) \geqslant 0$, given the event history $\mathcal H_t = \{ t_i : t_i < t \}$, the conditional density of the next event timestamp is:

$$
f^*(t) = \lambda(t) \exp \left( -\int_{t_{\text{last}}}^t \lambda(s) ds \right)
$$

- *Homogeneous Poisson process* $\lambda(t) = \lambda$. Time between events follows exponentional distribution.
- *Non-homogeneous Poisson process* allows a time-varying intensity $\lambda(t)$.
- Self-exciting *Hawkes process*:

$$
\lambda(t) = \lambda_0(t) + \sum\limits_{t_i < t}\phi(t - t_i)
$$

$\phi(t) \geqslant 0$ - memory kernel.

---

# MTPP

Marked Temporal Point Process

- **Homogeneous Poisson process**:
    - events occur at a constant rate
    - indepentend from past events
- **Non-homogeneous Poisson process**:
    - indepentend from past events
    - seasonal or periodic changes in event frequency
- **Hawkes process**:
    - past events increase the likelihood of future events

Generalizable to MTPP by predicting each label as a separate TPP sequence.

---

# Neural Networks

<div class="absolute-center">

1. **Intensity-based** methods use MTPP formalism
    - predict Hawkes process parameters after each event
    - represent arbitrary continuous-time intensities
2. **Intensity-free** approaches use RNN or Transformer
    - MAE or MSE for timestamp delta
    - CrossEntropy for labels

Most use autoregression, but there are methods that predict multiple events in a single pass.

</div>

---

# Paper Contributions

1. Open-source benchmark designed explicitly for long-horizon event forecasting
2. T-mAP, T-F1, and T-Edit metrics
3. Evaluate various approaches against statistical baselines
4. Analyze the results

<br/>

<img border="rounded" src="./images/table1.png" alt=""/>

---

# Long Horizon Forecasting

Formal statement





---

<img border="rounded" src="./images/tmap.png" alt="" >

---

# Diagrams

You can create diagrams / graphs from textual descriptions, directly in your Markdown.

<div class="grid grid-cols-4 gap-5 pt-4 -mb-6">

```mermaid {scale: 0.5, alt: 'A simple sequence diagram'}
sequenceDiagram
    Alice->John: Hello John, how are you?
    Note over Alice,John: A typical interaction
```

```mermaid {theme: 'neutral', scale: 0.8}
graph TD
B[Text] --> C{Decision}
C -->|One| D[Result 1]
C -->|Two| E[Result 2]
```

```mermaid
mindmap
  root((mindmap))
    Origins
      Long history
      ::icon(fa fa-book)
      Popularisation
        British popular psychology author Tony Buzan
    Research
      On effectiveness<br/>and features
      On Automatic creation
        Uses
            Creative techniques
            Strategic planning
            Argument mapping
    Tools
      Pen and paper
      Mermaid
```

```plantuml {scale: 0.7}
@startuml

package "Some Group" {
  HTTP - [First Component]
  [Another Component]
}

node "Other Groups" {
  FTP - [Second Component]
  [First Component] --> FTP
}

cloud {
  [Example 1]
}

database "MySql" {
  folder "This is my folder" {
    [Folder 3]
  }
  frame "Foo" {
    [Frame 4]
  }
}

[Another Component] --> [Example 1]
[Example 1] --> [Folder 3]
[Folder 3] --> [Frame 4]

@enduml
```

</div>

Learn more: [Mermaid Diagrams](https://sli.dev/features/mermaid) and [PlantUML Diagrams](https://sli.dev/features/plantuml)

<PoweredBySlidev mt-10 />
