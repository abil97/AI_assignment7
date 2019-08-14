Assingment 7. 26/10/18
======================================================

General notes:
======================================================

- This program executes the instructions given in the assignment7
- This program is an updated and upgraded version of program used in the last assignment
- Some algorthms were updated as well as bugs and errors were fixed
- All code was written by myself only. I did not use anybody's else code
- When constructing a maze, there are 12 parameters to input: N,K,k,p,M,H,W,G,T,sigma,omega,tau
	As before:	N - Number of rooms totally
			K - Number of border rooms
			k - Number of connections of ordinary rooms
			p - Number of connections of border rooms
			M - Number of monsters
			H - Number of holes
			W - Number of walls
			G - Number of gold
			T - Number of teleports
			sigma - denotes spread.
			omega - denoted decay. 
			tau - denoted number of cycles

	Greek symbols of sigma, omega, and tau: σ, ω, τ are not supported in Python 2.7 because they are Non-ASCII characters. 
	Because of that their names are written manually

- Number of rooms and their connections should satisfy following conditions: N > K, p > k. Otherwise error will be returned
- Program uses Havel-Hakimi algorithm to check if it is possible to create a maze with the following input. If it isn't possible, error will be returned
	- In the maze all items (monsters, walls , holes, gold, teleports) are distributed in a way such that:
	- No more than 1 item in each room
	- However, two monsters can be in one room
	- M + W + H + G + T < N. Otherwise error will be thrown
	- Number of any item cannot be negative
	- Number of teleports cannot be less than 2. One teleport in total makes no sense and an error will be thrown

- Spread and decay cannot be negative. Also decay should be <= 1, otherwise smell will increase, which makes no sense. An error will be thrown in such case
- Decay is implemented in such way that it should not be > 1. For example, if decay is 0.5, each consequent room will be multiplied by 0.5. 
- Monsters can be of two types: loner and social, which is selected randomly. For this assignment, all monsters will be of only one type
- When program is started, type of all monsters will be printed in the beginning
- Loner monster feels the MAX smell in the room, Social monster feels SUM of all smells in the room except its own
- Monsters are implemented in such way that they remember the path they have travelled
- If the monster is social, it percieves the sum of all smells except its own
- If the monster is loner, it perceives the MAX value of all smells, except its own
- Loner monster returns in the prevoius room, if value of smell in the previous room is less than value of smell in the current rooom. Also there should be no violations in previous room
- Social monster returns in the previous room, if the summ of smells in the previous room is greater than in the current room. Also there should be no violations in previous room
- Violations include:
	- If there is wall/hole in the previous room, so that monster need to return back
	- If there is teleport in the current room. Monster cannot teleport back, since destination is choosed randomly
	- If there is another monster in prevoius room:
		- Loner monster should stay away from other monsters
		- Social monster cannot be in the same room with another monster
		- Conditions above are mentioned in the assignment
- If monster cannot go back, it moves randomly to the neighbour room

 
======================================================

Running the program
======================================================

1. There is a folder in the archive: assignment7. It could be extracted in any directory
2. In the terminal, change the directory to assignment7
3. In the terminal, type: python maze.py
4. If you want to create the maze, type: initMaze N K k p M W H G T sigma omega tau
	- "initMaze" is case insensitive
	- Generated maze with requested number of cycles will be printed to console
	- Also, generated maze will be printed to file output.txt. 
	- In this file output, wind and smell are not spreaded, and only initial state of maze is printed
5. If you want to load the maze, type: loadMaze filename sigma omega tau
	- filename is assumed to be input.txt .However, it can be any text file in current directory.
	- The format of the maze to be read from the file, should be as specified in the assignment: id:M,W,H,G,T,w,s connected_rooms

			General format: 	id:M,W,H,G,T,w,s connected_rooms
			1. There should be no spaces if this part: id:M,W,H,G,T,w,s
			2. Connected_rooms should be separated by space
			Otherwise, input will not be read correctly
			3. Wind and smell should be initially set to 0.			

			Example of correct input: 
			
			9:0,0,0,0,0,0 4 2 10 6 7 
			7:0,0,1,0,0,0 3 2 9 5 1 
			1:0,0,1,0,0,0 8 7 6 
			3:1,0,0,0,0,0 5 7 6 
			2:0,1,0,0,0,0 8 9 7 
			6:0,1,0,0,0,0 3 10 9 1 5 
			4:1,0,0,0,0,0 8 9 5 
			8:0,0,0,0,0,0 4 2 10 5 1 
			10:0,0,0,0,0,0 6 8 9 
			5:0,0,1,0,0,0 3 4 8 7 6 

	- The maze that was read will be printed to the terminal with updated values of smell and wind

6. Only rooms that were changed will be printed. But sometimes all rooms are changed because of smell spreading

=========================================================

Contact info:
=========================================================

Author: Abil' Kuatbayev
Email: abil.kuatbayev@nu.edu.kz
