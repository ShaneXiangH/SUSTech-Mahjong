# Mahjong main logic implementation

## Cards are defined by numbers:

```
1 ~ 9: One tube ~ 9 tube
11 ~ 19: 10,000 ~ 90,000
21 ~ 29: one ~ 9
31 ~ 34: southeast and northwest wind
41: get rich
42: Red Middle
43: Whiteboard
4 cards of each type
ps: In the subsequent expansion, special cards are also represented by regular numbers
```

## Classes in the code:

1. User card wall maintenance:

   This class is instantiated for each user.

   It is used to store and maintain current hand cards and information such as Kong, eat, and touch.

   The methods of playing cards and drawing cards also exist in this category.

2. Various types of operation algorithms:

   Store the judgment functions and operation functions for judging bars, eating, touching, listening, and hustling operations.

   An instance of this class is instantiated in each card wall maintenance class for detection and special operations.

3. Hand category:

   The server controls this class.

   This class will maintain a library, in which the cards have three states: undisposed, dealt, and discarded (played)

   The draw list is stored here and is used for the operation of draws and shots.

   Control the user's card sequence and time limit.

## Class specific information:

1. User card wall maintenance:

During initialization, random numbers will be generated to enable the user to obtain the starting hand.

The card wall information is stored in a list that can be automatically sorted.

The information of the cards played in the last house will be sent to the current player through the server.

Use a temp to store the information of the cards issued by the home, which is used to judge the operation such as eating.

The information of eating, touching, and bar is stored in three arrays (or lists). The value in it represents the card type that is being operated on.

Draw: Randomly obtain a card from the card game maintained by the server.

Play a card: Kick a card from your list.



2. Operation algorithm class:

**Note: Only digital cards have this operation. **

**The specific implementation of Ting and Hu can refer to https://github.com/fwhappy/mahjong/tree/master/ting**

**According to the rules, when the player chooses the listening operation, no other operations can be performed, and only the cards drawn in this round can be played**.

Judgment to eat: (temp, list)

```
Traverse the card wall list, it can form two cards of 3 straight with temp and it is an option to eat.
Display it on the user interface for players to choose.
```

Judge bump and kong: (temp, list)

```
Similarly, traverse the card wall list. There are two cards that are the same as temp that can be touched. Three cards are kong.
Display it on the user interface for players to choose.
```

To eat, touch, and bar: (list)

```
When the player chooses the operation he wants, he kicks the corresponding card out of his card wall list, returns a record, and places it in the interface.
The card wall maintenance category also needs to record this information.
```

Judging Hu: (list)

```
Scan the card wall list to determine whether the conditions are met
```

Judge and listen: (list, library array)

```
Scan the card wall list again, and determine which cards you want to play based on the list and discarded cards.
```

Carry on Hu:

```
Win, settle the result and end.
```

Draw status:

```
The player enters a draw and triggers a special state. At this time, the server will maintain a list of draws belonging to the player.
When other players accidentally fire the cannon, this player will be judged to win.
```



3. Hand category:

To save the card library with an array (or other better way), you need to record the three states of the card.

Maintain the draw list and detect other players firing shots.

Control the player's order of cards, limit their time, and force them to randomly play cards if overtime.



## The general logic of the game:

At the beginning of the card game, the server records the order of the cards, and the game is played in this order.

Players automatically generate cards in their hands and start to operate in turn.

Before the player operates, check the player's card wall by using the functions in the operation algorithm class, and show the available operations to the player for their choice.

The cards and operations performed by the players will be passed to the server.

The server transmits the information that needs to be transmitted to other players, so that their interface changes accordingly.

At the end of the game, the settlement interface is displayed.