---
layout: post
title: Neural Network [grade 2]
---

## Neural Network
##### grade 2: single perceptron with linear classification

Subject for grade 2 is to develop a linear classification with single perceptron.

We will commence a classification problem: linearly split within a 2D space.

<img src="{{site.url}}/img/nn004.png" width="500px">

As showed in above picture, green and blue stands for 2 classes, the red lines represent 4 different scenarios in classification.

To solve problem of "linear classification", 1 perceptron could perform this task.

The network structure remain unchanged with grade 1:

<img src="{{site.url}}/img/nn001.png" width="500px">

Classification is a typical "supervised learning" in machine learning, which means machine's performance on predict objects will be measured all the time. When we are saying performance, usually we are talking about the degree of errors.

Let's review data we played with:
* inputs (2 inputs, reason of 2 is which could be easily mapped to the 2D space by transfer them to x and y coordinates);
* weights (initialized by random between 0 to 1);
* outputs (use the sign function to generate -1 and 1);

The object here is to accept any of inputs, make the perceptron outputs the rights classification, say "-1" and "1".
Thus data we could manipulate here is : weights.
How do we refine the magic weights, make those help the perceptron doing the right thing?

<img src="{{site.url}}/img/nn011.png" width="500px">

Just like driving, we wanna make sure that the car is heading the right direction. Here the direction or hint was gave by "error measurement".

Actual | Predict | Actual - Predict
--- | --- | ---
1 | 1 | 0
1 | -1 | 2
-1 | -1 | 0
-1 | 1 | -2

These are the scenarios on perceptron's prediction, total in 4.
Specifically, line 2 and line 4 are the perceptron making errors, and here we use a simple equation to describe how big is an error:

```
    Error = Actual - Predict
```

As we discussed, weights are the key to help perceptron does the right thing, here we present the key method in manipulate weights:

```
    Weights = Errors * Inputs * Learning_rate

```

Learning_rate is one of a hyper-parameters in neural network, which impacts the "speed of learning", in simple, we could take it as the degree that the current weights will yield to the current errors.

<img src="{{site.url}}/img/nn002.png" width="500px">

The process of:
Compare outputs with actual class, get the degree of errors, passed errors back to input layer, adjust weights accordingly is called: back propagation, or training (tweak outputs according to training data given). By doing this process, the neuron perceptrons are really learning from errors.

The coding part:
On top of predict function in grade 1, we will add another training function within perceptron class:

```



```




<img src="{{site.url}}/img/nn003.png" width="500px">

<img src="{{site.url}}/img/nn005.png" width="500px">


[Codes on github  https://github.com/hifreedo/nnfs](https://github.com/hifreedo/nnfs)




#### Math been invoked in this grade:

```

```



#### To be continued in Grade 3:


[half done]
