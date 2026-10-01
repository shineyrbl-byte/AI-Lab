# Lab 4: Logical Planning

## Artificial Intelligence Laboratory

### Topic
**Logical Reasoning for Planning using an LLM**

## Objective

This laboratory explores how logical reasoning and search can be combined to solve planning problems. A simple warehouse robot planning problem is used to understand states, actions, preconditions, effects, and goal states.

The laboratory also demonstrates how an LLM can be used to generate a planning agent and how the generated code can be tested and independently verified.

## Problem Scenario

A warehouse robot operates between three locations:

- A
- B
- C

Initially:

- The robot is at location A.
- The package is at location A.

The goal is to move the package to location C.

The available actions are:

- **Move** – move the robot between connected locations.
- **PickUp** – pick up the package when the robot and package are at the same location.
- **Drop** – drop the package at the robot's current location.

## Concepts Covered

- States and goal states
- Actions
- Positive and negative preconditions
- Positive and negative effects
- Action applicability
- State transitions
- Breadth-First Search (BFS)
- Logical reasoning for planning
- LLM-assisted code generation
- Testing and independent verification
- Prolog facts, rules, and queries

## Implementation

The Python planning agent represents a state as a set of logical propositions.

Each action contains:

- Action name
- Positive preconditions
- Negative preconditions
- Positive effects
- Negative effects

An action is applicable only when all its preconditions are satisfied.

Breadth-First Search is used to explore possible action sequences and find a sequence that reaches the goal state.

## Tests

The planner was tested using:

1. **Original warehouse problem**  
   Verified that the package can be moved from A to C.

2. **No PickUp action**  
   Verified that the planner correctly reports that no plan exists.

3. **Additional robot movement action**  
   Verified that reaching the goal requires the package itself to be at C, rather than only the robot.

## Prolog Extension

The optional Prolog extension demonstrates logical reasoning using:

- `connected/2`
- `can_move/2`
- `valid_move/2`
- Facts and rules
- Logical rule chaining

The Prolog program is used to verify valid and invalid movements and demonstrate inference through rules.

## Files

- `Lab4_Logical_Planning.ipynb` – Complete laboratory notebook containing the planning implementation, tests, explanations, and reflection.
- `planner.pl` – Prolog implementation for the logical reasoning extension.
- `logic_lab_ex.pdf` - Laboratory manual

## Key Takeaway

**Logic determines what is possible; search determines what to try.**

The laboratory demonstrates that an LLM can assist with implementing a planning agent, but generated code and results must still be tested and independently verified.
