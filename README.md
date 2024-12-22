1)7 SEGMENTS

include <REGX51.H>
unsigned char code segmentTable[16] = { 
    0x3F, // 0
    0x06, // 1
    0x5B, // 2
    0x4F, // 3
    0x66, // 4
    0x6D, // 5
    0x7D, // 6
    0x07, // 7
    0x7F, // 8
    0x6F, // 9
    0x77, // A
    0x7C, // B
    0x39, // C
    0x5E, // D
    0x79, // E
    0x71  // F
};

void delay() {
    unsigned int i, j;
    for (i = 0; i < 500; i++) {
        for (j = 0; j < 100; j++);
    }
}

void main() {
    unsigned int count = 0; 
    unsigned char lowNibble, midNibble, highNibble;

    while (1) {
        
        lowNibble = count & 0x0F;         
        midNibble = (count >> 4) & 0x0F; 
        highNibble = (count >> 8) & 0x0F; 

    
        P1 = segmentTable[lowNibble];    
        P2 = segmentTable[midNibble]; 
        P3 = segmentTable[highNibble];  

        delay(); 

        count++; 

        if (count > 0xFFF) { 
            count = 0;
        }
    }
}
 


2)TRAFFIC LIGHT SYSTEM USING 8051 MICRO-CONTROLLER

#include<reg51.h>
//signal 1
sbit tl1r = P2^0;     
sbit tl1o = P2^1;      
sbit tl1g = P2^2;    


sbit tl2r = P2^3; 
sbit tl2o = P2^4;     
sbit tl2g = P2^5;    


sbit tl3r = P3^0;    
sbit tl3o = P3^1;    
sbit tl3g = P3^2;    


void delay(int t);          
void trafficlight(void);
void main()                  
{                 
	P2=0x00;         
	P3=0x00;        
	
  while(1)
     {
	trafficlight();	
     }

}
void delay(unsigned long int t)              
{
	while(t>0)
	{
	unsigned long int i;
	for(i=1;i<10*1275;i++);
		t--;
	}
}
void trafficlight(void)        
{
P2= 0x11;  
P3= 0x04;
	/*
tl1r=1;    
tl1o=0;	
tl1g=0;

tl2r=0;  
tl2o=1;
tl2g=0;

tl3r=0; 
tl3o=0;
tl3g=1;

delay(100);    
P2= 0x0c;    
P3= 0x02;
 
tl1r=0;     
tl1o=0;	
tl1g=1;
	
tl2r=1;    
tl2o=0; 
tl2g=0;

tl3r=0;    
tl3o=1;
tl3g=0;	

delay(100);  
P2= 0x22;  
P3= 0x01;
 
tl1r=0;   
tl1o=1;	
tl1g=0;

tl2r=0;   
tl2o=0;
tl2g=1;

tl3r=1;  
tl3o=0;
tl3g=0;	

delay(100);  
}


3)ELAVATOR

#include <REGX51.H>


unsigned char code segmentTable[4] = {0x06, 0x5B, 0x4F, 0x66}; 


sbit FLOOR1 = P2^0; 
sbit FLOOR2 = P2^1;
sbit FLOOR3 = P2^2; 
sbit FLOOR4 = P2^3; 


void delay(unsigned int time) {
    unsigned int i, j;
    for (i = 0; i < time; i++) {
        for (j = 0; j < 120; j++);
    }
}


void displayFloor(unsigned char floor) {
    P1 = segmentTable[floor]; 
}

void main() {
    unsigned char currentFloor = 0; 

    while (1) {
        
        if (FLOOR1 == 0) { 
            while (currentFloor > 0) {
                currentFloor--;       
                displayFloor(currentFloor);
                delay(500);          
            }
        } else if (FLOOR2 == 0) { 
            while (currentFloor < 1) {
                currentFloor++;    
                displayFloor(currentFloor);
                delay(500);        
            }
            while (currentFloor > 1) {
                currentFloor--;      
                displayFloor(currentFloor);
                delay(500);
            }
        } else if (FLOOR3 == 0) {
            while (currentFloor < 2) {
                currentFloor++;       
                displayFloor(currentFloor);
                delay(500);
            }
            while (currentFloor > 2) {
                currentFloor--;       
                displayFloor(currentFloor);
                delay(500);
            }
        } else if (FLOOR4 == 0) {
            while (currentFloor < 3) {
                currentFloor++;       
                displayFloor(currentFloor);
                delay(500);
            }
        }
    }
}
  
