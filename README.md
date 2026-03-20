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

## Code Implementation

### Start Timer

```c
HAL_TIM_Base_Start(&htim2);
```

Starts the timer so it begins counting. This step is necessary because the delay function depends on the timer value.

---

### Microsecond Delay Function

```c
while (1)
{
    HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_8);
    delay_us(100);
}
```

**Functionality:**

* When the pin is LOW, it switches to HIGH
* When the pin is HIGH, it switches to LOW
* Repeating this with a fixed delay produces a square wave

---

### Square Wave Generation

```c
void delay_us(uint32_t us)
{
    __HAL_TIM_SET_COUNTER(&htim2, 0);
    while (__HAL_TIM_GET_COUNTER(&htim2) < us);
}
```

**Functionality:**

* Resets the timer counter before starting
* Waits until the counter reaches the required value
* Since each count equals 1 µs, the delay is precise

---
