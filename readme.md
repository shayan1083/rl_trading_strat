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
- Agent Class: The agent is defined as "Agent" class, that holds variables and member functions that perform the Q learning. An object of the "Agent" class  is created using the training phase and is used for training the model
- Helper Functions: Additional functions to help with training
- Training Module: Perform the training of the data. This will give one of three actions based on the states of the stock prices at the end of the day. During training, the action for each day is predicted, the rewards are computed, and the model weights are updated iteratively over a number of episodes (epochs). Additionally, the PnL (profit and loss) of each action is summed up to see whether an overall profit has occured. The aim is to maximize the total profit.

5/22/24 Commit:
Training Loss is not decreasing; agent is not making progress in increasing profit. Commit changes so that incase major restructuring messes up code I can pull original code back.