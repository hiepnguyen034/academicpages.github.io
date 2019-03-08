---
title: Stochastic Processes as Monad Transformers
author: Rafael S. Calsaverini
date: 2019-03-08
permalink: /posts/2019/03/stochastic-processes
category: programming
tags:
  - Haskell
  - Monad Transformers
  - Monads
  - Stochastic Processes
  - Probability Monad
---

Now, stochastic processes have characteristics related to two different monads. In one hand, they are dynamical processes, and the way to implement dynamics in Haskell is with state monads. For example, if I want to iterate the logistic map:

$$x_{t+1} = \alpha x_t\left(1-x_t\right)$$

I could do the following:

```haskell
  f :: Double -> Double
  f x = 4*x*(1-x)

  logistic :: State Double Double
  logistic = do x0 <- get
        let x1 = f x
        put x1
        return x1
  runLogistic :: State Double [Double]
  runLogistic n x0= evalState (replicateM n logistic) x0
```

Running this on ghci would give you, for example:

```haskell
  *Main> runLogistic 5 0.2
  [0.6400000000000001,0.9215999999999999,0.28901376000000045, 0.8219392261226504,0.5854205387341]
```

So we can make the loose correspondence: dynamical system ? state monad.

On the other hand, stochastic processes are compositions of random variables, and this is done with the Rand monad (found in `Control.Monad.Random`). As an example, the Box-Muller formula tells us that, if I have two inpendent random variables $x$ and $y$, distributed uniformly between in the \\([0, 1]\\) interval, then, the expression:

$$\sqrt{-2\log(x)}\cos(2\pi y)$$
