1. this is how you can solve a sudoku type problem
```cpp
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        int col=1,row=1;
        auto valid= [](vector<char> cr){

            for (auto c : cr){
                if(c=='.')continue;
             if (count(cr.begin(),cr.end(),c)>1){
                return false;
             }
            }
            return true;
        };

        vector<char> temp;
// Each row must contain the digits 1-9 without duplicates

for (auto i : board){
    if(valid(i)==false){
        return false;
    }
}




//Each column must contain the digits 1-9 without duplicates
  
  for (int i =0;i<9;i++){
     for (int j =0;j<9;j++){
        
        temp.push_back(board[j][i]);
  }
    if(valid(temp)==false){
        return false;
    } 
    temp.clear();
  }

   
//Each of the nine 3 x 3 sub-boxes of the grid must contain the digits 1-9 without duplicates
         for(int r =0;r<3;r++  ){
             for(int c =0;c<3;c++  ){

                for (int i = (r*3); i<((r+1)*3);i++){
                    for (int j = (c*3); j<((c+1)*3);j++){
                            temp.push_back(board[i][j]);

                            }

                }
                if(valid(temp)==false){
                     return false;
                        } 
                temp.clear();


                
       }


       }


     return true;


    }
};
```


