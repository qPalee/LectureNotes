The formulation of a search problem is the process of formally defining the search problem

We make the following assumptions about the environment:
- Observable - Agent able to know urrent state
- Discrete - Finite many actions
- Known - The agent can determine which states are reached by which action
- Deterministic - Each action has one outcome

Under these assumptions, the solution to any problem is a fixed sequence of actions. More formally, the solution to a search problem is the sequence of actions from the initial state to the goal state  

The agent’s task is to find out how to act, now and in the future, in order to reach a goal state: namely to determine a sequence of actions  

The process of looking for a sequence of actions is called **search**

Formally, a search problem is defined by the following five components:
- Initial State - the state the agent starts in
- Actions - the set describing the actions that can be executed in any state s
- Transition Model - a description of what each action does
- Goal Test - determines if a state is a goal state
- Path Cost - function that assigns a cost to each path

The first 3 define the state space of the problem, in the form of a graph/network
A path in the state space is a sequence of states connected by a sequence of actions

