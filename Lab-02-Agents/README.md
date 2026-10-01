# Lab 2: Agents — Constructing a Goal-Based Agent

## Objective

This laboratory focuses on constructing a goal-based intelligent agent for a warehouse navigation problem using a Large Language Model (LLM) as a software engineering assistant.

The laboratory covers:
- Understanding the warehouse navigation problem
- Designing a goal-based agent
- Using an LLM to generate Python code
- Executing and testing the generated program
- Evaluating the selected search algorithm
- Improving the program through iterative prompting when necessary

## Problem

A vehicle must navigate through a two-dimensional warehouse from a starting position `S` to a goal position `G`.

The warehouse contains free cells and obstacles. The vehicle can move one grid square at a time in four directions:

- Up
- Down
- Left
- Right

The agent must find a collision-free path from `S` to `G`.

## Agent Design

The environment is represented as a 2D grid.

The agent maintains:
- Its current position
- The warehouse layout
- The goal position
- The obstacle locations
- The valid neighboring positions

The agent uses a search algorithm to determine a sequence of actions that moves it toward the specified goal.

## Implementation

The Python implementation was generated using an LLM based on a detailed problem specification.

The generated program:
- Represents the warehouse as a 2D grid
- Locates the start and goal
- Uses Breadth-First Search (BFS)
- Avoids obstacles and invalid positions
- Reconstructs the discovered path
- Displays the warehouse with the path marked

## Testing

The generated program successfully found a collision-free path from `S` to `G`.

The resulting path required **20 moves**.

An independent validation function was also used to verify that:
- The path starts at `S`
- The path ends at `G`
- No obstacle is crossed
- Every movement is between adjacent grid cells
- The path remains within the warehouse boundaries

The validation result was:
Path Validation: Path is valid.

## Search Algorithm

The agent uses Breadth-First Search (BFS).

BFS explores reachable positions level by level. Since every movement has the same cost of one grid square, BFS is suitable for finding a shortest path in terms of the number of moves.

## LLM-Assisted Development

The first LLM-generated implementation worked correctly without requiring a second prompting iteration. The generated code was executed and independently validated rather than being assumed to be correct.

## Files
- Lab2_Agents.ipynb — Python implementation, agent design, prompt, execution, and validation
- Lab2_Agents_Report.pdf — Laboratory report
- agents_lab.pdf - Laboratory Manual
