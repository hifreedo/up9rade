---
layout: post
title: Neural Network [grade 5]
---

# Neural Network solving mnist

## grade 4: Mini version of mnist classification

The mnist solving is a big milestone for neural network practice in real field.

We will present a workable mini version, in this version, the main items and challenges will be went through.

To get started, you will need to download mnist dataset in csv format, the dataset is pretty easy to be found online. There are 2 csv files: 1 for training, 60k images in toal, and 1 for test, 10k images. Each line represents an image, 785 columns in total, 1st number denotes a label (from 0 to 9), the following 784 numbers denote the 28*28 pixels image.

The core part: "train function" in neural network as following, is no more than 20 lines of code.
Yet with these 20 lines, in 30 epochs, the model could achieve up to 97.76% accuracy in training set, which means among 10,000 images, only 240 images was misclassified.

This is quite amazing result, the back propagation algorithm is easy to understand and not difficult to implement, yet could achieve better classification result than the other algorithms, such as: SVM, KNN, Random Forest etc.

To achieve above performance of 97.6% in the mini 2 layers' network (1 hidden layer and 1 output layer, we do not count the input layer in, because it won't participate in the calculation), you will need to pay attention to the following key points, otherwise you won't be able to reproduce, or even could not make the network work in a reasonable way.

Key points:

