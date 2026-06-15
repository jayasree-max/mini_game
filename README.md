# mini_game
#include <iostream>
using namespace std;

char board[3][3] = {
    {'1','2','3'},
    {'4','5','6'},
    {'7','8','9'}
};

char player = 'X';

void displayBoard() {
    cout << "\n";
    for(int i=0;i<3;i++) {
        for(int j=0;j<3;j++) {
            cout << " " << board[i][j] << " ";
            if(j<2) cout << "|";
        }
        cout << "\n";
        if(i<2) cout << "---|---|---\n";
    }
}

bool checkWin() {
    for(int i=0;i<3;i++) {
        if(board[i][0]==board[i][1] &&
           board[i][1]==board[i][2])
            return true;

        if(board[0][i]==board[1][i] &&
           board[1][i]==board[2][i])
            return true;
    }

    if(board[0][0]==board[1][1] &&
       board[1][1]==board[2][2])
        return true;

    if(board[0][2]==board[1][1] &&
       board[1][1]==board[2][0])
        return true;

    return false;
}

bool move(int position) {
    int row=(position-1)/3;
    int col=(position-1)%3;

    if(board[row][col]=='X' || board[row][col]=='O')
        return false;

    board[row][col]=player;
    return true;
}

void reset() {
    char num='1';

    for(int i=0;i<3;i++)
        for(int j=0;j<3;j++)
            board[i][j]=num++;
}

int main() {

char again;

do {
reset();
player='X';

int turns=0;

while(true) {

displayBoard();

int pos;

cout << "\nPlayer " << player
<< " Enter Position (1-9): ";
cin >> pos;

if(pos<1 || pos>9 || !move(pos)) {
cout << "Invalid Move!\n";
continue;
}

turns++;

if(checkWin()) {
displayBoard();

cout << "\nPlayer "
<< player
<< " Wins!\n";

break;
}

if(turns==9) {
displayBoard();
cout << "\nGame Draw!\n";
break;
}

player=(player=='X') ? 'O' : 'X';
}

cout << "\nPlay Again? (Y/N): ";
cin >> again;

} while(again=='Y' || again=='y');

cout << "\nThanks for Playing!";

return 0;
}