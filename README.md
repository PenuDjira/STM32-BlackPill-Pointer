# STM32F411CEU6 BLack Pill - Pointer (Bare Metal)
We will tried to control the on board LED + we add a LED on pin 14
We do Direct register access. No HAL. No Library. Just Manual Reference

## What this does?
 - Pointer RCC AHB1ENR addresses and saves it on pointer
 - After that we enable the RCC AHB1ENR with bitwise operation
```c
	*pRCC_AHB1ENR |= (1U << 2);
```
 - Pointer to GPIOC_MODER addresses
 - Clear the bit then set the bit
```c
	// Use technique to combined the clearing bit for both of bit 26,28
  *pGPIOC_MODER &= ~((3U << 26) | (3U << 28));
	
	// Use technique to combined the setting bit for both of bit 26,28
  *pGPIOC_MODER |= ((1U << 26) | (1U << 28));
```
 - Raw pointer to GPIOC ODR Register
 ```c
   // Address: GPIOC base (0x40020800) + ODR offset (0x14)
  uint32_t *pGPIOC_ODR = (uint32_t*) 0x40020814;
```

## Hardware i use
- STM32F411CEU6 WeAct Black Pill
- WeAct Mini ST-Link (SWD)
- Pop!_OS 22.04 | STM32CubeIDE 2.0.0 | STM32CubeMX 6.17

## Register used
| Register | Address | Purpose |
|----------|---------|---------|
| RCC_AHB1ENR | 0x40023830 | Enable GPIOC + GPIOC clocks |
| GPIOC_MODER | 0x40020800 | PC13 and PC14 as output (01) |
| GPIOC_ODR | 0x40020814 | Control PC13 and PC14 LED |


# Key Concept i Learned
- Memory Mapped I/O: Hardware registers = memory addresses
- How to combined the clearing bit just in a line of code
- How to combined the setting bit judt in a line of code
# WARNING!!!!!!
Always read your manual reference for the addresses
If you use this code, always re-check the addresses if you use different MCU
You can download the FREE MANUAL REFERENCE FROM OFFICIAL ST WEBSITE
just search on internet specific with your MCU series number

# Reference
RM0383 - STM32F411 Reference Manual
