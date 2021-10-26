# Server

## LoginMsg:

The protocol sent when logging in, the account number, password and other information are transmitted.

The corresponding Handler in the server will connect to the database to check whether the information is legal.

If it is illegal, it will prompt login failure.

If you click the register button, the current account will be added to the database.

## SysMsg:

To detect the delayed protocol, it will detect whether the client can respond.

## BattleMsg:

When the player performs each step of the operation (playing cards, hitting the kong, etc.) in the game, the situation of the entire game is changed.

Including the logic of automatic licensing.

## RoomMsg:

## ResultMsg:

At the end of the game, the points, rankings and other information are settled.

# NetManager

starloop starts to work.

Continuously monitor information, and delay detection will be performed if the message is not received over time.

Populate the checkRead list.

Message distribution.

Receive client information.

Processing information.

# Polymorphism

MsgBase is the parent class of the protocol, and its subclasses are specific protocol types.

# Client

To be perfected



# Which class and file do we program in

![1570757293833](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\1570757293833.png)

The above figure shows the various classes that the server and client perform corresponding processing when they accept the corresponding agreement.

![1570757412263](C:\Users\PC\AppData\Roaming\Typora\typora-user-images\1570757412263.png)

The above figure is a class used to define variables and other information in a specific protocol.