---
layout: post
title: Magic in algorithm implementation
---

# Magic in algorithm implementation

It's quite common when you get stuck in algorithm implementation, no matter how hard tried, it just doesn't converge.

There's a good line in the classic "Matrix" movie: Sooner or later, you are going to realize, it's different between knowing the path and walking the path.

Whenever get stuck, it's a good chance to understand deeper, learn more.

Among these takeaways, a piece of interesting part is: implementing algorithm is not like the analogy of building, a whole building won't collapse because of a small brick was not in place, but the prior does.

Let's initiate with 2 samples, and sure the list will grow: 

## case 1: leave out the plus sign

In a [simple neuron network]({{site.url}}/2018/06/12/neural-network-grade-2.html), when doing the training part, we are trying to get the right "weight" as described below:

$$Weight += Error * Learning_rate * Input$$

Here, a small "+" sign was leave out, and in a consequence, the weight parameter won't converge, as every time doing the training, it starts from a fresh, instead of standing on previous weights' tuning basis.
Leave the "+" out, there won't be any "error" or "warning" generated from your program, it just doesn't converge.

## case 2: leave out the bracket notation

This is a language specific case:

```python
import numpy as np
threshold = 0.1
rand = np.random.random
if rand < threshold:
    do_something()

```

The program will run with no error or warnings under python 2.7 version, except the "do_something()" will never be executed.

The "np.random.random" is a python builtin method or function, the "np.random.random()" is a "float". The error is quite covert as the program does not throw out any warning or error message.

This might not be a perfect case to emphasize importance of a single notation, cases like leave out brackets are also quite common in formulas. We will try to come up with more later.