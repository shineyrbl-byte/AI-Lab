# Lab 3: Search and A*

## Overview

This laboratory focuses on formulating a warehouse robot navigation problem as a search problem and implementing the A* search algorithm with the assistance of a Large Language Model (LLM).

The laboratory investigates search problem formulation, A* search, heuristic functions, testing and validation, BFS vs A* comparison, and the use of an LLM as an engineering assistant.

## Objectives

- Formulate a warehouse navigation problem as a search problem.
- Identify states, actions, transitions, initial state, goal state, and costs.
- Design a search agent before implementation.
- Implement A* search with LLM assistance.
- Test and validate the generated search agent.
- Compare BFS and A* on the same problem.
- Investigate the effect of different heuristic functions.
- Evaluate the reliability and limitations of LLM-generated code.

## Problem

A warehouse is represented as a 2D grid containing:

- `S` — starting position
- `G` — goal position
- `#` — obstacle
- `.` — free cell

The robot can move Up, Down, Left, or Right, with every movement having a cost of 1.

The objective is to find a valid path from `S` to `G`.

## Algorithms

### A*

A* selects states using:

`f(n) = g(n) + h(n)`

where:

- `g(n)` is the cost from the start state to the current state.
- `h(n)` is the estimated cost from the current state to the goal.
- `f(n)` is the total estimated cost through the current state.

The main A* implementation uses Manhattan distance as the heuristic.

### BFS

Breadth-First Search was implemented and compared with A* on the same warehouse.

## Experiments

The A* agent was tested on:

1. Original warehouse
2. One-step solution
3. No-solution warehouse
4. Warehouse with alternative paths

The following heuristics were also investigated:

- Manhattan distance
- `h(n) = 0`
- Euclidean distance
- `2 × Manhattan distance`

## Results

| Experiment | Solution | Path Length | States Expanded |
|---|---|---:|---:|
| Original A* | Yes | 40 | 64 |
| One-step map | Yes | 1 | 2 |
| No-solution map | No | N/A | 9 |
| Alternative paths | Yes | 4 | 5 |
| BFS | Yes | 40 | 64 |
| A* | Yes | 40 | 64 |

### Heuristic Investigation

| Heuristic | Solution | Path Length | States Expanded |
|---|---|---:|---:|
| Manhattan | Yes | 40 | 64 |
| `h(n) = 0` | Yes | 40 | 64 |
| Euclidean | Yes | 40 | 64 |
| `2 × Manhattan` | Yes | 40 | 64 |

For this particular warehouse and implementation, all four heuristics produced the same measured path length and number of expanded states.

### Key Learning

The laboratory demonstrates that an LLM can assist with implementing a search algorithm, but generated code must be inspected, tested, and validated before being trusted. The engineer remains responsible for the correctness of the final implementation.

## Files
- Lab3_Search_AStar.ipynb — Python implementation, agent design, prompt, execution, and validation
- Lab3_Search_AStar_Report.pdf — Laboratory report
- search_lab_ex.pdf - Laboratory Manual
