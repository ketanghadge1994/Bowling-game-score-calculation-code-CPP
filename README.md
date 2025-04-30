#include <iostream>
#include <vector>

int main() {
    // User input
    std::vector<int> vec {
    1,4,
    4,5,
    6,4,
    5,5,
    10,
    0,1,
    7,3,
    6,4,
    10,
    2,8,6};
    
// Total no of frame
int frame = 10;
int totalScore = 0; //  total score
int strik = 0;
int spare = 0;
int vecIdx = 0;
for (int inx =0; inx <frame; inx++)
{
    std::cout<<"\n "; 
    int FrameNo = inx +1; // To show  the frame count
    std::cout<< "frame :" << FrameNo << "\n "; 
    int rollCount = 2;
    int roll1 = 0; //roll1value
    bool frame10Spare = false;
    for (int inxRoll =0; inxRoll < rollCount; inxRoll++)
    {
        int currroll = vec[vecIdx];
        if(inxRoll == 0 )
        {
            std::cout << "Roll1: " << currroll ;
        }
        else if(inxRoll == 1 && inx == 9 && frame10Spare == true )
        {
            std::cout << "   Roll3:" << currroll << "\n ";
        }
        else if(inxRoll == 1 )
        {
         std::cout << "   Roll2:" << currroll << "\n ";
        }
        
        if(strik > 0 )
        {
           totalScore += currroll;
           strik -=1;
           //std::cout<< "strik1 :" << strik << "\n ";
        }
        
        if(spare > 0 )
        {
           totalScore += currroll; 
           spare -=1;
        }
        
        if(inxRoll == 0 )
        {
            roll1 = currroll ;
            if(currroll == 10 && inx != 9)
            {
                strik +=2;
                rollCount = 0;
                totalScore += currroll;
                vecIdx++;
                std::cout<< "  Roll2 :" << "NA" << "\n ";
                break;
            }
            //std::cout<< "strik :" << strik << "\n "; 
        }
        else if(inxRoll == 1 )
        { 
            if((currroll + roll1) == 10 && inx != 9)
            {
                spare+=1;
            }
            else if((currroll + roll1) == 10 && inx == 9)
            {
                inxRoll = 0;
                frame10Spare = true;
            }
        }
        
        totalScore += currroll;
        vecIdx++;
    }
}
 std::cout<< "Score :" << totalScore << "\n ";   
    return 0;
}
