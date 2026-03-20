##  STM32 Microsecond Delay

###  Description

This project showcases how to generate a square wave signal on an STM32 microcontroller using precise microsecond delays. A hardware timer (TIM2) is utilized to achieve accurate timing, and a GPIO pin is periodically toggled to create a waveform that can be viewed on an oscilloscope.

---

###  Objective

* Create a square wave using microsecond-level delay
* Understand how hardware timers can be used for precise timing
* Observe and verify the output waveform using an oscilloscope

---

###  Hardware Used

* STM32F401 microcontroller (or any compatible STM32 board)
* Oscilloscope (for signal observation)
* Jumper wires

---

###  Working Principle

The timer (TIM2) is configured in such a way that:

👉 Each increment of the timer corresponds to **1 microsecond**

By leveraging this behavior, the program can introduce accurate delays and toggle a GPIO pin at fixed intervals, resulting in a stable square wave output.

### Timer Configuration

Timer: TIM2
Prescaler: 84 - 1
System Clock: 84 MHz
Timer Frequency: 1 MHz
Resolution: 1 µs

### Code Implementation

Start Timer
HAL_TIM_Base_Start(&htim2);
Starts TIM2 so that it begins counting. Without this, delay will not work.

Microsecond Delay Function
while (1)
{
    HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_8);
    delay_us(100);
}

Functionality:

If the pin is LOW, it becomes HIGH
If the pin is HIGH, it becomes LOW
By toggling the pin with a fixed delay, a square wave signal is generated.

Square Wave Generation
void delay_us(uint32_t us)
{
    __HAL_TIM_SET_COUNTER(&htim2, 0);
    while (__HAL_TIM_GET_COUNTER(&htim2) < us);
}

Functionality:

Resets the timer counter to zero
Waits until the timer reaches the specified value
Since each count equals 1 µs, the delay is accurate
