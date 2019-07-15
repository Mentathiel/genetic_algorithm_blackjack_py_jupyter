# AI Course Practice

This project is one of the projects written for my AI class in Jupyter notebook using PyCharm.

A lot of the codes I did that are related to this class are heavily based on [my Teaching Assistant's code](https://github.com/matfvi/vi), though I try and create different problems for myself to apply the algorithms to. When it comes to real applications of this, modeling the problem is the real challenge, while the algorithm structure and implementation is fairly easy to get a hang on at that point, so that's what I'm aiming to focus on.

Following is a short description of the Blackjack algorithm.



### Blackjack

This is an implementation of genetic algorithm for finding the optimal Blackjack strategy. This algorithm does not count cards as the game progresses, so any card can be pulled at any point.

A genome is composed of two separate lists of probabilities. The `hit_probability` list represents the list of probabilities that the agent will choose to hit (take another card) at each given sum of cards in hand, while `ace_is_one_probability` is referring to whether the agent will prefer to consider an ace in his hand as a 1 or as an 11, again, for each respective sum of non-ace cards. Probabilities are represented in percentages aka they vary from 0 to a 100. The reason I chose to use probabilities instead of a dichotomy is because I wasn't sure if non-deterministic (or probability-based) strategy had any advantages over the deterministic one, but I concluded that if it didn't, it would develop a strategy where each probability gravitated toward either 0 or a 100%.

Fitness is calculated as the average win rate across 20 games multiplied by the average score in the games that were won. Win rate is there to prevent aggressive hitting strategies from developing, where the agent might win only 1 of 10 games, but do so with a high score, while the average is there to prevent the selection of passive strategies of always stopping in the first move and hence always winning.

Another concept worth mentioning is `player_preferred_sum`. The reason I created this is that cards in hand can have several "meanings" depends on how the aces are interpreted. The player should strive to interpret the aces in the best possible way for him, hence why `ace_is_one_probability` is optimized as well, and why fitness depends on `player_preferred_sum`. I didn't implement the game considering the player's sum as the optimal one at the end, but instead chose to always regard `player_preferred_sum` as his result. This was to increase selection pressure around `ace_is_one_probability` optimization, because agents which chose to regard their sum as smaller when both possibilities are winning would be selected against.

To test the performance of the algorithm, I've set it to play against itself, expecting it to yield approximtely 50-50 result on average, which it does. To further test it, I've set it to play with a completely randomized strategy several times with different strategies, and took the average number of wins in each of the situations. The testing so far indicates that the evolved strategy always outperforms the random strategy, but not by much. The evolved strategy wins about 56% of the time, while the random strategy wins 44% of the time. I'm not sure whether better results can be achieved with further optimization or bettering of my algorithm. It may be that a better strategy can't be made, given that the game is random.