# Zenly-Ghost-mode-attack

## foreword

This repository enumerates an exhaustive way to obtain the precise location of the Zenly APP ghost mode.

## What is Ghost Mode 👻

Zenly was developed to use a fun way to connect and share your location. However, we know that sometimes for various reasons, you may not want to share your precise real-time location, which is why we developed Ghost Mode, which allows you to decide for yourself who sees and sees what! Ghost mode can be set individually for one, some or all of your friends.

**There are three options to choose from:**

1.  Precise: Shows your exact real-time location.
2.  Blur: Shows a random location in your area. Between 10 meters and 1.2 kilometers from your actual location.
3.  Freeze: After enabling Freeze Mode, your position will remain fixed at the last position you were before you turned Freeze Mode on.

How to open: On the Zenly profile page, click the Ghost icon in the upper right corner of the page to open the Ghost mode setting interface.

## principle

The Zenly fuzzy positioning algorithm will orientate the user at a certain coordinate point every time. In fact, although this seems very random, if you have two friends in the same place and both have fuzzy positioning enabled, the Zenly server will The coordinates of the two of them are directional offset, and then through observation, it is found that they are displayed in the same coordinate position, and the avatars coincide. It can be seen from this that although Zenly's fuzzy positioning belongs to random movement, the random coordinates are not based on user-distinguished movements, but are fixed random movements.

Therefore, you can take advantage of this feature, use the Android emulator and install Zenly, and then use the virtual GPS function of the emulator to traverse the coordinates in the fuzzy positioning range of the friend. If you observe that the avatars in the APP overlap, you can roughly judge. its precise location.

## manual attack

> initialization

First, we need three accounts for attack verification, namely:

-   A - attacker
-   B - A's friend
-   C - the attacker's puppet robot

The three of them are related as follows:

As an attacker, A needs to obtain the precise location of B.

B is a friend of A, and B has enabled fuzzy positioning for A.

C is A's puppet and is used to exhaustively enumerate the exact location of B. At the same time, A and C are friends, and C has also opened fuzzy positioning for A, and C and B are not friends.

> verify

As an attacker, the account will be used to observe the location of B and C. Since B and C have opened fuzzy positions for A, we need to confirm the approximate range of B first.

Assuming that the position of B remains unchanged, only the coordinates of C need to be moved. If it is observed that the positions of B and C overlap, that is, the current coordinates of C are the coordinates of B.

The blur range of Zenly is actually a square. Since it is displayed as a circular range in the APP, it is necessary to take the latitude and longitude value of the current coordinate of B, add the latitude and longitude value of a point outside the circle, and draw a square with this distance as the side length. Scope. (According to Zenly's official explanation, the side length should be 1200M.)

Divide the square into 9 areas on average, modify the coordinates of C 9 times with the center point of each area as the target, and find 9 points that show the area closest to C.

Repeat the above steps until the positions of B and C coincide, that is, it is determined that the coordinates of C are the coordinates of B.

You can use more accounts to exhaustively list the position of B. In theory, the more accounts, the faster the speed and the shorter the time.

## Automated attacks (ideas)

> ideas

Use the Android emulator to run two instances, one logged in to the attacker account (A) and the other logged in to the robot account (C).

Use openCV and PyAutoGUI to observe and control instances A and C, obtain the position of A's friend B, modify the coordinates of instance C through the Android simulator, until A observes that the positions of B and C overlap, and finally print out the last position of C .

## Remark

> repair

If Zenly wants to solve the problem of fuzzy positioning, it should modify the random algorithm. If it detects users who are roughly at the same coordinates, it should perform different coordinate offsets for each user, instead of the same random offset position each time.

This project is only for sharing ideas, without any public code, all experimental accounts are my own accounts.
