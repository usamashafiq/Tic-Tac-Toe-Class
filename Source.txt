#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <string>
#include <iostream>
#include<conio.h>
using namespace std;
class TicTacToe

{

private:

	int Position[9];

	int Player;

	int TurnCounter;

	int NumberOfPlayers;

	bool PlayerType[20];

public:

	TicTacToe();

	void PrintTurn();

	bool PlayerHuman();

	void HumanMove();

	void ComputerMove();

	void DrawBoard();

	bool Winner();

	bool FullBoard();

	void NextTurn();

}; //End of the Class Declaration
TicTacToe::TicTacToe()
{
	srand(time(0)); //Get a Random Number

	Player = 1; //Determines who starts first

	TurnCounter = 0; //Initializes the turn counter

	int i = 0;



	//Set up New Players when game begins

	NumberOfPlayers = 2;

	PlayerType[1] = 1; //PlayerType[Player] is the Human User(1)

	PlayerType[2] = 0; //PlayerType[Player] is the Computer (0)



	for (i = 0; i < 9; i++)

	{

		Position[i] = 0;

	}
}

void TicTacToe::DrawBoard()

{

	cout << endl

		<< Position[0] << " | " << Position[1] << " | " << Position[2]

		<< "\n--+---+--\n"

		<< Position[3] << " | " << Position[4] << " | " << Position[5]

		<< "\n--+---+--\n"

		<< Position[6] << " | " << Position[7] << " | " << Position[8]

		<< endl;

} //End Drawing the TicTacToe Board



void TicTacToe::PrintTurn()

{

	cout << "\nPlayer " << Player;

} //End Printing Turn



void TicTacToe::NextTurn()

{

	TurnCounter++;



	if (++Player > NumberOfPlayers)

	{

		Player = 1;

	}

} //End Next Turn



bool TicTacToe::PlayerHuman()

{
	return PlayerType[Player];

} //End Determination of A Human Player



void TicTacToe::HumanMove()

{
	cout << "\nEnter your move (1-9): ";
	int Move;
	do
	{
		cin >> Move;

		Move--; // For user to enter 1-9 instead of 0-8

	}

	while (Move < 0 || Move > 8 || Position[Move] != 0);

	Position[Move] = Player;

} //End the Human Move



void TicTacToe::ComputerMove()

{

	int Move;
	do {

		Move = rand() % 9; //Not really a Smart AI, Just picks a random move

	}

	while (Move < 0 || Move > 8 || Position[Move] != 0);

	Position[Move] = Player;
} //End the Computer Move



bool TicTacToe::Winner()

{

	int i = 0;

	int Board[8][3] = { { 0,1,2 },{ 3,4,5 },{ 6,7,8 },{ 0,3,6 },{ 1,4,7 },{ 2,5,8 },{ 0,4,8 },{ 2,4,6 } }; //List of all possible winning outcomes



	for (i = 0; i < 8; i++) //Loop for all possible winning outcomes

	{

		if ((Position[Board[i][0]] == Position[Board[i][1]]) && (Position[Board[i][1]] == Position[Board[i][2]]) && Position[Board[i][0]] != 0)

		{

			cout << "\nPlayer " << Position[Board[i][0]]

				<< " wins!\n\n";

			cout << "Press Enter to Close...." << endl;

			system("pause");

			return 1;  //Returns a true value (1 with the bool data type).

		}

	}

	return 0; //Else a winner has not been found yet, and return a false (0) value

} //End Checking the Winner



bool TicTacToe::FullBoard()

{

	if (TurnCounter == 9)

	{

		cout << "\nTie game!\n\n";

		return 1;

	}

	else

	{

		return 0;

	}

} //End Checking for a Full Board



void main()

{

	TicTacToe NewGame;


	cout << "The Game Board is step up in the following manner:" << endl << endl;
	cout << " 1 | 2 | 3 " << endl;
	cout << "---+---+---" << endl;

	cout << " 4 | 5 | 6 " << endl;
	cout << "---+---+---" << endl;
	cout << " 7 | 8 | 9 " << endl << endl;



	NewGame.DrawBoard();


	do
	{
		NewGame.PrintTurn();

		if (NewGame.PlayerHuman()) //If it is the Human turn, allow the human to move

		{
			NewGame.HumanMove();
		}

		else //Else if it is not the Human turn, it is the computer's turn

		{
			NewGame.ComputerMove();

		}


		NewGame.DrawBoard();
		NewGame.NextTurn();

	}

	while (!NewGame.Winner() && !NewGame.FullBoard()); //Execute the code in the do loop while there is no winner
													   //And the game board is not full
	_getch();

}
