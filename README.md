# Tic-Tac-Toe
#include<iostream>
using namespace std;

char board[3][3]={{'1','2','3'},{'4','5','6'},{'7','8','9'}};
int current_player=1;
char current_marker='X';

void create_board(){
    for(int i=0;i<3;i++){
        for (int j=0;j<3;j++){
            cout<<" ";
            cout<<board[i][j];
            if(j<2){
            cout<<" | ";
        }
        }
        cout<<"\n";
        if(i<2){
            cout<<"---|----|---\n";
        } 
    }
}

int winner(){
    for(int i=0;i<3;i++){
        if(board[i][0]==board[i][1] && board[i][1]==board[i][2]){
        return current_player;
    }
    if(board[0][i]==board[1][i] && board[1][i]==board[2][i]){
        return current_player;
    }
    }
    
    if(board[0][0]==board[1][1] && board[1][1]==board[2][2]){
        return current_player;
    }
    if(board[0][2]==board[1][1] && board[1][1]==board[2][0]){
        return current_player;
    }
    return 0;
}

void swap_player(){
    if(current_marker=='X'){
        current_marker='O';
        current_player=2;
    }
    else{
        current_marker='X';
        current_player=1;
    }
}

bool place_marker(int slot){
    int i=(slot-1)/3;
    int j=(slot-1)%3;
    if(board[i][j]!='X' || board[i][j]!='O'){
        board[i][j]=current_marker;
        return true;
    }
    return false;
}

void game(){
    cout<<"PLaying my fav glam game Tic Tac Toe!\n";
    cout<<"Player 1 is X and Player 2 is Y\n";
    create_board();
    current_player=1;
    current_marker='X';
    
    int player_won;
    
    for(int i=0;i<9;i++){
        int slot;
        cout<<"Player "<<current_player<<" insert your marker: ";
        cin>>slot;
        
        if(slot>9 || slot<1){
            cout<<"Invalid pls try again!";
            i--;
            continue;
        }
        
        if(!place_marker(slot)){
            cout<<"Sorry this slot is slready fll try again";
            i--;
            continue;
        }
        create_board();
        
        player_won=winner();
        
        if(player_won==1 || player_won==2){
            cout<<"Congratulations "<<player_won<<" you won the game!";
            return;
        }
        swap_player();
    }
    cout<<"Its a draw";
}
int main(){
    game();
}
