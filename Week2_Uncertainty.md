# Uncertainty - CS50AI Lecture 2

## Probability Theory:

In a dice, there are 6 possible worlds: 1, 2, 3, 4, 5, and 6. Each world has a probability of being true and we can represent both the world and its probability by doing the following.

<img src="https://render.githubusercontent.com/render/math?math=\omega"> -> A possible world  
<img src="https://render.githubusercontent.com/render/math?math=\Omega"> -> The probability of world 
<img src="https://render.githubusercontent.com/render/math?math=\omega"> being true where  
0 ≤ P(<img src="https://render.githubusercontent.com/render/math?math=\omega">) ≤ 1.

The sum of all _P(<img src="https://render.githubusercontent.com/render/math?math=\omega">)_ has to be equal to 1. Logically, this tells us that something thing will be true. In the dice example, it is guaranteed that we will get a number 
<img src="https://render.githubusercontent.com/render/math?math=x"> where 
1 ≤ <img src="https://render.githubusercontent.com/render/math?math=x"> ≤ 6. We can represent this with the equation:

![$\sum_{\omega \in \Omega} P(\omega) = 1$](https://render.githubusercontent.com/render/math?math=%24%5Csum_%7B%5Comega%20%5Cin%20%5COmega%7D%20P(%5Comega)%20%3D%201%24)

Tthe sum of the probabilities of all possible worlds will be equal to 1.

In a more complex model, it's not always the case that each world is equally as likely.  
Example:  
![dice](images/2_Uncertainty/dice.png)

In this example, although each world is equally likely(a combination of dice rolls), the sum of the rolls are not.
There are 6 possible worlds where 7 is the sum but only 1 possible world where the sum is 12. We can represent this using the following.

<img src="https://render.githubusercontent.com/render/math?math=$P(12) = \frac{1}{36}$"> Only 1 out of the 36 worlds have a sum of 12.  
<img src="https://render.githubusercontent.com/render/math?math=$P(7) = \frac{6}{36} = \frac{1}{6}$"> 6 worlds have a sum of 12.

## Unconditional Probability:

Degree of belief in a proposition in the absence of any other evidence.

## Conditional Probability:

Degree of belief in a proposition given some evidence that has already been revealed.

Probability that
<img src="https://render.githubusercontent.com/render/math?math=a"> is true given
<img src="https://render.githubusercontent.com/render/math?math=b">.  
<img src="https://render.githubusercontent.com/render/math?math=$P(a | b)$"> 

All cases where a and b are true with the exception of b being true.
<p align="center">
  <img src="https://render.githubusercontent.com/render/math?math=P(a | b) = \frac{P(a \verb|∧| b)}{P(b)}">
</p> 
or, 
<p align="center">
  <img src="https://render.githubusercontent.com/render/math?math=P(a \verb|∧| b) = P(a | b)*P(b)">
</p> 

Example: In the image above, the probability of the sum being 12 given a red die with value 6.

<img src="https://render.githubusercontent.com/render/math?math=$a = 12$">: the a value in the above equation is 12.  
<img src="https://render.githubusercontent.com/render/math?math=$b = r6$">: the b value in the above equation is a red 6 die.

First, the probability of red being 6 is <img src="https://render.githubusercontent.com/render/math?math=$\frac{6}{36} = \frac{1}{6}$">. Next, we need the probability of both _a_ and _b_ being true which is <img src="https://render.githubusercontent.com/render/math?math=$\frac{1}{36}$"> because only 1 world has a sum of 12 with red being 6. Finally, we divide these two to get the probability of both _a_ and _b_ being true.

<img src="https://render.githubusercontent.com/render/math?math=$P(a | b) = \frac{\frac{1}{36}}{\frac{1}{6}} = \frac{1}{6}$"> <br>
Therefore, given that the red die rolled 6, the probability of the sum being 12 is <img src="https://render.githubusercontent.com/render/math?math=\frac{1}{6}">.

## Random Variables:

A variable in porbability that has a domain of values that it can be

Ex: _Roll = {1, 2, 3, 4, 5, 6}_    
Ex: _Weather = {sum, cloud, rain, wind, snow}_  
Ex: _Traffic_ = _{none, light, heavy}_  
Ex: _Flight = {on time, delayed, cancelled}_  

### Probability Distribution:

Ex: _P_(_Flight_ = _on time_) = 0.6  
Ex: _P_(_Flight_ = _delayed_) = 0.3  
Ex: _P_(_Flight_ = _cancelled_) = 0.1

This can be represented using a vector: A sequence of values(interpreted in order).  
**P**(_Flight_) = <0.6, 0.3, 0.1>

## Independence:

The knowledge that one event occurs does not affect the probability of other events.  
Ex: The red die roll does not influence the blue die roll.  
Ex: Clouds and rain are most likely not independent.

If independent,  
<img src="https://render.githubusercontent.com/render/math?math=$P(a \verb|∧| b) = P(a)*P(b)$">

Example of Independence:  
<img src="https://render.githubusercontent.com/render/math?math=$P(red6 \verb|∧| blue6) = P(red6)*P(blue6) = \frac{1}{6} * \frac{1}{6} = \frac{1}{36}$">

Example of Non-Independence:  
<img src="https://render.githubusercontent.com/render/math?math=$P(red6 \verb|∧| red4) \neq P(red6)*P(red4)$  ">

There is no way you can get 4 if you get 6. Therefore the event that red rolls 6 and the event that red rolls 4 are non-independent. If one of them occurs, the other is guaranteed not to occur on that specific roll.

## Bayes' Rule:

### Derivation:

Given:
<p align="center">
  <img src="https://render.githubusercontent.com/render/math?math=$P(a \verb|∧| b) = P(a | b)*P(b)$">
</p>  
and
<p align="center">
  <img src="https://render.githubusercontent.com/render/math?math=$P(a \verb|∧| b) = P(b | a)*P(a)$">
</p> 
We can use substitution to derive Bayes' Rule.
<p align="center">
  <img src="https://render.githubusercontent.com/render/math?math=$P(b | a)*P(a) = P(a | b)*P(b)$">
</p>    
Divide by P(a) to get: 
<p align="center">
  <img src="https://render.githubusercontent.com/render/math?math=$P(b | a) = \frac{P(a | b)*P(b)}{P(a)}$">
</p>

This is useful when one probability is easier to know than another probability. Knowing _P(visible effect | unknown cause)_, we can calculate _P(unkown cause | visible effect)_.

## Joint Probability:

**AM:** 
| _C = cloud_   | _C = ¬cloud_  |
| ------------- | ------------- |
|      0.4      |      0.6      |

**PM:**  
| _R = rain_   | _R = ¬rain_   |
| ------------ | ------------- |
|     0.1      |      0.9      |


**AM & PM:**
|              | _R = rain_   | _R = ¬rain_   |
| ------------ | ------------ | ------------- |
| _C = cloud_  |     0.08     |     0.32      |
| _C = ¬cloud_ |      0.02    |      0.58     |

Probability of clouds given it is raining(`,` and `∧` are used interchangably).
<p align="center">
  <img src="https://render.githubusercontent.com/render/math?math=$P(C | rain) = \frac{P(C, rain)}{P(rain)} = \alpha P(C, rain)$">
</p>  

Conditional distribution of <img src="https://render.githubusercontent.com/render/math?math=$P(C | rain)$"> is proportional to the joint probability of <img src="https://render.githubusercontent.com/render/math?math=$\alpha P(C, rain)$"> where <img src="https://render.githubusercontent.com/render/math?math=$\alpha$"> = <0.08, 0.02>(cloud probability given it's raining). Equivalently, <img src="https://render.githubusercontent.com/render/math?math=$\alpha$"> = <0.8, 0.2> to reach a sum of 1.

### Negation:

<img src="https://render.githubusercontent.com/render/math?math=$P(\verb|¬|a) = 1 - P(a)$">

The probability of _¬a_ happening is 1 - the probability of _a_ happening.

### Inclusion-Exclusion:

![$P(a \verb|∨| b) = P(a)+P(b) - P(a \verb|∧| b)$](https://render.githubusercontent.com/render/math?math=%24P(a%20%5Cverb%7C%E2%88%A8%7C%20b)%20%3D%20P(a)%2BP(b)%20-%20P(a%20%5Cverb%7C%E2%88%A7%7C%20b)%24)

The probability of _a_ or _b_ being true is the the probability of _a_ being true plus the probability of _b_ being true - the probability of both _a_ and _b_ being true.

### Marginalization:

![$P(a) = P(a, b) + P(a, \verb|¬|b)$](https://render.githubusercontent.com/render/math?math=%24P(a)%20%3D%20P(a%2C%20b)%20%2B%20P(a%2C%20%5Cverb%7C%C2%AC%7Cb)%24)

This formula helps find the probability of _a_ using some other information like _b_. Either _b_ is true or _b_ is not true but the probability of _a_ being true is the sum of both these cases. Sometimes _b_ could take the form of a random variable where there are multple possible values. Now, we have to sum up all the possible values that _b_ could take. This can be represented as follows:

<p align="center">
  <img src="https://render.githubusercontent.com/render/math?math=$P(X = x_i) = \sum_{j} {P(X = x_i, Y = y_i)}$">
</p> 

### Conditioning:

![$P(a) = P(a | b)P(b) + p(a|\verb|¬|b)P(\verb|¬|b)$](https://render.githubusercontent.com/render/math?math=%24P(a)%20%3D%20P(a%20%7C%20b)P(b)%20%2B%20p(a%7C%5Cverb%7C%C2%AC%7Cb)P(%5Cverb%7C%C2%AC%7Cb)%24)

Similar to margininalization except it uses conditional probability instead of joint probability. Again, there is a version of conditioning that can be applied to random variables.

<p align="center">
  <img src="https://render.githubusercontent.com/render/math?math=$P(X = x_i) = \sum_{j} {P(X = x_i | Y = y_i)P(Y = y_i)}$">
</p>

The above basically means given variable _Y_, what is the probability that it takes on state <img src="https://render.githubusercontent.com/render/math?math=$y_i$">. We then multiply this by the probability of _X_ taking on the state <img src="https://render.githubusercontent.com/render/math?math=$x_i$"> given _Y_ took on state <img src="https://render.githubusercontent.com/render/math?math=$y_i$">.

## Bayesian Network:

Data structure that represents the dependencies among random variables.

- Directed graph
- Each node represents a random variable
- Arrow from _X_ to _Y_ means _X_ is a parent of _Y_
- Each node _X_ has probabillity distribution: <img src="https://render.githubusercontent.com/render/math?math=$P(X|Parents(X))$">

Example:  
![BayesianNetworkExample](images/2_Uncertainty/bayesianNetwork.png)

Description:

**Appointment**: Dependent on Train(1 arrow pointing to it)  
**Train**: Dependent on maintenance and Rain(2 arrows pointing to it)  
**Maintenance**: Dependent on Rain(1 arrow pointing to it)  
**Rain**: Not dependent on anything(no arrows pointing to it)

**Using Bayesian Networks:**

Let's say we wanted to find _P(light, no, delayed, miss)_.  
Maintenance is dependent on rain so we write the probability of maintence taking on the value of _no_ as _P(light)*P(no | light)_.  
The train is dependent on both Rain and Maintenance so we add both `light, no` to the previous expression to get   
_P(light)*P(no | light)*P(delayed | light, no)_.  
Ultimately, appointment is only dependent on the Train so we add another segment to get the probability of   
_P(light, no, delayed, miss)_:  

<img src="https://render.githubusercontent.com/render/math?math=$P(light)*P(no | light)*P(delayed | light, no)*P(miss | delayed)$">

## Inference:

- Query _X_: variable for which to compute distribution.
- Evidence variables _E_: observed variables for event _e_.
- Hidden variables _Y_: non-evidence, non-query variables.

Goal: Calculate <img src="https://render.githubusercontent.com/render/math?math=$P(X|e)$">

Let's say we wanted to find <img src="https://render.githubusercontent.com/render/math?math=$P(Appointment | light, no)$">  

Query: _Appointment_  
Evidence: _light_, _no_  
Hidden: _Train_  

We know that a conditional probability is equiavalent to <img src="https://render.githubusercontent.com/render/math?math=$\alpha$"> times joint probability. 
<p align="center">
  <img src="https://render.githubusercontent.com/render/math?math=$P(Appointment | light, no)$">
</p>
<p align="center">
  <img src="https://render.githubusercontent.com/render/math?math=$ = \alpha P(Appointment, light, no)$">
</p>  
Either the train is on time, or the train is delayed:  

![$ = \alpha \[P(Appointment, light, no, on-time)\] + P(Appointment, light, no, delayed)$](https://render.githubusercontent.com/render/math?math=%24%20%3D%20%5Calpha%20%5BP(Appointment%2C%20light%2C%20no%2C%20on-time)%5D%20%2B%20P(Appointment%2C%20light%2C%20no%2C%20delayed)%24)

### Inference by Enumeration:

<p align="center">
  <img src="https://render.githubusercontent.com/render/math?math=$P(X | e) = \alpha P(X, e) = \alpha \sum_{y} {P(X, e, y)}$">
</p>

_X_ is the query variable.  
_e_ is the evidence.  
_y_ ranges over values of hidden variables.  
<img src="https://render.githubusercontent.com/render/math?math=$\alpha$"> normalizes the result.

## Sampling:

### Conditional Sampling:

Randomly choose a world for one of the random variables. Every variable from that point is chosen based on this value. Now, if we run this sampling simulation many many times, we can choose the results where the query is true and estimate the probability rather than computing every possible case.

### Unconditional Sampling:

This works similar to conditional sampling except we reject the worlds where the evidence is not satisfied and choose the ones where it is.

**Problems with Sampling**: If a world is very unlikely to occur, a lot of computation is wasted.

### Likelihood Weighting:

- Start by fixing the values for evidence variables
- Sample the non-evidence variables using conditional probabilities in the Bayesian Network
- Eight each sample by its **likelihood**: the probability of all the evidence.

## Markov Model:

### Markov Assumption:

The assumption that the curent state depends on only a finite fixed number of previous states.

### Markov Chain:

A sequence of random variables where the distribution of each variable follows the Markov assumption.  
![markovChainExample](images/2_Uncertainty/markovChain.png)  

**Transition Model:** Transition from one state to another state.

Given today's weather, predict tomorrow's weather. Use tomorrow's weather to predict the day after's weather and so on...

## Hidden Markov Model:

A Markov model for a system with hidden states that generate some observed event.  
Sensor Model:  
![hiddenMarkov](images/2_Uncertainty/hiddenMarkovModel.png)  
In this case, we aren't directly observing umbrellas but we are using sun and rain to predict something that is "hidden."

### Sensor Markov Assumption:

The assumption that the evidence variable depends only on the corresponding state.

**Filtering**: Given observations from start until now, calculate probability for the current state.  
**Prediction**: Given observations from start until now, calculate probability for a future state.  
**Smoothing**: Given observations from start until now, calculate probability for a past state.  
**Most Likely**: Given observations from start until now, calculate most likely sequence of states.