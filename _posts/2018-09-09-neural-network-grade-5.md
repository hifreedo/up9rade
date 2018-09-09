---
layout: post
title: Neural Network [grade 5]
---

# Neural Network solving mnist

## grade 4: Mini version of solving mnist

The mnist solving is a big milestone for neural network practice in real field.

We will represent a workable mini version for solving mnist, on this version, the main items and challenges will be went through.

To get started, you will need to download mnist dataset in csv format by your own. The csv files will be 1 for training, 60k images in toal, and 1 for test, 10k images.
For each line, represents an image, 785 columns, 1st number denotes a label (from 0 to 9), the following 784 numbers denote pixels of the 28 * 28 image.

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
        
_activate = relu
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

[post status: half done]