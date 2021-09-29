# Value-Iteration-Dice-Game
A coursework where we were required to create an agent that was able to play a dice game and consistently obtain an above-average score. My agent managed to obtain a score of 12.4 out of a maximum of 18 for the simple rules game, and for the extended rules game my agent returned an agent of 4.1 out of a maximum of 6. Therefore, my agent consistently returned a score that was 70% of the maximum score.


## DICE GAME | README

## ----- INTRODUCTION -----
This coursework was based on a simple dice game that involved rolling three dice. Starting with 0 points, the only two actions the player can choose from are to 'stick' or reroll any or all the dice, with a penalty of -1. The score is the sum of the dice faces, but if there are any duplicates, the dice is flipped upside down. The aim of the game is to get the highest score possible - the maximum score is 18.

The objective of this assignment was to create an agent that was able to play the game and generate a decent average score. The method I used to implement this agent was value iteration. To calculate the optimal action to take at each state, I used the expected value of taking each action from a state to find the best possible value of the state, independent of any policy.


## ----- IMPLEMENTATION -----
My general implementation involved first retrieving the lists of all possible states and actions in the game. After initialising gamma to 0.9 and theta to 0.025, I then declared two empty dictionaries using the list of states as keys: one for the maximum state values and one for the policy. A third dictionary was also declared (actionValues{}) which stored the summed Bellman values for each action that could be taken from each state. actionValues{} was reset to 0 for each key before looping through the next state.

The value iteration algorithm loops through every state, and then loops through every action possible for that state. The transition probability and reward are retrieved for each. The above values are then used in the Bellman equation to get the key value for each state. The maximum of these values is selected (i.e the best action).

The value in the dictionary stateValues{} is updated to the corresponding maximum state key value. The policy dictionary is also updated with the optimal action to take for the state. If the key value hasn't changed by a significant amount (if delta < theta) then the loop is ended early - it has converged to the true expected values of the state. 
        
The most important variables I used to implement value iteration were the dictionaries and convergence values. The three dictionaries I declared (stateValues{}, actionValues{}, policy{}) all used the actual states themselves as keys. For example, the state value for (1, 2, 2) was 11.7058287500, which resulted in an action of rerolling dice number (1, 2) so that the 1 would be held.

Additionally, the convergence threshold values were beneficial in calculating the maximum values for each state. The variable delta was used to store the modulo of the difference between the previous and current state values. If delta was below a certain threshold (theta = 0.025), then the values for the Bellman equation had converged to an appropriate amount and there was no need to continue the loop.

Lastly, my Bellman equation was of the form:

probability * (reward + (gamma * [expanded state]))

With all of the resulting values being summed up for each action. To turn the recursive pseudocode into an update equation, I used an iterative loop to iterate through each new state. The loop was then broken on convergence. The only exception to the Bellman equation was when the next state was [None], as occurs when all three dice are held. Instead of using the Bellman equation, I updated the corresponding value with:

probability * reward

To signify a terminal state, where the game ends.


## ----- TESTING -----
I tested my code as follows on the standard tests and obtained the following results:

Score for 100 tests: 12.75, Time: 1.8438 seconds
Score for 1000 tests: 12.473, Time: 2.4688 seconds
Score for 10000 tests: 12.3277, Time: 7.3750 seconds

From these results it can be inferred that my implemented agent returns an average score of about 12.4. The maximum score is 18, so my agent returns 70% of the maximum score.

When analysing the policy, the best action for (1,1,1) to (1,1,6) is to hold all dice. The best action for (6,6,6) is to hold (0,), which seems unlikely for a human player to choose, but in the case of no duplicates when dice (1, 2) are rerolled, the 6 on dice 0 will boost the final score.

Testing my agent for the extended rules with two three-sided dice results in:

Score for 100 tests: 4.11, Time: 0.00031 seconds
Score for 1000 tests: 4.122, Time: 0.00020 seconds
Score for 10000 tests: 4.1216, Time: 0.00018 seconds

The maximum score that can be obtained in this case is 6, resulting in my agent returning an average that is also approximately 70% of the maximum score.

From these tests, I can conclude that my implementation of value iteration for the agent returns an average score that tends to be around 70% of the maximum possible score.