* [Feature scaling](https://en.wikipedia.org/wiki/Feature_scaling) , scale the training data from (0 to 255) to (0 to 1). Take the simple min max normalization, is to divide by 255 to each number.
* Weights distribution, to make sure the random assigned weights to the input nodes and hidden nodes, are aligned with standard normal distribution, they should have positives and negatives, instead of common mistakes: all positive or all in 0 to 1.
* Reasonable network structure and hyper parameters: the input and output nodes are fixed numbers, 784 and 10. The hidden layer nodes are suggested to take a number between 100 to 400, it's a balance need to make between efficiency and accuracy. You might make a network with 1000 hidden nodes work and yield good performance, but which will take way longer time to train. As the learning rate, suggestion is to tune around 0.1.

When we have a fixed depth neural network, it seems better performance still could be achieved by increasing width of network, even have number of nodes from middle layer bigger than number of input nodes, for e.g. set the hidden layer nodes 1000 compares to inputs of 784.
And of course, the training time is dramatically increased.  

Towards current network structure： a large net (from width perspective, slightly bigger than input nodes) might give you some good, only if you could bare with training cost. A large learning rate, greater than 1, definitely could not supply any of goods on both performance and efficiency.

And you might also take this into consideration, what will the accuracy be after run many epochs if we set the learning rate as negative value?

```python
# mnist mini version

%matplotlib inline
import numpy as np
import matplotlib.pyplot as plt

# prepare data
img_size = 28
img_pixel = 28*28
num_label = 10

train_set = np.loadtxt("dataset/mnist/mnist_train.csv", delimiter=",")
test_set = np.loadtxt("dataset/mnist/mnist_test.csv", delimiter=",")

train_label, train_img = np.asfarray(train_set[:, :1]), np.asfarray(train_set[:, 1:]) / 255
test_label, test_img = np.asfarray(test_set[:, :1]), np.asfarray(test_set[:, 1:]) / 255

one = np.arange(num_label)
train_label_onehot = (one == train_label).astype(np.float)
test_label_onehot = (one == test_label).astype(np.float)

# review data
for i in range(10):
    data = train_img[i].reshape(28, 28)
    plt.imshow(data)
    plt.show()

def sigmoid(x):
    return 1 / (1 + np.exp(-x))

def dsigmoid(x):
    return x * (1 - x)

class NeuralNetwork():
    def __init__(self, _num_in_nodes, _num_hidden_nodes, _num_out_nodes, _lr, _activate, _dactivate, _bias=1):
        self.num_in_nodes = _num_in_nodes
        self.num_hidden_nodes = _num_hidden_nodes
        self.num_out_nodes = _num_out_nodes
        self.lr = _lr
        self.activate = _activate
        self.dactivate = _dactivate
        self.bias = _bias
        
        # init weights, +1 is the bias node
        self.wih = np.random.randn(self.num_hidden_nodes, self.num_in_nodes + 1)
        self.who = np.random.randn(self.num_out_nodes, self.num_hidden_nodes + 1)
        
    def train(self, inputs, labels):
        # calcuate output and errors
        inputs = np.concatenate((inputs, [self.bias]))      
        inputs = np.array(inputs, ndmin=2).T
        labels = np.array(labels, ndmin=2).T
        
        hidden_layer = np.dot(self.wih, inputs)
        hidden_layer = self.activate(hidden_layer)
                
        hidden_layer = np.concatenate((hidden_layer, [[self.bias]]))
        output_layer = np.dot(self.who, hidden_layer)
        output_layer = self.activate(output_layer)
        
        output_errors = labels - output_layer
        
        # start backpropagation for who      
        gradients = output_errors * self.dactivate(output_layer)
        gradients = self.lr * gradients
        who_delta = np.dot(gradients, hidden_layer.T)
        
        self.who += who_delta
        
        # backpropagation for wih
        hidden_errors = np.dot(self.who.T, output_errors)
        gradients = self.dactivate(hidden_layer)
        gradients = hidden_errors * gradients
        gradients = self.lr * gradients
        wih_delta = np.dot(gradients, inputs.T)[:-1, :]
        
        self.wih += wih_delta
        
    def run(self, inputs, labels, epochs=1):
        # multiple runs
        for epoch in range(epochs):
            for i in range(len(inputs)):
                self.train(inputs[i], labels[i])
    
    def predict(self, inputs):
        # generate output based inputs
        inputs = np.concatenate((inputs, [self.bias]))
        inputs = np.array(inputs, ndmin=2).T
        hidden_layer = np.dot(self.wih, inputs)
        hidden_layer = self.activate(hidden_layer)
        
        hidden_layer = np.concatenate((hidden_layer, [[self.bias]]))
        output_layer = np.dot(self.who, hidden_layer)
        output_layer = self.activate(output_layer)
        
        return output_layer
    
    def evaluate(self, inputs, labels):
        # evaluate result
        correct, wrong = 0, 0
        for i in range(len(inputs)):
            res = self.predict(inputs[i])
            res_max = res.argmax()
            if res_max == labels[i]:
                correct += 1
            else:
                wrong += 1
        return correct, wrong        
        
_activate = sigmoid
_dactivate = dsigmoid
_num_in_nodes = 784
_num_hidden_nodes = 100
_num_out_nodes = 10
_lr = 0.1
_bias = 1
NN = NeuralNetwork(_num_in_nodes, _num_hidden_nodes, _num_out_nodes, _lr, _activate, _dactivate, _bias)

epochs = 30
for i in range(epochs):
    NN.run(train_img, train_label_onehot, 1)
    correct, wrong = NN.evaluate(train_img, train_label)
    print("epoch {0}".format(i))
    print("train precision: {0}".format(correct / (correct + wrong)))
    correct, wrong = NN.evaluate(test_img, test_label)
    print("test precision: {0}".format(correct / (correct + wrong)))
    
# for i in range(20):
#     res = NN.predict(test_img[i])
#     print(test_label[i], np.argmax(res), np.max(res))

```

Please be noted the above codes were in python 3 notebook.

Following is an experiment, with parameters as:

* Input nodes: 784
* Hidden nodes: 100
* Output nodes: 10
* Learning_rate: 0.1
* Bias: 1

Use the above settings as benchmark, then wiggle the parameters from different perspective.

A few observations through the experiments:

* Set bias to 0, 0.5, 1 doesn’t make observable difference.
Greater than 0.1 on learning rate side doesn’t make good on performance either.
* Performance goes up while increasing number of hidden nodes (up to 97.79%), especially when set the number to 1000, on the other hand, the training time increases significantly, take 10X times compares to the benchmark with 100 hidden nodes.

So, we may consider to have a solid network structure first, then tune the hyper parameters.

As said, this is the mini version of mnist classification, in the coming future posts, various activation functions, multi hidden layers, L1 and L2 normalization and batch normalization methods will be introduced into coming versions.

<img src="{{site.url}}/img/nn022.png">




[post status: half done]