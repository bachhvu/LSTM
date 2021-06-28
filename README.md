# **Recurrent Neural Network**
Taking stock market data for a specific stock as an example of sequential data. Machine learning model can base on many characteristics such as the open, high, low, close values and volume of trades each day to learn to predict stock prices. Although the stock price depends on these characteristics, it is also largely depending on the stock value of the previous few days. In fact, for traders, the value (or the trend) of these previous days is an important determinant of prediction. 
Recurrent neural networks can solve this problem. They are neural networks with loops that allow information to persist. RNN processes the input sequentially, where the context of the previous input is considered when calculating the output of the current step. This allows the neural network to carry information in different time steps instead of keeping all inputs independent of each other.
 
 ![Picture1](https://user-images.githubusercontent.com/46337239/123663401-43a64f00-d82e-11eb-9abf-9d5bad1f0f4d.png)

Figure 1. RNN architecture

![Picture2](https://user-images.githubusercontent.com/46337239/123663426-4acd5d00-d82e-11eb-8cc8-c4e90c1e1d46.png)

Figure 2. Unrolled RNN architecture

During processing, the RNN passes the hidden state from before to the next step in the sequence. The hidden state acts as the memory of the neural network and saves information on previous data previously viewed by the network. The input at a time-step and the hidden state from the previous time step are combined to form a vector. The vector is passed through a tanh activation function to obtain the output of a new hidden state.
