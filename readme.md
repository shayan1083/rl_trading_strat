A super basic trading strategy that can tell when to buy and sell a stock using Deep Q Learning. I followed the original jupyter notebook here: https://github.com/tatsath/fin-ml/blob/master/Chapter%209%20-%20Reinforcement%20Learning/Case%20Study%201%20-%20Reinforcement%20Learning%20based%20Trading%20Strategy/ReinforcementLearningBasedTradingStrategy.ipynb

As of right now, the neural network is not buying or buying too much. Ill get back to it when i have the time. 

Create VENV:
1) Enter terminal
2) navigate to main folder
3) python3 -m venv {venv name}

Activate env:
1) Enter terminal
2) navigate to main folder
3) type "source {venv name}/bin/activate"

- the name of the virtual environment should be next to the terminal prompt if it is activated
- everything installed when the venv is running will be installed locally

Install Libraries:
1) Enter terminal
2) pip3 install -r requirements.txt

- strat.ipynb has the code
- When in "strat.ipynb", select kernel in the top right, and choose {venv name} to enter virtual environment
- "deactivate" in terminal deactivates virtual env

Algorithm:
This is a reinforcement learning based trading algorithm. The algorithm takes an action depending on the current state of stock price. The algorithm is trained usign Deep Q Learning.

Key Components: 
- Agent: Trading Agent
- Action: Buy, Sell, Hold
- Reward Function: Realized profit and loss (PnL) is used as the reward function
    - Sell: Realized profit and loss (sell price - buy price)
    - Buy: No reward
    - Hold: No reward
- State: Differences of past stock prices for a given time window 

The data used is from the S&P 500. 
When calling yfinance.Ticker.history, it returns a table of information.
- The date column is the date of the recorded data point
- open is the price the stock was at when the market opened that day
- high is the highest price the stock was at that day
- low is the lowest price the stock was at that day
- close is the price the stock was at when the market closed that day
- volume is the total number of shares or contracts traded that day
- dividends is the amount of dividents paid out per share that day.
- stock splits is the stock split ratio on that day
The S&P500 is an index; it tracks the performance of stocks. It doesn't pay dividends, nor does it undergo stock splits, so both of these columns are zero. 

Step 3:
The algorithm deciedes whether to buy, sell, or hold, when provided with the current market price. The algorithm is based on the "Q-learning" approach and uses Deep Q Learning to come up with a policy. The name Q learning comes from the Q(s, a) function where, based on state 's' and action 'a', the expected reward is returned

To implement the DQN algorithm, several functions and modules are implemented that interact with each other during the model training: 
- Memory Class: The Agent stores its experiences in a dequeue called Memory. Its functions include pushing an experience to memory, getting a random sample of the experiences, and getting the length of the memory

- DQN Class: Deep Q learning uses a neural network, which this class creates. It creates the layers, the loss function, optimizer, and sets the learning rate. It contains functions to perform a forward pass on the model, and train the model using gradient descent. 
    - Model Architecture: The model outputs a separate output unit for each possible action, and only the state representation is passed into the neural network as input. The outputs correspond to the predicted Q-values of the individual action for the input state. The main advantage of this architecture is the ability to compute Q-values for all possible actions in a given state with only a single forward pass through the network. 

- Agent Class: The agent is defined as "Agent" class, that holds variables and member functions that perform the Q learning. An object of the "Agent" class  is created using the training phase and is used for training the model. It has a function act that chooses an action using epsilon greedy policy, and it has experience replay. 
    - Experience Replay: The agent's experiences at each time step are stored in memory. Experiences take the form of (state, action, reward, next_state) tuples. Durring the inner loop of the training module, apply minibatch updates to the experiences that are randomly sampled from memory. Random Sampling is beneficial because each step of exerpience is potentially used in many weight updates, which allows for greater data efficiency. Also, learning from consecutive samples is inefficient, due to strong correlations between samples. Randomizing samples breaks correlations and therefore reduces the variance of the updates. 

- Helper Functions: Additional functions to help during training

- Training Module: Perform the training of the data. This will give one of three actions based on the states of the stock prices at the end of the day. During training, the action for each day is predicted, the rewards are computed, and the model weights are updated iteratively over a number of episodes (epochs). Additionally, the PnL (profit and loss) of each action is summed up to see whether an overall profit has occured. The aim is to maximize the total profit.

5/22/24 Commit:
Training Loss is not decreasing; agent is not making progress in increasing profit. Commit changes so that incase major restructuring messes up code I can pull original code back.

6/4/24 Commit:
increased to 15 years of data. 12 years of training, 3 of test. added one layer in neural net, increased number of neurons. added some more plotting functions. Training results in not buying anything or only buying.
