# Suduko-Game
#include<bits/stdc++.h>
#include<string>
using namespace std;
#define N 9
bool issafe(int grid[N][N] , int row , int col  , int num){
    bool a = true;
    //safe  for row:
    for(int i = 0 ; i<N ; i++){
        if(grid[row][i] == num){
            return false;
        }
    } 
    //safe for col:
    for(int i = 0 ; i<N ; i++){
        if(grid[i][col] == num){
            return false;
        }
    }
    //safe for both row and col for mini box 3*3:
    int rowfactor = row-(row%3);
    int colfactor = col-(col%3);
    for(int i = 0 ; i<3 ; i++){
     for(int j = 0 ; j<3 ; j++){
         if(grid[rowfactor+i][colfactor+j] == num){
             return false;
          }
       }
    }
    return true;
}
bool findemptylocation(int grid[N][N] , int &row , int &col){
    for(int i = 0 ; i<N ; i++){
        for(int j = 0 ; j<N ; j++){
            if(grid[i][j] == 0){
                row = i;
                col = j;
                return true;
            }
        }
    }
    return false;
}
bool solvesudoku(int grid[N][N]){
    int row , col;
    if(!findemptylocation(grid , row , col)){
        return true;
    }
    for(int i = 1; i<=9 ; i++){
        if(issafe(grid , row , col , i)){
            grid[row][col] = i;
            if(solvesudoku(grid)){
                return true;
            }
            grid[row][col] = 0;
        }
    }
    return false;
}
int main(){
  int grid[N][N];
    for(int i = 0 ; i<N ; i++){
         for(int j=0;j<N;j++)
        {
            cin>>grid[i][j];
        }
    }
    if(solvesudoku(grid)){
        cout<<"true"<<endl;
    }
    else{
        cout<<"false"<<endl;
    }
    return 0;
}
