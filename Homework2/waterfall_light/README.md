# 电控组第二次培训作业

- **陈曦皓**
- ***20263008811***
- 实现思路：      
首先，定义最新执行时间和步数。  
主要代码部分我们把延时阻塞HAL_Delay换成了HAL_GetTick计时装置， 这样在if假设外面while循环里面可以写额外的任务，让CPU可以充分利用，不是死等在那里。  
而if假设里面，我先定好时间为500毫秒，当时间超过500毫秒，就根据步数执行一次灯泡循环操作，步数为0就第一颗灯泡亮，为1就第二颗灯泡亮，以此类推。  
每执行一次if就更新一次最新执行时间，然后把步数加一，再把步数取余使之循环在零到四之间。  
就完成了非阻塞延时的流水灯的设计。
- 核心代码：   
while (1)  
{ if (HAL_GetTick()-last_time > 500)  
  {  
  HAL_GPIO_WritePin(LED0_GPIO_Port, LED0_Pin,(led_step==0u)?GPIO_PIN_SET:GPIO_PIN_RESET);
  HAL_GPIO_WritePin(LED1_GPIO_Port, LED1_Pin,(led_step==1u)?GPIO_PIN_SET:GPIO_PIN_RESET);
  HAL_GPIO_WritePin(LED2_GPIO_Port, LED2_Pin,(led_step==2u)?GPIO_PIN_SET:GPIO_PIN_RESET);
  HAL_GPIO_WritePin(LED3_GPIO_Port, LED3_Pin,(led_step==3u)?GPIO_PIN_SET:GPIO_PIN_RESET);
  HAL_GPIO_WritePin(LED4_GPIO_Port, LED4_Pin,(led_step==4u)?GPIO_PIN_SET:GPIO_PIN_RESET);

        last_time = HAL_GetTick();

        led_step++;
        led_step = led_step % 5;
      }