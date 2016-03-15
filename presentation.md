% Numerical Simulation 
% Assignment 2
% Daniel Dimitrov, Tilburg University

Introduction
================

---------

The Brownian Motion, a.k.a. Wiener process, is a foundational block in quantitative finance 


Used extensively for 
---------

    - Pricing of Derivative Products
    - Risk Management and Hedging
    - Portfolio Construction

Basic Definition
================

---------

A *Wiener process* ${W_t}$ in continous time satisfes the following properties for $t\geq0$.

(i) $W_0 = 0$.
(ii) If $t_1<t_2\leq t_3<t_4$, then the increments 
$W_{t_2}-W_{t_1}$ and $W_{t_4} - W_{t_3}$ are independent.
(ii) For any given $t_1$ and $t_2$ with $t_2 > t_1$, the increment 
$W_{t_2}-W_{t_1}$ is normally distributed with mean $0$ and variance $t_2-t_1$.

Details are available in the course script Financial Models by Prof. Dr. J.M.Schumacher.


Asmnt Part A: Simulation of Brownian Motion Paths 
=================

---------

Plot two sample paths of a discrete-time standard random walk. That is, plot
two trajectories of the process defned by the recursion $X_{k+1} = X_k + Z_k$ where
$X_0 = 0$ and the $Z_k$'s are independent standard normal variables. Take 200 steps.

---------

The MATLab function $cumsum$  helps avoid generating a time loop. 

MATLAB Code
---------

```
N=200; %number of steps
%initial values for the paths

path1(1)=0;
path2(1)=0;

%generating the paths
path1(2:N+1)=cumsum(randn(N,1));
path2(2:N+1)=cumsum(randn(N,1));

%output
figure 
hold on
plot([0:1:200],path1)
plot([0:1:200],path2,'r')
xlabel('Steps')
legend('path1','path2')
```

----------

Here are two Brownian Motion Paths
----------

![](images/asmtA_Brownian.jpg)

Asmnt Part B: Covaraience of overlaping motions 
=================

---------

Let $W_t$ be a Wiener process. Show that 

$$Cov(W_{t_1} ;W_{t_2}) = min(t_1; t_2)$$

For every step in your reasoning, indicate which property of the Wiener process you use.

----------

Solution
----------

- Assume that $t_0 < t_1 < t_2$ where $t_0=0$. 

- Then we can consider that
 
$W_{t_1}=W_{t_1}−W_{t_0})$ 

$W_{t_2}=(W_{t_1}-W_{t_0})+(W_{t_2}-W_{t_1})$ where $W_{t_0}=0$ from property (i) of a Wiener process. 


----------

What we did so far is to show that each of the random variables can be written as Brownian Motion increments. 
Those increments are 

- independent due to (ii) 
- normally distributed due to (iii), 
- with zero mean 
- variance that is equal to the time interval between the two random variables. 

----------

What we have is that $W_{t_0}=0$, $W_{t_1}\sim N(0,t_1)$ and $W_{t_2}-W_{t_1}\sim N(0,t_2-t_1)$

The sum of two independent and normally distributed random variables is 
- normally distributed 
- with variance equal to the sum of the variances of the initial random variables:

\implies  $$W_{t_2}\sim N(0,t_2)$$

----------

Working out the math we have


$$Cov(W_{t_1},W_{t_2})\\
=E(W_{t_1}W_{t_2})-E(W_{t_1})E(W_{t_2})\\
=E(W_{t_1}W_{t_2})=E(W_{t_1}(W_{t_1}+(W_{t_2}-W_{t_1}))\\
=E((W_{t_1})^2)+E((W_{t_1}(W_{t_2}-W_{t_1}))\\
=E((W_{t_1})^2)+E(((W_{t_1}-W_{t_0})(W_{t_2}-W_{t_1}))\\
=E((W_{t_1})^2)=Var(W_{t_1})=t_1$$


----------

Analogously, for $t_0<t_2<t_1$, then $Cov(W_{t_1},W_{t_2})=E(W_{t_2}^2)=t_2$.

Conclusion
----------

$$Cov(W_{t_1},W_{t_2})=min(t_1,t_2)$$.
