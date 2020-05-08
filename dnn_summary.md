# What is a neural network?

Neural networks, a biologically-inspired programming paradigm which enables a computer to learn from observational data. It is inspired from th human brain which consists of 100 billion cells called neurons, connected together by synapses. So as the name suggests, **Neural**-> neuron, or something which contains number, has inputs and outputs. and **Network**-> a systematic way in which these neurons are connected to learn from observational data.

So simply saying, neural network is a graph of input and output neurons. For example:
![](NN.png)

This is a simple three layer network, one input layer, one hidden and one output layer. The image pixels are the input in DNN, and is making three very simple decisions, by weighing the input evidence. The output layer is the prediction made. The hidden layers, whose each of those perceptrons is making a decision by weighing up the results from the first layer of decision-making. In this way a perceptron in the second layer can make a decision at a more complex and more abstract level than perceptrons in the first layer. And even more complex decisions can be made by the perceptron in the third layer. In this way, a many-layer network of perceptrons can engage in sophisticated decision making.
So we can see that neural networks hame basic parts-
<ol>
  <li>**Neurons** - A neural network is a graph of neurons. A neuron has inputs and outputs.</li>
  <li>**Connections and Weights** - A neural network consists of connections, each connection transferring the output of a neuron to the input of another neuron. Each connection is assigned a weight.</li>
  <li>**Propagation function** - The propagation function computes the input of a neuron from the outputs of predecessor neurons. The propagation function is leveraged during the forward propagation stage of training.</li>
  <li>**Learning Rule** - The learning rule is a function that modifies the weights of the connections. This serves to produce a favored output for a given input for the neural network.
