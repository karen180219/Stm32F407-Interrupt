# Stm32F407-Interrupt
experiment to know how the interrupt works
1.	EXTI2_IRQn 程序
//外部中断2服务程序
void EXTI2_IRQHandler(void)
{	delay_ms(10);	//消抖
	if(KEY2==0)	  
	{	LED0=!LED0; 		}	
	for (int i=0;i<100;i++)
	{	   delay_ms(500);
		LED0=!LED0; 		}
	EXTI->PR=1<<2;  //清除LINE2上的中断标志位  
}
2.	MY_NVIC_Init(3,2,EXTI2_IRQn,2);		//抢占3，子优先级2，组2    PE2
	MY_NVIC_Init(2,2,EXTI3_IRQn,2);		//抢占2，子优先级2，组2	   PE3
	MY_NVIC_Init(1,2,EXTI4_IRQn,2);		//抢占1，子优先级2，组2	   PE4
	MY_NVIC_Init(0,2,EXTI0_IRQn,2);		//抢占0，子优先级2，组2	   PA0
2,0，3，4都可以互相中断
3.	MY_NVIC_Init(0,2,EXTI2_IRQn,2);		//抢占0，子优先级2，组2    PE2
	MY_NVIC_Init(2,2,EXTI3_IRQn,2);		//抢占2，子优先级2，组2	   PE3
	MY_NVIC_Init(1,2,EXTI4_IRQn,2);		//抢占1，子优先级2，组2	   PE4
	MY_NVIC_Init(0,2,EXTI0_IRQn,2);		//抢占0，子优先级2，组2	   PA0
0，3，4不可以中断2，0.3.4可以互相中断，2可以中断0，3，4
4.	MY_NVIC_Init(3,2,EXTI2_IRQn,0);		//抢占3，子优先级2，组0    PE2
MY_NVIC_Init(2,2,EXTI3_IRQn,2);		//抢占2，子优先级2，组2	   PE3
MY_NVIC_Init(1,2,EXTI4_IRQn,2);		//抢占1，子优先级2，组2	   PE4
MY_NVIC_Init(0,2,EXTI0_IRQn,2);		//抢占0，子优先级2，组2	   PA0
0，3，4不可以中断2，

5.	MY_NVIC_Init(3,2,EXTI2_IRQn,2);		//抢占3，子优先级2，组2    PE2
MY_NVIC_Init(2,2,EXTI3_IRQn,0);		//抢占2，子优先级2，组0	   PE3
MY_NVIC_Init(1,2,EXTI4_IRQn,2);		//抢占1，子优先级2，组2	   PE4
MY_NVIC_Init(0,2,EXTI0_IRQn,2);		//抢占0，子优先级2，组2	   PA0
0，3，4都可以中断2，
6.	MY_NVIC_Init(1,2,EXTI2_IRQn,2);		//抢占3，子优先级2，组2    PE2
MY_NVIC_Init(2,0,EXTI3_IRQn,2);		//抢占2，子优先级2，组2	   PE3
MY_NVIC_Init(1,2,EXTI4_IRQn,2);		//抢占1，子优先级2，组2	   PE4
MY_NVIC_Init(0,2,EXTI0_IRQn,2);		//抢占0，子优先级2，组2	   PA0
只有0可以中断2；3，4不可以中断2
