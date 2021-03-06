# PS2控制舵机转动

## 实验目的：

通过ps2手柄转动控制舵机转动

## 实验所需函数

HAL_TIM_Base_Init(&htim3);

HAL_TIM_PWM_Start(&htim3,TIM_Channel_1);

HAL_ADC_Start(&hadc1);

HAL_ADC_PollForConversion(&hadc1,10);

HAL_ADC_GetValue(&hadc1);

## 步骤

### 1. 开启AD转换

### 2. 查询舵机转动所需脉冲宽度

![](.\image\6.png)

### 3.编写程序进行控制

故预分配71，ARR设为19999，可得到20ms的时基脉冲。并设置初始状态（ps2为中间状态）CCR为1500。当ps2手柄滑动时，stm32可由ADC得到一个11位（0~4095）的数字信号。故ps2手柄到最高值时仅有4095，我们将它减去2047，并除以2048乘以500，于是手柄最高值时pwm脉宽为2000，最低时为1000。

![](.\image\7.png)

## 总结

该实验需要注意的点有：

1.ADC的范围仅有0到4095

2.舵机的时基脉冲为20ms，脉冲宽度一般在0.5ms到2.5ms，即中间位置为1.5ms

3.注意转换比例使其一一映射。即2048-----500。