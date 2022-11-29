#include <iostream>
using namespace std;
#include <cstring>
#include <cassert>
#include <vector>
#include <iomanip>
#include <sstream>
class ProblemALG004r { // class of magic square class ProblemALG004r
    public:
    ProblemALG004r(int d,int r) :
    sqr(d*d,0), sz(d){
        assert(d&1);
        fillSqr();
        
    }
    void display(){
        cout << "Odd Magic Square: " << sz << " x " << sz << "\n\n\n";
        ostringstream cvr;
        cvr << sz * sz;
        int l = cvr.str().size();
        for( int y = 0; y < sz; y++ ){
            int yy = y * sz;
            for( int x = 0; x < sz; x++ )
            cout << setw( l + 2 ) << sqr[yy + x];
            cout << "\n";
            
        }
        cout << "\n\n";
        cout << "Sum of rows,column and diagonals is same and equal to : " << magicNumber() << "\n\n";
        
    }
    void magicSquare(int num){
        int magicSquare[num][num];  // set all slots as 0
        memset(magicSquare, 0, sizeof(magicSquare)); // Initialize position for 1
        int i = num / 2; // One by one put all values in magic square
        int j = num - 1;
        for(int num2 = 1; num2 <= num * num;){
            if (i == -1 && j == num){ // 3rd condition
                j = num - 2;
                i = 0;
                
            }
            else { // 1st condition helper if next numbern  // goes to out of square's right side
                if (j == num)
                j = 0; // if next number is goes to out of square's upper side
                if (i < 0)
                i = num - 1;
                
            }
            if (magicSquare[i][j]){
                j -= 2;
                i++;
                continue;
                
            }
            else
            magicSquare[i][j] = num2++; // set number
            j++;
            i--;
            
        }  	// Print magic square
        
        cout << "The Magic Square for n=" << num<< ":\n Sum of each row or column : "<< num * (num * num + 1) / 2 << "\n\n";
        for (i = 0; i < num; i++) {
            for (j = 0; j < num; j++) 
            cout << setw(4) << magicSquare[i][j] << " "; // setw(7) is used so that the matrix gets printed in a proper square fashion.
            cout << endl;
            
        }
        
    }
    private:
    void fillSqr(){
        int sx = sz / 2, sy = 0, c = 0;
        while( c < sz * sz ) 	{
            if( !sqr[sx + sy * sz] ){
                sqr[sx + sy * sz]= c + 1;
                inc( sx );
                dec( sy );
                c++;
                
            }
            else
            {
                dec( sx );
                inc( sy );
                inc( sy );
                
            }
            
        }
        
    }
    int magicNumber(){ // magic number (sum of row or cols)
        return sz * ( ( sz * sz ) + 1 ) / 2;
        
    }
    void inc( int& a ){ // increment by 1
        if( ++a == sz )
        a = 0;
        
    }
    void dec( int& a ){ // decrement by 1
        if( --a < 0 )
        a = sz - 1;
        
    }
    bool CheckPosition( int x, int y ) { // check  inside the square
        return( IsInside( x ) && IsInside( y ) && !sqr[sz * y + x] );
        
    }
    bool IsInside( int s ){
        return ( s < sz && s > -1 );
        
    }
    vector<int> sqr;
    int sz;
    };
    int main() {
        int n,rotation;
        cout << "Enter the dimensions of a magic square: "<<endl;
        cin>>n; // odd dimension
        cout << "Enter the rotation: "<<endl;
        cin>>rotation; // odd dimension
        ProblemALG004r a(n,rotation);
        if(rotation==1)
        a.magicSquare(n);
        else
        a.display();
        return 0;
        
    }
