# Zephyr2048

A Zephyr RTOS port of the classic **2048** game, powered by [LVGL](https://lvgl.io/) on the **FRDM_MCXN947** development board with the **lcd_par_s035_8080** shield.

![2048 on Zephyr](assets/screenshot.png)

## Features

- **Smooth 4×4 grid** rendered with LVGL  
- **Classic 2048 color palette** and tile animations  
- **Swipe‑to‑move** gesture support  
- **Optional on‑screen arrow buttons** (enable via `CONFIG_2048_USE_BUTTONS_TO_MOVE`)  
- **Game‑over detection** and “Game Over” overlay  

## Hardware

- **Board:** FRDM_MCXN947 (NXP MCU)  
- **Shield:** lcd_par_s035_8080 (16‑bit 8080‑parallel TFT LCD)

## Prerequisites

- [Zephyr SDK](https://docs.zephyrproject.org/latest/getting_started/index.html) (with CMake, Ninja, Python, west)  
- West tool (v0.12 or later)  
- LVGL module in `modules/lib/lvgl` (pulled in by your `west.yml`)  

## Getting Started

1. **Clone application** :

   ```bash
   west init -l lvgl_2048_zephyr
   west update
   west build --board frdm_mcxn947/mcxn947/cpu0

## Known Issues & Workarounds

### Touch controller timing tweak

If you see missed touches, edit  
`zephyr/drivers/input/input_gt911.c` and locate the comment:

```c
/* hold down 50ms to make sure the address available */
k_sleep(K_MSEC(50));

Change it to 200