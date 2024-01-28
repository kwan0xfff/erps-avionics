# Real-Time OS Survey

This is a survey of a few real-time operating systems that began in early 2015.
There is a slant here toward free/open source software (F/OSS),
with an eye for rocket or spacecraft applications.
Much of this content originally appeared on the ERPS BB under
"Groups < Avionics" "real-time OS survey".
This page now also includes brief notes about drone software frameworks,
which include flight controller, comm, and ground control.

Rick's gut feel:
1. Arduino boards are mostly not powerful enough for rocket guidance and control (assuming you want active guidance).
2. Linux systems vary widely in their sufficiency for real-time application, and for hard real-time feedback, a lot of special work needs to be done (e.g., Xenomai). (Life could be really easy if I could be proven wrong. :-) )

As a result, I've been hunting for other alternatives. Below are some that stand out.

## Aerospace-originated RTOSs

### core Flight Executive (cFE)

Space flight application and run-time environment.

Resources:
- https://opensource.gsfc.nasa.gov/projects/cfe/index.php#software

### Portland State Aerospace Society (PSAS) Flight Computer

PSAS seems to be doing lots of good stuff.
From Space Access, it seems like their avionics is actively progressing.

Resources:
- PSAS Software: http://psas.pdx.edu/software/
- Flight Computer docs: http://psas-flight-computer.readthedocs.org/en/latest/


### Real-Time Executive for Multiprocessor Systems (RTEMS)

Used for a lot of space missions.
Got its start in Huntsville.
It has been a sponsored project of Google Summer of Code (GSoC).
Furthermore, it is part of ESA Summer of Code in Space.

Resources:
- Main site: https://www.rtems.org/
- Summer of Code 2014: https://www.rtems.org/node/109

## General RTOSs

Below are a couple of mainstay free RTOS systems; I’m not sure about their adoption into space or rocketry applications.

### FreeRTOS

Arguably the most popular open source RTOS.
Began around 2003, maintained by Real Time Engineers Ltd,
until 2017, when stewardship was passed to AWS.
Supported by many embedded board vendors.

Variants include:
- OpenRTOS - commercially licensed version from Wittenstein.
- SafeRTOS - proprietary derivative analyzed and tested for
  safety-critical application from Wittenstein.

Resources:
- main site: http://www.freertos.org/
- Github: https://github.com/FreeRTOS/FreeRTOS

### eCOS
Began in 1997 by Cygnus Solutions which was later acquired by RedHat.
Rights transferred to Free Software Foundation in 2004.
Last release was in March 2009.

Resources:
- main site: http://ecos.sourceware.org/

### Zephyr
Major focus on connected devices or Internet of Things (IoT).
Began in 2015 as the Rocket kernel by Wind River.
Became a project of the Linux Foundation in 2016.
Supported by many embedded board vendors.

Resources:
- main site: https://www.zephyrproject.org/
- Github: https://github.com/zephyrproject-rtos/zephyr

### VxWorks

VxWorks is a proprietary RTOS from Wind River.
It began as a series of enhancements to VRTX from Hunter-Ready
(later Ready Systems).
First release was in 1987.
It has been the mainstay of many interplanetary programs.
It is supported on a wide variety of architectures.
(It is a really expensive commercial product.)

Resources:

- main site: https://www.windriver.com/products/vxworks

## Drone RTOSs

### NuttX
Nuttx is an RTOS for 8-bit to 32-bit microcontroller environments.  Its primary API guidance comes from POSIX and ANSI standards. NuttX is used in drone autopilots like PX4, which is the flight stack of DroneCode.
- http://www.nuttx.org/
- https://pixhawk.org/dev/nuttx/start - PX4 boards using NuttX
- http://www.nuttx.org/doku.php?id=docume ... :userguide

### BeaglePilot / Erle-Brain
http://wiki.ros.org/Robots/Erle-brain

This is uses a port of ArduPilot to BeagleBone Black.

### Erle-Brain 3
https://erlerobotics.com/blog/product/erle-brain-3/

To keep up with advances in embedded Linux, the Erle-Brain family has migrated off of BeagleBone, and onto Raspberry Pi 3.
Includes ROS, a bunch of sensors, etc.

### Linux port for PX4 Flightstack
https://pixhawk.org/dev/ros/px4linux

As of 2015, this was a work in progress.
Normally, I tend to think that the people proposing Linux for real-time controls are fooling themselves.
However, this one proposes to use Xenomai V3, a co-resident real-time framework for catching interrupts before Linux does and determining if there is any real-time work to be done with them.
Xenomai V2 seems to have been highly successful, but the framework code is very tightly coupled to the Linux kernel itself.
And thus, you cannot blindly upgrade the Linux kernel without breaking the Xenomai framework.

### Qualcomm Snapdragon Flight Kit
https://ardupilot.org/copter/docs/common-qualcomm-snapdragon-flight-kit.html
https://docs.px4.io/v1.9.0/en/flight_controller/snapdragon_flight.html

The Snapdragon Flight platform utilizes the Snapdragon 801 processor, which includes a quad-core Krait CPU and Hexagon DSP.
The Krait CPU is based on the ARM64 architecture and runs Linux.
The Hexagon DSP is a multi-threaded VLIW (very long instruction word) architecture that runs the PX4 flight stack.
The platform also includes a 9-axis accel/gyro/mag sensor, video, optical flow, etc.
The Snapdragon Flight was adapted by NASA JPL to control the Mars helicopter, "Ingenuity".

## Drone software frameworks
The domain of flight controllers has migrated to 32-bit processors with floating point,
primarily the ST Microelectronics STM32F3/4/7 series,
which are based on the Cortex-M4 and higher M versions of the ARM architecture.
The flight controller software is accompanied by ground controller, communications, and calibration software.
This family of components essentially comprise a drone software framework.
At this writing (early 2017), the two most popular drone frameworks were DroneCode and CleanFlight.
Since then, interesting variations of CleanFlight have gained strength, specifically, BetaFlight and CleanFlight.

- Dronecode – a combination of PX4, MAVlink, and QGroundControl.
  - main site: https://www.dronecode.org
  - source code - directory of repos: https://www.dronecode.org/source_code/
- CleanFlight – a combination of the CleanFlight flight controller,
  CleanFlight-configurator (running on Google Chrome), and a variety of comm protocols.
  - main site: http://cleanflight.com
  - source code (controller): https://github.com/cleanflight/cleanflight
- BetaFlight - a popular, more cutting-edge fork of CleanFlight.
  Sometimes code from BetaFlight is merged back into CleanFlight.
  - wiki: https://github.com/betaflight/betaflight/wiki
  - source code (controller): https://github.com/betaflight/betaflight
- iNav - in the family of CleanFlight and BetaFlight, but with improvements for better integration with GPS
  - main site: http://inavflight.com/
  - source code (controller): https://github.com/iNavFlight/inav
