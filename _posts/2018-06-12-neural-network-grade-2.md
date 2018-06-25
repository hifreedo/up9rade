---
layout: post
title: Neural Network [grade 2]
---

# Neural Network

## grade 2: single perceptron with linear classification

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
Thus the data we could manipulate here is : weights.
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

Let's take a look at an simple example:
Following is a feed forward process, 2 inputs are 0.5 and 1, 2 randomly assigned weights: 0.1 and -0.5, the perceptron generates output of -1.

Inputs | Original weights | Sum(inputs * weights) | Sign outputs
--- | --- | --- | ---
0.5 | 0.1 | 0.5 * 0.1 |
1 | -0.5 | 1 * -0.5|
 | | 0.05 - 0.5 | -1

Now assume we are expecting the output of "1" instead of "-1", let's see how the back propagation impacts weights:

Errors | Inputs | Learning_rate | New Weights | Original weights
--- | --- | --- | --- | ---
1 - (-1) | 0.5 | 1 | 2 * 0.5 * 1 | 0.1
1 - (-1) | 1 | 1 | 2 * 1 * 1 | -0.5

Under the original weights combination, 0.1 and -0.5, gave the output of -1.
Through back propagation, they were been tweaked into 1 and 2. They were increased especially for the latter: -0.5 was punished, from negative to positive value, aka, the direction of impact was changed.

（Note: "1" is not the usual value for learning rate, we will take a much smaller learning rate in practical. ）

Now let's cook the coding part:
On top of predict function in grade 1, we will add another training function within perceptron class in processing:

```processing
class Perceptron {
  float[] weights;
  float learning_rate = 0.01;

  // Constructor, takes in # of weights and initialize
  Perceptron(int n) {
    weights = new float[n];
    for (int i = 0; i < weights.length; i++) {
      weights[i] = random(-1, 1);
    }
  }

  // Generate outputs
  int predict(float[] inputs) {
    float sum = 0;
    for (int i= 0; i < weights.length; i++) {
      sum += inputs[i] * weights[i];
    }
    int predict = sign(sum);
    return predict;
  }

  // training
  void training(float[] inputs, int label, int predict ) {
    int error = label - predict;
    for (int i = 0; i < weights.length; i++) {
      weights[i] += error * input[i] * learning_rate;
    }
  }

  // Activate function
  int sign(float sum) {
    if (sum >= 0) {
      return 1;
    } else {
      return -1;
    }
  }

}

```

<img src="{{site.url}}/img/nn003.png" width="500px">

<img src="{{site.url}}/img/nn005.png" width="500px">

[Codes on github  https://github.com/hifreedo/nnfs](https://github.com/hifreedo/nnfs)


<img src="{{site.url}}/img/nn_g2.gif" width="500px">

#### Math been invoked in this grade:

```

```



#### To be continued in Grade 3:


[half done]
