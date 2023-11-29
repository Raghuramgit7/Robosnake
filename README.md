# Robosnake

This is an implementation of a 4-player [Snake](https://en.wikipedia.org/wiki/Snake_(video_game_genre)) game, where each player is controlled by a different piece of AI code.

(The AI code is very, **very** basic! You will be able to understand this codebase even if you've never studied AI.)

You are a developer at an organization that wants to ship this game to users. People will "play" the game by trying to program clever AI agents (or "bots") to compete against other people's AI agents.

This repository currently contains prototype code which works as intended, but the code is not very readable or maintainable. Your job is to refactor the codebase so that it's easier to extend with new features.


## Gameplay

There is no user input in the game: the keyboard and mouse do not do anything. All four players are controlled by AI agent code. The "Run game" button starts the game.

The game board is a square grid of square cells, drawn below the "Statistics" table. The cells on the grid are the "pixels" on the "screen" that displays the game.

Each player is represented by a different color on the board: A is green, B is blue, C is orange, and D is purple.

Each player starts in a different corner of the game board. On a player's turn, they are allowed to move into any cell adjacent to their current position.

The players take turns in order: A moves first, then B, C, D, and then A again (and so on). The game screen updates the position of every player simultaneously, but if two players try to move into the same cell, the "tie" is broken by turn order.

When a player moves into a cell, the player takes that cell. To indicate this, the cell changes to display the color of the player.

A cell may contain an apple, which is indicated by the color red. In the "Statistics" table, each player has a counter of how many apples they've taken. After each round of turns, new apples are added to the board in random unoccupied cells.

A player loses if they try to move into a cell that has already been taken, or if they try to move outside the boundaries of the game board. This includes if an AI agent tries to move "backwards" (in the opposite direction as its previous move).

The game is over when all players have lost. The "winner" is the player with the highest apples counter at the end of the game.


## Agents

The AI agents cannot "see" the entire board: on their turn, they can only "see" a 5x5 region of cells centered around their current position.

This restriction is implemented in the type of the `agentMove` function, which controls the AI's behavior on each move. This function is not given access to the data of the whole board: it's only given access to the data of the 5x5 region that the current player should be able to "see".

When users are playing the game by writing agents, each agent can do whatever it wants with the region that it can "see": it may run any kind of algorithm over the data structure, or even ignore it altogether.

Each agent should be able to keep its own "private" state, but this is currently not implemented: the hard-coded behavior for C depends on some global variables.


## The codebase

The codebase is organized into multiple modules within the `src` folder:
- `DrawingLibrary.ts` is a library which is used by the rest of the code. You **must not modify** this file: it's owned by a different team of developers.
- `GameScreen.ts` defines the `Cell` and `GameScreen` types, which represent "pixels" on the "game board".
- `GameRunner.ts` defines the rules of the game, but **not** the behavior of the AI players.
- `Agent.ts` defines the behavior of each AI player.
