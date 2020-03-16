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
<sub>Source: https://systems.jhu.edu/research/public-health/ncov/ as of March 12th.</sub>

Curiously enough, the numbers might help us understand all the fuss we hear about social distancing, flattening the curve, lockdowns and ultimately vaccinations.

#### Exponential Growth

An epidemic is a textbook example of an exponential growth. Not only an example, but its underlying principle is a centerpiece in the history of Mathematics and its discovery was fundamental for breakthroughs in Probability Theory, Mathematical Analysis, Differential Equations, Physics, Chemistry and Biology and even Pop Culture.

The idea is rather straightforward: it has do with the way a quantity changes. When the rate on which a given quantity changes is proportional to the quantity itself at any given moment, mathematicians called it exponential.

```
the rate of change is proportional to the quantity at any given time
```

Let us apply that idea on data from the beginning of the outbreak in China,

{% include posts/2020-03-13-why-is-coronavirus-all-about-mathematics/7.html %}
<sub>Source: https://systems.jhu.edu/research/public-health/ncov/ as of March 12th.</sub>

Probably many in the past observed this behavior on how populations expand, diseases spread, biology decays or even how science progresses, but it was formally brought to life in the work on logarithms.

Later, while studying compound interest - more money you have, more money you make - [Jabob Bernoulli](https://en.wikipedia.org/wiki/Jacob_Bernoulli) discovered a constant ironically known as [Euler's number](https://en.wikipedia.org/wiki/E_(mathematical_constant)).

We shall have the opportunity to talk about that constant's multiple "origins" in the future.

#### Exponentiate!

Coming back to the virus. In our case, having an exponential growth suggests that the larger the infectious population, quicker we will have new cases and that infectious population will grow. We pratically experience that whenever people get sick around us (or whenever all of our friends start getting pregnant at the same...no! it is not exponential...or is it?)

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

We are going to formulate a model using variables and parameters to quantify *how proportial* that relation is. Using our intuition, there are two parameters we will take into account. 

- *$\beta$*: *contact rate* or how many people an infected person comes into contact with in given time
- *$\gamma$*: *recovery rate* or how many people recover in given time

The rate on which people get infected should grow the more contact they have to each other and should decay as they recover. In another words, the rate of change is *positively* proportional to $\beta$ (*contact rate*) and *negatively* proportional to $\gamma$ (*recovery rate*)

Finally, we have our equation as follows,

$$
\begin{equation}
\frac{dI}{dt} = \left(\beta - \gamma\right) I 
\end{equation}
$$

Now let us take some time to check if we can take some conclusions from it. 

If the *recovery rate* is greater than the *contact rate*, the rate of change will always be negative, so the infection will eventually dissipate and even won't outbreak. 

On the other hand, if the *contact rate* is greater the the *recovery rate*, we will have an outbreak. Apparently, those paramaters indicate how strong an epidemic can be.

If $\gamma$ is the *recovery rate*, then $1/\gamma$ is the *infectious/recovery period* or the period of time during which an infected person is sick and then can pass it on.

Consider the product between the $\beta$ and $1/\gamma$. That gives the average number of people an infected patient will pass the infection on. For example, let us say that in a given scenario the *contact rate* is $\beta = 0.2$ and the *infectious/recovery* period is $1/\gamma = 10$ days. Then we expect that each infected patient will pass the infection onto 2 people.

$$
\begin{equation}
R_{0} = \frac {\beta}{\gamma}
\end{equation}
$$

In fact, that indicator is known as the *basic reproduction number*. Note that when $R_0 > 1$ the infection will be able to start spreading in a population, but not if $R_0 < 1$. So that is indeed a very important indicator.

Probably everybody has that number in their minds in the present. When trying to mitigiate the contamination, we will see how important bringing it down is in order to slow down the epidemic.

After the outbreak in China, studies found that COVID-19's basic reproduction number is between [1.4-3.9](https://pubmed.ncbi.nlm.nih.gov/31995857-early-transmission-dynamics-in-wuhan-china-of-novel-coronavirus-infected-pneumonia/), which means that, on avarage, a sick patient transmits the infection to 1.4 and 3.9 others. The *recovery period* is around [10 days](https://www.statnews.com/2020/03/09/people-shed-high-levels-of-coronavirus-study-finds-but-most-are-likely-not-infectious-after-recovery-begins/). 

We solved our equation numerically inputting different parameters to see how they play out.

{% include posts/2020-03-13-why-is-coronavirus-all-about-mathematics/2.html %}
<sub></sub>

We visually check how small decrements *basic reproduction number* will have a huge accumulative gain over time. That is reason why we should take agressive action, either by social distancing, avoiding and cancelling events.

We saw that the *basic reproduction number* depends on *contact rate* and *recovery rate*. Since the *recovery rate* is barely in our control - as it is typicallly a biological charateristic of the virus -, controlling the *contact rate* is our best chance to flatten the curve. That does not mean we should not invest in treatments and in the best case scenario we should bring both down.

### Thou shall not exponentiate!

But here is the plot twist: an epidemic is not purely exponential! Our first model assumed that the infection will spread indefinitely, the population is infinite and there is no immunity or cure. 

Of course, that is nonsense. A rather evil way of think of it is that once the entire population is infected, there is none left to be infected!

Let us address that in a new model by assuming the following,

- fixed population (nobody dying, moving or being born)
- recovery and immunity

In COVID-19's case, [it is not clear how long the protection lasts](https://www.independent.co.uk/life-style/health-and-families/coronavirus-immunity-reinfection-get-covid-19-twice-sick-spread-relapse-a9400691.html). But we will assume it lasts longer than our simulated timeframe.

We will use a model that was first introduced by [Anderson Ogilvy Kermack](https://en.wikipedia.org/wiki/Anderson_Gray_McKendrick) and [Anderson Gray McKendrick](https://en.wikipedia.org/wiki/Anderson_Gray_McKendrick]) called a compartmental model. The idea is to divide the population into group (or *compartments*) and describe how the infection moves from one to another.

Let the SIR model be as follows,

- *S(t)*: susceptible but not yet infected population
- *I(t)*: infectious population
- *R(t)*: recovered population

- *$\beta$*: *contact rate* or how many people an infected person comes into contact with in given time
- *$\gamma$*: *recovery rate* or how many people recover in given time
- *N*: total population 

First, the *equation S* tell us that as the population gets infected, the susceptible population becomes smaller. 

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

Last, the *equation R* says that the recovered population is proportinal to the recovery rate.

$$
\begin{equation}
\frac{dR}{dt} =  \gamma I
\end{equation}
$$

Unfortunately, that system of differential equations is non-linear and does not have analytical solution. Fortunately, we solve it numerically with the following initial conditions,

- *I(0)* = 1 (patient zero)
- *N* = 1.000.000 (population)

{% include posts/2020-03-13-why-is-coronavirus-all-about-mathematics/3.html %}
<sub></sub>

Well...We added all that math...for nothing? Wait for it and zoom out for a moment,

{% include posts/2020-03-13-why-is-coronavirus-all-about-mathematics/4.html %}
<sub></sub>

Now we have it! 

Note that our original model gave us 1.5M for $R_0 = 4.2$, exceeding our total simulated population of 1M. That's nonsense!

Let us see the rest of the solution,

{% include posts/2020-03-13-why-is-coronavirus-all-about-mathematics/5.html %}
<sub></sub>

Once more, we visually check how sensitive those systems are to the *basic reproduction number*.

Just imagine that rather than each infected patient passing the infection onto other $4$ people, we could slow it down to $3$, that would result in a 25% reduction of active cases at the peak. If social distancing from 4 to 2, the peak would be cut in half!

By mitigating the contamination, we will be able to not only to postpone the peak of the outbreak, but to bring the maximum number of active cases the at the peak to a lower ground and then to protect the most vulnerable by making them less susceptible and giving people the chance to get proper treatment.

{% include posts/2020-03-13-why-is-coronavirus-all-about-mathematics/6.html %}
<sub></sub>

Another important point to make is that our resources, like healthcare and food supply chain, are limited and not lowering the peak of infection could stress them to a point where they could not operate, leading to catastrophe.

### Herd immunity

<blockquote>
Herd immunity (also called herd effect, community immunity, population immunity, or social immunity) is a form of indirect protection from infectious disease that occurs when a large percentage of a population has become immune to an infection, thereby providing a measure of protection for individuals who are not immune
</blockquote>

I will let the numbers talk. Assuming that 50% of the polulation is immune/vaccinated initially,

{% include posts/2020-03-13-why-is-coronavirus-all-about-mathematics/8.html %}
{% include posts/2020-03-13-why-is-coronavirus-all-about-mathematics/9.html %}

and even in the event of the apocalypse,

{% include posts/2020-03-13-why-is-coronavirus-all-about-mathematics/10.html %}
{% include posts/2020-03-13-why-is-coronavirus-all-about-mathematics/11.html %}


<br>
That's why Coronavirus all about Mathematics. As Euler once wrote, "nothing whatsoever takes place in the universe in which some relation of maximum and minimum does not appear.".

*If you enjoyed this story, please feel free go the [code](https://github.com/g4brielvs/COVID-19/blob/master/2020-03-11-gs-covid19.ipynb) or launch the [notebook](https://mybinder.org/v2/gh/g4brielvs/COVID-19/master?filepath=2020-03-11-gs-covid19.ipynb).*

