# Palace Card Game
## Background

### Rules
There are many variations of the rules of Palace, the following are my rules, and the ones that will be used for this project.

Cards are dealt clockwise, with a number of cards face down, face up, and in the hand, with the number of each being dependent on the number of players.

| No. Players | Total No. Cards Each | No. Cards for Each Pile | Remainder |
|-------------|----------------------|-------------------------|-----------|
| 2           | 24                   | 8                       | 4         |
| 3           | 15                   | 5                       | 7         |
| 4           | 12                   | 4                       | 4         |

After the cards are dealt, players can swap cards between their hand, which only they can see, and their face-up cards, which everyone can see.
After this phase in the game, swapping is no longer allowed.
Once the game starts properly, players must play a card onto the discard pile that is higher than or equal to in value to the currently played card.
If a player cannot play a card, they must pick up the entire discard pile.
If a player has multiples of a card, they can all be played at once.

The order of play is clockwise.
The values of the cards are in order as follows:\
2, 3, 4, 5, 6, 7, 8, 9, 10, J, Q, K, A

Some cards have special effects on the game.
These are as follows:

| Card | Effect                                                                                        |
|------|-----------------------------------------------------------------------------------------------|
| 2    | Can be played on any card. Resets the current value back down to 2                            |
| 3    | Can be played on any card. Mimics the card it was played on                                   |
| 7    | The next card played must have a value of 7 or lower                                          |
| 8    | Switches the direction of play. Playing multiple will switch the direction that many times    |
| 10   | 'Burns' the current discard pile, setting it aside. The player that played it gets another go |
| Q    | Skips the next player's turn. Playing multiple will skip that many player's turns             |

Another card interaction is that if 4 cards of the same value are in a row on the discard pile, the discard pile is burned, and the player gets another turn.

Players must play from the cards in their hand first, then from the face up cards, then from the face down cards.
The last person with cards is the loser.
There is no winner.

## Timeline

### 1. Server
The main goal of this project is to have a fully functional backend for the card game that any sort of frontend can be added to.

### 2. Console-based Frontend
After the backend is created, the goal will be to create some sort of basic frontend that interfaces with the api and allows players to actually play the game

### 3. Graphical Frontend
This will be a heuristics-focused application designed for a good user experience. 
It will either be a web-app made using react, or an actual game made using the Godot game engine.

## Requirements

### Server
#### MVP
- A user should be able to create a game
- A user should be able to join a game via a code
- The user that created the game should be able to start it
- Users should be able to swap cards between their hand, and their face-up cards
- The game should support between 2 and 4 players
- The game should start properly once every player is ready
- Users should be able to request data about the state of the game
    - Who's turn it is
    - How many cards each user has
    - What another user's face-up cards are
    - How many cards are in the draw pile
    - How many cards are in the current discard pile
- Users should be able to perform an action
    - If it is not the user's turn, the action should fail
    - Users should be able to play 1-4 cards
        - This should fail if the card doesn't meet the requirements of the game
        - This should fail if the user doesn't have access to the card they're tring to play e.g. a face-up card when they still have cards in their hand
        - This should fail if the cards aren't of the same type
    - Users should be able to pick up the discard pile
- Server should determine who's turn it is
    - A user without any cards should not have any further turns

#### Additional Features
- The user that creates the game should be able to customise the rules of the game
    - This user should be able to enable and disable certain cards' effects
    - This user should be able to alter certain game behaviour such as
        - If a player can pick up the deck when they're able to play a card
        - If a 3 copies the effect of the card below it, or just the value
- The game should be able to support additional players with multiple decks of cards

## Design
### Data

The following shows how data is modeled for this application.

![Entity Relationship Diagram](/docs/ERD_1.png)

There is only one relation between the player and the game.
As there is no need to store information betwen games, there is no need for a link table, as even though a game can have multiple players, a player is only relevant to one game.
One part I was unsure about is storing information about which user created the game.
It is information that is both relevant to the player and the game but it can be inferred by the player's index, as the first player in the game should have the index `0`.

## Project Resources
As this is a project to help me learn, I've listed some resources I used in case I want to come back to them.

- [Get It Right the First Time: Writing Better Requirements](https://www.ibm.com/docs/en/SSYQBZ_9.6.1/com.ibm.doors.requirements.doc/topics/get_it_right_the_first_time.pdf)

- [Swagger Docs](https://swagger.io/docs/specification/v3_0)