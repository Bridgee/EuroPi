# Setting up and programming the EuroPi

This document will take you through the steps to get your module ready to program.  
  
## NOTE:
If you already have any version of the firmware or any other code loaded onto your EuroPi and want to ensure a clean installation, or you just want to make sure you have all the most recent scripts available, first follow these instructions:

1. Download [flash_nuke.uf2](https://learn.adafruit.com/getting-started-with-raspberry-pi-pico-circuitpython/circuitpython) from Adafruit.
  
2. Holding down the white button labeled 'BOOTSEL' on the Raspberry Pi Pico, connect the module to your computer via the USB cable.  

![_DSC2400](https://user-images.githubusercontent.com/79809962/148647201-52b0d279-fc1e-4615-9e65-e51543605e15.jpg)

3. Open your file manager and drag and drop the downloaded `flash_nuke.uf2` onto the new drive named 'RPI-RP2'. This will wipe your Pico clean, ready for a new installation of the firmware.  

4. The Pico will automatically eject once the process is completed.  
  
5. Continue to [Setting Up](#setting-up) as normal.

  
  
## Setting Up
  
### Downloading Thonny
To start with, you'll need to download the [Thonny IDE](https://thonny.org/). This is what you will use to program and debug the module.  

![Thonny](https://i.imgur.com/UX4uQDO.jpg)

### Installing the firmware
1. Download the [most recent firmware](https://micropython.org/download/rp2-pico/) from the MicroPython website.
2. Holding down the white button labeled 'BOOTSEL' on the Raspberry Pi Pico, connect the module to your computer via the USB cable.

    ![_DSC2400](https://user-images.githubusercontent.com/79809962/148647201-52b0d279-fc1e-4615-9e65-e51543605e15.jpg)

3. Open your file manager and drag and drop the downloaded .uf2 onto the new drive named 'RPI-RP2'.
4. The Pico will automatically eject once the process is completed.

### Installing the OLED library
1. Disconnect the Pico from the USB cable.
2. Reconnect, this time without holding down the button on the back.

    ![_DSC2401](https://user-images.githubusercontent.com/79809962/148647207-b43a2e44-0ca2-48d0-b13c-b5d091b44ae1.jpg)

3. Open up Thonny if not already open, and go to the bottom right where you can select the interpreter.
4. Click to select interpreter and choose 'MicroPython (Raspberry Pi Pico)'.

    ![Interpreter Select](https://i.imgur.com/XeRem1w.jpg)

5. Click Tools -> Manage Packages to open the package manager.
6. Type 'ssd1306' into the search box and click 'Search on PyPi'
7. Click the result named 'micropython-ssd1306'.

    ![ssd1306 library](https://i.imgur.com/7t2mWHh.jpg)

8. Click 'Install'.
9. You will see that a folder has been created inside the Pico named 'lib', which contains the new file 'ssd1306.py'.

    ![ssd1306 inside lib](https://i.imgur.com/jkmeaFM.jpg)

### Installing the EuroPi library

Use the exact same process as for the ssd1306 library to install the europi library:
1. Type 'europi' into the search box and click 'Search on PyPi'
2. Click the result named 'micropython-europi'.

    ![image](https://user-images.githubusercontent.com/79809962/156630180-7f727567-89b1-4b8a-a3e0-63f2da3ea30c.png)

3. Click 'Install'.
4. You will now see several new files, including 'europi.py' alongside the 'ssd1306.py' inside the 'lib' folder.

## Next Steps

Now that you have installed the europi.py and ssd1306 libraries, you are ready to take the next step with the module.  

* [Option 1](#write-your-own-program-from-scratch): Start writing your own program from scratch
* [Option 2](#copy-someone-elses-program-to-run-on-your-module): Use someone else's program from the [contrib folder](/software/contrib/)
* [Option 3](#install-the-contrib-scripts-and-setup-the-menu): Install all of the contrib scripts and use the bootloader menu
* [Option 4](#calibrate-the-module): Calibrate the module for higher accuracy


### Write your own program from scratch

To program the module, just create a new Python file, and then press Ctrl-Shift-S to save as to the Raspberry Pi Pico, and name it 'main.py'.  
Do not save files to the 'lib' folder, as this is just for libraries to be imported rather than programs that you will write.  
Now import the entire europi library by simply adding the line 'from europi import *'

  ![From europi import](https://i.imgur.com/UK3nJcV.jpg)

Now you have access to the inputs and outputs using easy methods, which you can read about more in the [README.md](/software/README.md) of the software folder.


### Copy someone else's program to run on your module

1. Use the exact same process as for the ssd1306 and europi libraries to install the europi-contrib library:
   1. In Thonny, click Tools -> Manage Packages to open the package manager.
   2. Type 'europi' into the search box and click 'Search on PyPi'
   3. Click the result named 'micropython-europi-contrib'.
   4. Click 'Install'.
2. You will now see the new directory 'contrib' inside the 'lib' folder, containing the contrib scripts. 
3. You can now choose any script from inside this contrib folder to run on your module. When you've chosen, double click the file on the Pico to open it.
4. Press 'Ctrl-Shift-S' to Save As, and choose 'Raspberry Pi Pico'
  
  ![image](https://user-images.githubusercontent.com/79809962/151053911-7145ddb6-12e9-4606-909c-e1f888e3b4b9.png)  
5. Name the file ``main.py``, being careful to include the '.py' so the module knows it is a Python file. If you do not name it ``main.py``, the module will not know to automatically run your program whenever it is connected to power. Save the file to the root directory of the Pico (not inside any folders)  
  
  ![image](https://user-images.githubusercontent.com/79809962/151054018-0f495bb5-067e-4cd6-9640-c38e44a216de.png)  
6. Now you can disconnect the module from your computer, connect it to rack power, and the your chosen script will run automatically.
  
  
### Install the contrib scripts and setup the menu

1. Complete all of the steps for [Option 2](https://github.com/Allen-Synthesis/EuroPi/edit/release_prep/0.2.0/software/programming_instructions.md#copy-someone-elses-program-to-run-on-your-module), but you must use ``menu.py`` as the file to save to the root directory. Name it ``main.py`` as you would any other script.
2. Now you can disconnect the module from your computer, connect it to rack power, and the menu will open automatically. After you choose a program that will become the default program that runs when the module is connected to power, but you can still go back to the menu at any time by pressing and holding both buttons for >0.5s and then releasing.


### Calibrate the module

To use the module for accurately reading and outputting voltages, you need to complete a calibration process. This will allow your specific module to account for any differences in components, such as resistor tolerances.  
If you do not wish to calibrate the module and don't mind your voltages being slightly inaccurate, simply skip to the programming step and your module will use default values.

1. To begin, you need to choose the `calibrate.py` file and save it as `main.py` in the root directory, as we did in [Option 2](#copy-someone-elses-program-to-run-on-your-module) above. You can obtain the `calibrate.py` file from either the `lib` directory on your Pico, or from [the firmware directory in the repository](/software/firmware/calibrate.py).
2. Make sure your module is connected to rack power for the calibration process. It doesn't matter if it connected to USB as well, however if it is it will give an extra warning to turn on rack power which you need to skip using button 1.
3. Turn on the rack power supply, and the screen will display 'Calibration Mode'. If it doesn't, try [troubleshooting](../troubleshooting.md).  
4. There are 2 options for calibration:
  - Low Accuracy: Only a single 10V supply is required
  - High Accuracy: A variable supply is required to produce voltages from 0-10V  
  Press button 1 to choose Low Accuracy mode, or button 2 to choose High Accuracy mode.
5. Connect your voltage source to the analogue input, and input each voltage displayed on the screen. To take a reading (once your voltage is connected), press button 1.
6. Once all the required voltages have been input, you now need to disconnect the analogue input from your voltage source, and instead connect it to CV output 1.
7. Once you have connected the analogue input to CV output 1, press button 1
8. Wait for each voltage up to 10V to complete. The module will tell you once it has completed.
9. The calibration process is now complete! You now need to rename or delete the 'calibrate.py' program, however DO NOT delete the new file created called 'calibration_values.py'. This file is where the calibration values are stored, and if you delete it you will have to complete the calibration again.


# Programming Limitations

As with all hardware, the EuroPi has certain limitations. Some are more obvious and are required knowledge for any user, and some are more in depth and are only relevant if you will be programming the module yourself.

### Obvious Limitations
- Analogue input is only 0-10V
- Digital input can only detect signals above 0.7V (meaning it may trigger accidentally if you have a noisy 'low' state)
- Outputs, analogue input, and knobs, have a maximum resolution of 12 bits (4096 steps)
- Debouncing of the buttons means that very fast double presses may not be detected

### In Depth Limitations
- Clock pulses shorter than approximately 0.01s (10ms) will not be reliably detected (this depends on clock speed too)
- Reading any analogue source, either the analogue input or knobs, will result in a slight delay of the script (this can be reduced by using fewer samples, at the cost of accuracy)

