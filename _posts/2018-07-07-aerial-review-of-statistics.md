---
layout: post
title: Aerial view of statistics
---

# Aerial view of statistics

## Statistics is about change mind with math.

We are dealing with uncertainties everyday, are the samples/ occurances as we wish or on the contrary, will happen all the same (apply to whole population)? The traffic, weather, gambling, every piece of our life contains probabilities.

 -- | Bayesian | Frequentist
 --- | --- | ---
 focus on | Change Belief | Change Action
 result | credible intervals | confidence coefficient
 example | Winning chance: 40% ~ 60% | 55% chance, all in

Though bayesian treats the world in a more "rational" way, frequentist are more popular nowadays, maybe due to people doesn't like this kind of uncertainty either.

A typical way of statistics:

1. Make hypotheses
2. Collect supportive data
3. Check power of data
4. Test hypotheses

Assume your friend is making a bet with you, the winner is going to get 100$. The rule is simple, flip a coin, if it's up, you win. Otherwise, you lose. But wait, the coin offered by your friend, which you have never seem such type before.

Is there any cheating? There are 2 hypothesis come to your mind naturally:

## Make hypotheses, describe probabilities of the world

hypothesis | description
--- | ---
null hypothesis | the coin is a normal one as usual
alternative hypothesis | the new coin is abnormal

## Collect supportive data, which provides evidence to hypothesis

Agreed or not, you took the coin and made some experiments alone. Under the pushy of your friend, you made 5 flips, got 5 times of tail.

## Check power of data, does it provides enough evidence

Is 3 or 5 flips enough? Should you try more times to verify the hypothesis? Power analysis is a way to check how much power you will get among the collected data. The power is about to take you away from the null / default hypothesis, after all, it's pretty easy to not to accept any alternatives by doing nothing.

## Test hypotheses, see what will you get and avoid making errors

As conclusion of testing process, you will either stick to original / null hypothesis, reject the alternative, which means there's no new thing found or learned. Or you will accept the alternative and reject the null hypothesis, yes, you found it, someone's cheating.

### P-value plays the key role of indicating accept or reject null hypothesis

P-value indicates how surprising the evidence looks, if you stick to null hypothesis. Usually we compare the P-value to a significant level, which is a threshold of 0.05, a conventional number. P-value of 0.05 means, give 100 chances, there will be only 5 shots, very unlikely to be happen in null hypothesis world. The less p-value is, the likely you should reject null hypothesis.

Back to the story, now let's do the calculation:

$$P_{5tails} = \cfrac{1}{2} * \cfrac{1}{2} * \cfrac{1}{2} * \cfrac{1}{2} * \cfrac{1}{2} = 0.03125$$

Which means, the probability is extremely small(between range 0 to 1), of getting a five tails with a normal coin. So, you are going to reject the null hypothesis and accept alternative one.

Last but not least, we are distilling evidence from data, data could be dirty, we are human, human make mistakes. What if we are wrong? Well, there are 2 types for errors with different of names of probabilities: 

Null hypothesis | Accept | Reject | Error explanation | Error probability
--- | --- | --- | --- | ---
True | Correct | Type I error | Changing ur mind when shouldn't | $\alpha$
False | Type II error | Correct | Not change ur mind when u should | $\beta$

Usually, type I error is worse, consider about what talked above, we did a lot of work, which leads us to the wrong way. We could have been sitting there doing nothing and stick to the correct original way.

On the flipping coin story, you may jump to conclusions with only 1 flip, or 2, obviously that will leads to errors. With more flips, say 100 even 1000, you will have more confidence on not making type I or type II errors, because you have more evidence on hands.

No wonder, till today, deep learning is still a labor work of dealing with more data.


[post status: half done]