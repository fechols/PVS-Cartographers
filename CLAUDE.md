# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

PVS Cartographers is a single-page HTML/CSS/JavaScript simulation demonstrating "map-compressing entities" - agents that explore a grid world while building and maintaining compressed internal representations of their environment.

## Running the Project

Open `index.html` in a web browser. No build step, dependencies, or server required.

## Architecture

The entire application is contained in `index.html` with embedded CSS and JavaScript:

- **Grid World**: 56x28 tile grid with walls, empty spaces, and dynamic "flippy" tiles that randomly toggle between wall/empty states
- **Agents**: Entities with 360-degree field of view that move through the world, each maintaining:
  - `map[][]`: Bayesian belief about each tile (0=empty, 1=wall, 0.5=uncertain)
  - `surpriseField[][]`: Prediction error magnitude at each cell
  - `visitField[][]`: Recent visit intensity for exploration guidance
- **PVS (Potentially Visible Set)**: Raycasting-based visibility calculation determining which tiles each agent can currently see
- **Movement Heuristic**: Agents prefer exploring unknown regions, chasing surprise signals, and avoiding recently visited areas

## Key Simulation Parameters (UI Controls)

- **Speed**: Simulation step rate multiplier
- **Forget**: Rate at which beliefs decay toward uncertainty (0.5) for unseen tiles
- **Surprise**: Weight of prediction error in belief updates and visualization
- **PVS**: Toggle visibility overlay display
- **2nd agent**: Enable/disable second exploring agent

## Visualization Panels

1. **Top-left**: Agent 1 world view with PVS overlay (green)
2. **Bottom-left**: Agent 2 world view with PVS overlay (blue)
3. **Top-right**: Combined compressed map showing merged agent beliefs
4. **Bottom-right**: Inverse field showing regions "forgotten" by agents (high uncertainty)
