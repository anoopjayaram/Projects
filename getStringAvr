#include<stdio.h>
#include<avr\io.h>
#include<util\delay.h>
void trans(char);
char rec();
void cmd(int);
void data(char);
void TRANS_STRING(const char *p);
void main()
{
	char a;
	char RC[100],test[]="apple";
	char buffer[100];
	int i=0;
	DDRB=0XFF;
	DDRC=0XFF;
	DDRD=0X02;
	UCSRA=0X00;
	UCSRB=0X18;
	UCSRC=0X86;
	UBRRL=0X33;
	UBRRH=0X00;
	cmd(0X38);
	cmd(0X80);
	cmd(0X06);
	cmd(0X0E);
	cmd(0X01);
	TRANS_STRING("AT\rAT\r");
	while(1)
	{
		//TRANS_STRING("STARTED");
		

		do
		{
			RC[i]=rec();
			trans(RC[i]);
			i++;	
		}while(RC[i-1]!='\r');
		 RC[i]='\0';
		  
		    sprintf(buffer, "got ");
			//  strncat(test, buffer, 15);
			strncat(buffer, RC, 50);
			  TRANS_STRING(buffer);
		
		
	}
}

char rec()
{
	while((UCSRA&0X80)==0);
	return(UDR);
}

void trans(char b)
{
	UDR=b;
	while((UCSRA&0X40)==0);
	_delay_ms(500);
}

void cmd(int c)
{
	PORTB=c;
	PORTC=0X02;
	_delay_ms(500);
	PORTC=0X00;
}

void data(char d)
{
	PORTB=d;
	PORTC=0X03;
	_delay_ms(500);
	PORTC=0X01;
}

void TRANS_STRING(const char *p)
{
	while(*p!=0)
	{
		trans(*p);
		p++;
		
	}
	
}

/*



for (int k=0;RC[k]!='\r';k++)
{
	RC[k]=rec();
	trans(RC[k]);
	//TRANS_STRING("loop\r");
}
RC[i+1]='\0';
//TRANS_STRING("ENDED\r");
*/
