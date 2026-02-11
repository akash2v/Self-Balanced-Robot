Here is your updated `README.md` without emojis and with images inserted from `assets/1.jpg` to `assets/5.jpg`.

---

# Self Balancing Robot (Arduino + MPU6050 + PID)

This project implements a two-wheel self-balancing robot using:

* Arduino
* MPU6050 (with DMP enabled)
* PID control algorithm
* L298N (or compatible) motor driver
* Custom `LMotorController` library

The robot continuously reads tilt data from the MPU6050 and applies PID control to keep itself balanced vertically.

---

## Project Preview

![Robot View 1](/assets/1.webp)

---

## Features

* Real-time angle estimation using MPU6050 DMP (Digital Motion Processor)
* PID-based stabilization
* Live PID tuning via Serial Monitor
* Adjustable motor speed compensation (left/right factors)
* Interrupt-driven sensor reading for efficient performance

---

## How It Works

1. The MPU6050 provides orientation data (Yaw, Pitch, Roll).
2. The robot uses the pitch angle as input.
3. A PID controller calculates corrective motor output.
4. Motors rotate forward or backward to maintain vertical balance.

The control loop continuously:

* Reads angle from DMP
* Computes PID output
* Drives motors accordingly

---

## Hardware Requirements

* Arduino Uno (or compatible)
* MPU6050 (I2C)
* L298N Motor Driver (or equivalent)
* 2 DC geared motors
* Robot chassis
* External battery (7–12V recommended)

---

## Pin Configuration

### Motor Driver Pins

| Function | Pin |
| -------- | --- |
| ENA      | 11  |
| IN1      | 7   |
| IN2      | 6   |
| IN3      | 5   |
| IN4      | 4   |
| ENB      | 10  |

MPU6050 uses I2C (SDA, SCL).

---

## Required Libraries

Install the following libraries before uploading:

* PID_v1
* I2Cdev
* MPU6050_6Axis_MotionApps20
* LMotorController

---

## PID Parameters

Default values:

```
Kp = 60
Ki = 200
Kd = 2.2
```

These values must be tuned according to your robot’s weight, motor power, and battery voltage.

---

## Live PID Tuning (Serial Monitor)

Open Serial Monitor at 115200 baud.

Use the following keys to adjust parameters in real time:

| Key   | Action                 |
| ----- | ---------------------- |
| q / a | Increase / Decrease Kp |
| w / s | Increase / Decrease Kd |
| e / d | Increase / Decrease Ki |

Updated values will be printed in the Serial Monitor.

---

## Calibration Notes

Adjust gyro and accelerometer offsets if necessary:

```cpp
mpu.setXGyroOffset(0);
mpu.setYGyroOffset(0);
mpu.setZGyroOffset(0);
mpu.setZAccelOffset(0);
```

Proper calibration is critical for stable balancing.
See This Article for Calibration Code - [Click Here ]([url](https://wired.chillibasket.com/2015/01/calibrating-mpu6050/))
---

## Important Parameters

* `MIN_ABS_SPEED = 30`
  Prevents motors from stalling at low speeds.

* `motorSpeedFactorLeft` and `motorSpeedFactorRight`
  Used to compensate for motor mismatch.

---

## Upload Instructions

1. Connect Arduino.
2. Install required libraries.
3. Select correct board and port.
4. Upload the `.ino` file.
5. Open Serial Monitor at 115200 baud.
6. Place the robot upright and tune PID carefully.

---

## Troubleshooting

### MPU6050 Connection Failed

* Check SDA/SCL wiring.
* Confirm I2C address (usually 0x68).
* Verify power supply.

### Robot Falls Immediately

* PID values not tuned correctly.
* Motor direction reversed.
* Incorrect gyro offsets.
* Low battery voltage.

### FIFO Overflow Error

If you see:

```
FIFO overflow!
```

The loop may be too slow or wiring may be unstable.

---

## Future Improvements

* Bluetooth-based PID tuning
* Mobile app interface
* Forward/backward motion control
* Advanced calibration routine
* Improved sensor fusion

---

## License

This project is open-source. Modify and improve as needed.
