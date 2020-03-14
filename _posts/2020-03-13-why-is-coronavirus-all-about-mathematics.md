---
layout: post
title: "Why is Coronavirus all about Mathematics?"
categories:
    - mathematics
crosspost_to_medium: false
use_math: True
---

<blockquote>
“For since the fabric of the universe is most perfect, and is the work of a most wise Creator, nothing whatsoever takes place in the universe in which some relation of maximum and minimum does not appear.”
<br><b>― Leonhard Euler </b>
</blockquote>

On 11 March 2020, the World Health Organization officiallly [declared](https://twitter.com/WHO/status/1237777021742338049?s=20) the coronavirus (SARS-CoV-2 or COVID-19) a [pandemic](https://en.wikipedia.org/wiki/Pandemic). But, fear not, this is not yet another opinionated response on the failing of society and the end of times. This is all about Mathematics!

{% include posts/2020-03-13-why-is-coronavirus-all-about-mathematics/1.html %}
<sub>Source: https://systems.jhu.edu/research/public-health/ncov/</sub>

Curiously enough, the numbers might help us understand all the fuss we hear about social distancing, flattening the curve, lockdowns and ultimately vaccinations.

#### Exponential Growth

An epidemic is a textbook example of an exponential growth. Not only an example, but its underlying principle is a centerpiece in the history of Mathematics and its discovery was fundamental for breakthroughs in Probability Theory, Mathematical Analysis, Differential Equations, Physics, Chemistry and Biology and even Pop Culture.

The idea is rather straightforward: it has do with the way a quantity changes. When the rate on which a given quantity changes is proportional to the quantity itself at any given moment, mathematicians called it exponential.

```
the rate of change is proportional to the quantity at any given time
```

Probably many in the past observed this behavior on how populations expand, diseases spread, biology decays or even how science progresses, but it was formally brought to life in the work on logarithms. Later, while studying compound interest - more money you have, more money you make - [Bernoulli](https://en.wikipedia.org/wiki/Jacob_Bernoulli) discovered a constant ironically known as [Euler's number](https://en.wikipedia.org/wiki/E_(mathematical_constant)).

We will have the opportunity to talk about the multiple "origins" of that constant in the future.

#### Exponentiate!

Coming back to the virus. In our case, having an exponential growth suggests that the larger the infectious population, quicker we will have new cases and the infectious population will grow. We pratically experience that whenever people get sick around us (or when all of our friends start getting pregnant at the same...no! it is not exponential...or is it?)

Scientists denote ideas using mathematical script for convenience (sometimes laziness). Let us do it then,

- *I(t)*: infectious population

$$
\begin{equation}
\Delta I(t) \sim I(t) \implies \frac{dI}{dt} \sim I(t)
\end{equation}
$$

```
the rate of infection is proportional to the infectious population
```

Well, stating a relation of proportionality does not give us much. We still are not able to answer any questions. Is this virus dangerous? How contagious is it? Is it deadly? Are we all going to die?

We are going to formulate a model using variables and parameters to quantify *how proportial* that relation is.

- *$\beta$*: *contact rate* or how many people an infected person comes into contact with in given time
- *$\gamma$*: *recovery rate* or how many people recover in given time

Using our intuition for the model's formulation, those are the two parameters we will take into account. The rate on which people are infected should grow the more contact they have to each other and should decay as they recover. In another words, the rate of change is *positively* proportional to $\beta$ (*contact rate*) and *negatively* proportional to $\gamma$ (*recovery rate*)

Finally, we have our equation,

$$
\begin{equation}
\frac{dI}{dt} = \left(\beta - \gamma\right) I 
\end{equation}
$$

Now let us take some time to check if we can take some conclusions from it. 

If the *recovery rate* is greater than *contact rate*, the rate of change will always be negative, so the infection will eventually dissipate and even not outbreak. On the other hand, if *contact rate* is greater *recovery rate*, we will have a disaster. Apparently, those paramaters indicate how strong an epidemic can be.

Now, if $\gamma$ is the *recovery rate*, then $1/\gamma$ is the *infectious/recovery period* or the period of time during which an infected individual can pass it on, consider the product between the $\beta$ (*contact rate*) and $1/\gamma$ (*infectious period/recovery*) and we will have the average number of people an infected patient will pass it on.

$$
\begin{equation}
R_{0} = \frac {\beta}{\gamma}
\end{equation}
$$

In fact, that indicator is known as the *basic reproduction number*. Note that when $R_0 > 1$ the infection will be able to start spreading in a population, but not if $R_0 < 1$.

Probably everybody has that number in their minds at the present. When trying to mitigiate, we will see how important bringing it down is in order to slow down the epidemic.

After the outbreak in China, studies found that COVID-19's basic reproduction number is between [1.4-3.9](https://pubmed.ncbi.nlm.nih.gov/31995857-early-transmission-dynamics-in-wuhan-china-of-novel-coronavirus-infected-pneumonia/), which means that, on avarage, a sick patient transmits the infection to 1.4 and 3.9 others. The *recovery period* is around [10 days](https://www.statnews.com/2020/03/09/people-shed-high-levels-of-coronavirus-study-finds-but-most-are-likely-not-infectious-after-recovery-begins/). 

We solved our equation numerically inputting different parameters to see how it plays out.

{% include posts/2020-03-13-why-is-coronavirus-all-about-mathematics/2.html %}
<sub></sub>

We visually check how small decrements *basic reproduction number* will have a huge accumulative gain over time.That is reason why we should take agressive action, either by social distancing, avoiding and cancelling events. 

We saw that the *basic reproduction number* depends on *contact rate* and *recovery rate*. Since the *recovery rate* is barely in our control as it is typicallly a biological charateristic of the virus, controlling the *contact rate* is our best chance to flatten the curve. That does not mean we should not invest in treatments, best case scenario will bring both down.

### Thou shall not exponentiate!

But here is the plot twist: an epidemic is not purely exponential! Our first model assumed that the infection will spread indefinitely, the population is infinite and there is no immunity or cure. 

Of course, that is nonsense. An rather evil way of think is that once the entire population is infected, there is none left to be infected!

Let us address that in a new model by assuming the following,

- fixed population (nobody dying, moving or being born)
- recovery and immunity

In COVID's case, [it is not clear how long the protection lasts](https://www.independent.co.uk/life-style/health-and-families/coronavirus-immunity-reinfection-get-covid-19-twice-sick-spread-relapse-a9400691.html). But we will assume it lasts longer than our simulated timeframe.

We will use a compartmental model. The idea is to divide the population into group (or *compartments*) and describe how the infection moves from one to another. It was first introduced by [Anderson Ogilvy Kermack](https://en.wikipedia.org/wiki/Anderson_Gray_McKendrick) and [Anderson Gray McKendrick](https://en.wikipedia.org/wiki/Anderson_Gray_McKendrick]).

Let the SIR model be as follows,

- *S(t)*: susceptible but not yet infected population
- *I(t)*: infectious population
- *R(t)*: recovered population

- *$\beta$*: *contact rate* or how many people an infected person comes into contact with in given time
- *$\gamma$*: *recovery rate* or how many people recover in given time
- *N*: total population 

First, the *equation S* tell us that as the population is infected, the susceptible population becames smaller. 

$$
\begin{equation}
\frac{dS}{dt} = - \frac{\beta SI}{N}
\end{equation}
$$

Second, the *equation I* is similar to our original model's, adding a factor of susceptibility.

$$
\begin{equation}
\frac{dI}{dt} = \frac{\beta SI}{N} - \gamma I
\end{equation}
$$

Last, the *equation R* represents that recovered population is proportinal to the recovery rate.

$$
\begin{equation}
\frac{dR}{dt} =  \gamma I
\end{equation}
$$

Unfortunately, that system of differential equations non-linear and does not have analytical solution. Fortunately, we solve it numerically with the following initial conditions,

- *I(0)* = 1 (patient zero)
- *N* = 1.000.000 (population)

{% include posts/2020-03-13-why-is-coronavirus-all-about-mathematics/3.html %}
<sub></sub>

Well...We added all that math...for nothing? Wait for it and zoom out for a moment,

{% include posts/2020-03-13-why-is-coronavirus-all-about-mathematics/4.html %}
<sub></sub>

Now we have it! 

Note that for $R_0 = 4.2$, the original mdoel gave us 1.5M, exceeding our population of 1M. That's nonsense!

Let us see the rest of the solution,

{% include posts/2020-03-13-why-is-coronavirus-all-about-mathematics/5.html %}
<sub></sub>

Once more, we visually check how sensitive those systems are to the *basic reproduction number*. By mitigating the infection, we will be able to not only to postpone the peak of the outbreak, but bringing the maximum number of active cases the at the peak to a lower ground and then protecting the most vulnerable by making them less susceptible and giving people the chance to get proper treatment.

{% include posts/2020-03-13-why-is-coronavirus-all-about-mathematics/6.html %}
<sub></sub>

Another important point to make it is our resources, like healthcare and food supply chain, are limited and not postponing the peak of infection could stress them to a point where they can not operate, leading to catastrophe.

That's why Coronavirus all about Mathematics. As Euler once wrote, "nothing whatsoever takes place in the universe in which some relation of maximum and minimum does not appear.".