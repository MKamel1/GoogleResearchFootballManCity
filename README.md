# Google Research Football AI Agent (Ongoing)
Researchers want to explore AI agents' ability to play in complex settings like football. The sport requires a balance of short-term control, learned concepts such as passing, and high-level strategy, which can be difficult to teach agents. A current environment exists to train and test agents, but other solutions may offer better results.
We are going to create AI agents that can play football. Teams compete in “steps,” where agents react to a game state. Each agent in an 11 vs 11 game controls a single active player and takes actions to improve their team’s situation. As with a typical football game, we want our team to score more than the other side. we can optionally see our efforts rendered in a physics-based 3D football simulation.
If successful, we'll help researchers explore the ability of AI agents to play in complex settings. This could offer new insights into the strategies of the world's most-watched sport. Additionally, this research could pave the way for a new generation of AI agents that can be trained to learn complex skills.
## Rules
In this competition you control a single player in 11-player teams. Rules are similar to the official football (soccer) rules - https://www.rulesofsport.com/sports/football.html, including offsides, yellow and red cards. There are, however, small differences:
###### Game consists of two halves, 45 minutes (1500 steps) each. Kick-off at the beginning of each half is done by a different team, but there is no sides swap (game is fully symmetrical).
###### Each agent controls a single player on the team. Controlled player is always the one in the ball's possession or the one close to the ball when defending.
###### Teams do not switch sides during the game. Left/right sides are assigned randomly.
###### For convenience of agent's implementation, observations provided to the agent are always presented as if the agent controlled the left team. Environment applies appropriate conversions to both observations and actions. Game engine is fully symmetrical, so sides swapping does not affect the game in any way.
###### Non-cup scoring rules apply, i.e. the team which scored more goal wins; otherwise it is a draw.
###### There is no walkover applied when the number of players on the team goes below 7.
###### There are no substitute players.
###### There is no extra time applied.
## Observations and Actions
On each turn, agent receives observations representing full state of the game, including current score, position of all players, their speed, and tired factor. Detailed format of observations is described here: https://github.com/google-research/football/blob/master/gfootball/doc/observation.md#raw-observations

In each turn, agent is supposed to generate one of 19 actions (numbered from 0 to 18) from the default action set:
https://github.com/google-research/football/blob/master/gfootball/doc/observation.md#default-action-set. Returning an action outside of the action set results in agent's loss.

## Game End
Game ends after 3000 turns or when one of the agents has an error (either timeout, thrown exception, or invalid action returned). The agent who caused an error loses; the other wins. In case of no errors, the winning team is the one which scored more goals. Ranking is then updated according to the evaluation rules. Check out the evaluation tab for more details.

## Source Code
Our game rules are implemented in the following open source code:
https://github.com/Kaggle/kaggle-environments/blob/master/kaggle_environments/envs/football/football.py

JSON schema:
https://github.com/Kaggle/kaggle-environments/blob/master/kaggle_environments/envs/football/football.json
