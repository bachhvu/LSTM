https://bachvu98.github.io/LSTM/

<p align="justify">

# **Recurrent Neural Network**
Taking stock market data for a specific stock as an example of sequential data. Machine learning model can base on many characteristics such as the open, high, low, close values and volume of trades each day to learn to predict stock prices. Although the stock price depends on these characteristics, it is also largely depending on the stock value of the previous few days. In fact, for traders, the value (or the trend) of these previous days is an important determinant of prediction. 
Recurrent neural networks can solve this problem. They are neural networks with loops that allow information to persist. RNN processes the input sequentially, where the context of the previous input is considered when calculating the output of the current step. This allows the neural network to carry information in different time steps instead of keeping all inputs independent of each other.
  
<p align="center">
  <img src="https://user-images.githubusercontent.com/46337239/123663401-43a64f00-d82e-11eb-9abf-9d5bad1f0f4d.png?raw=true" alt="Sublime's custom image"/>
  <br>
    <em>Figure 1. RNN architecture</em>
</p>

<figcaption style="text-align:center"></figcaption>

<p align="center">
  <img src="https://user-images.githubusercontent.com/46337239/123663426-4acd5d00-d82e-11eb-8cc8-c4e90c1e1d46.png?raw=true" alt="Sublime's custom image"/>
  <br>
    <em>Figure 2. Unrolled RNN architecture</em>
</p>

During processing, the RNN passes the hidden state from before to the next step in the sequence. The hidden state acts as the memory of the neural network and saves information on previous data previously viewed by the network. The input at a time-step and the hidden state from the previous time step are combined to form a vector. The vector is passed through a tanh activation function to obtain the output of a new hidden state.

### **Limitations**
Recurrent neural networks are affected by short-term memory. If the sequence is long enough, it will be difficult for them to pass information from the previous steps to the later steps. Therefore, if you try to process a piece of text to make predictions, the RNN may miss important information early on. An example of this problem would be in the Natural Language Processing topic. Consider having a network that generating the next word based on the previous ones. If we are trying to predict the last word in the text “I grew up in the United Kingdom. I speak fluent _____”. The latter sentence structure indicates that the next word might be the name of a language. However, in order to know exactly what the language is, the context of ‘the United Kingdom” from the former sentence is required. In a real scenario, it is feasible for the distance between the relevant data and the point at which it is required to grow significantly. RNNs become unable to learn to connect the information as that gap widens.

In neural network, the gradient is the value used to update the weight. Due to the chain rule, the gradients must go through continuous matrix multiplications during the back-propagation process, making it to either diminish exponentially (vanish) or increase exponentially (explode). For activation functions like the sigmoid function, as we move to the initial layer, the gradient will multiply many times. Therefore, when we go to the initial layer, the gradient becomes too small, and it is difficult to train these layers because the parameter updates become insignificant. This makes the learning of long data sequences difficult. Thus, RNNs suffer from short-term memory as a result of these difficulties, as they are unable to remember what it seen in longer sequences and hold on to long-term dependencies. Thankfully, this problem can be solved by using a modified version of RNNs – the Long Short-Term Memory Networks. 

# **Long Short-Term Memory (LSTM)**
Long Short-Term Memory Networks are a kinds of RNN and has a similar flow as a recurrent neural network. They were introduced by Hochreiter & Schmidhuber (1997). It is an upgrade to resolve RNN learning failure when there are more than 5-10 discrete time steps between the relevant input event and the target signal in past observations (vanishing/exploding gradient problem). The key to LSTMs is by introducing a memory unit called "cell state".  At each time step, the LSTM unit obtains 3 different pieces of information: the current input data, the short-term memory (hidden state) of the previous unit (similar to the hidden state in RNN), and finally the long-term memory (cell state).

<p align="center">
  <img src="https://user-images.githubusercontent.com/46337239/123663804-aa2b6d00-d82e-11eb-8d74-5cd335de2ba0.jpg?raw=true" alt="Sublime's custom image"/>
  <br>
    <em>Figure 3. LSTM architecture</em>
</p>



Short Term and Long-Term Memory cells are like mini neural networks designed to enable memory in larger neural networks. This is achieved through the use of recurrent nodes in the LSTM cell. The node has an edge looping back with a weight of 1, which means that in each iteration of feedforward, the cell can retain information from the previous step and all previous steps. Since the weight of the looping connection is 1, the old memory will not disappear over time like in traditional RNN.

LSTM has 3 gates, to regulate the information flow in an LSTM cell.

The forget gate decides to keep or discard information from the long-term memory based on current input and previous hidden states. This is done through the sigmoid activation function. This function only returns 0 and 1 for input. Once multiplied by something, it either drop (multiplied by zero results in zero) or passes completely (multiplied by 1 results in the same value)

<p align="center">
  <img src="https://user-images.githubusercontent.com/46337239/123663845-b44d6b80-d82e-11eb-8785-3993cb41369c.png?raw=true" alt="Sublime's custom image"/>
  <br>
    <em>Figure 4. Forget Gate</em>
</p>


The input gate decides what new information to store in the long-term memory. At this point, the previous hidden state and the current input is passed into a sigmoid function, which determines the values need to be updated by converting it between 0 and 1. This is very similar to the forget gate and can removes any unwanted information from the current input. The hidden state and current input are also passed into the tanh activation function to compress the value to always be between -1 and 1 which help regulating the network. Next, the output from tanh and sigmoid are then multiplied, and the results represents the information that will be retained in long-term memory. Finally, this output will be added to the cell state to update it.

<p align="center">
  <img src="https://user-images.githubusercontent.com/46337239/123663875-ba434c80-d82e-11eb-87ae-d8a68c504f89.png?raw=true" alt="Sublime's custom image"/>
  <br>
    <em>Figure 5. Input Gate</em>
</p>

The output gate decides what the next hidden state should be. The current input and hidden state will be passed through a sigmoid function. Then, the cell state is put through a tanh activation function. The output from these two processed is multiplied to produce the new hidden state for the next time step.

<p align="center">
  <img src="https://user-images.githubusercontent.com/46337239/123663904-bfa09700-d82e-11eb-99c6-ae14cd2ff2c4.png?raw=true" alt="Sublime's custom image"/>
  <br>
    <em>Figure 6. Output Gate</em>
</p>

## **Variant**
The RNNs and LSTMs architecture stated above are only capable of capturing the dependencies in only one direction. This poses a challenge when performing tasks such as machine translation, where we also need context from words we haven’t seen yet. This results in bidirectional RNNs and LSTMs, which is a variant of RNN and LSTM that works in both ways. Bidirectional LSTM is frequently seen in papers and application because to its utility in grasping the context. 

# **Conclusion**
In summary, RNNs are good at processing sequential data, but they have a short-term memory problem. LSTMs were developed as a way to reduce short-term memory by employing a long-term memory unit called “cell state”. They have been applied successfully to a variety of applications such as speech recognition, speech synthesis, language modeling, translation, image captioning.

# **References**
Hochreiter, S. & Schimidhuber, J., 1997. Long Short_term Memory. Neural Computation, 9(8).
</p>
