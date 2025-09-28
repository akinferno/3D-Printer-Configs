First, follow instruction on ArmoredTurtle AFC-Klipper-Addon for installation...

https://github.com/ArmoredTurtle/AFC-Klipper-Add-On

**Installation**
To install this plugin, you should have the following pre-requisites installed:

--Klipper

--Moonraker

--WebUI (Mainsail or Fluidd)

--Both jq and crudini should be installed on your RaspPi (or equivalent). This can typically be accomplished with the following commands:
    
    sudo apt-get install jq crudini

-Python >= 3.8

To install this plugin, you can use the following commands from the users home directory:

    cd ~
    git clone https://github.com/ArmoredTurtle/AFC-Klipper-Add-On.git
    cd AFC-Klipper-Add-On
    ./install-afc.sh
    
Full options for the install-afc.sh script can be found by running the following command:

    ./install-afc.sh -h
    
**Updates**
To update the AFC plugin software, you can simply run the following command:

    cd AFC-Klipper-Add-On
    ./install-afc.sh

The update process should be non-destructive and will not overwrite any existing configuration files without your permission. If you run into an issue due to a specific configuration, you may need to comment out the AFC plugin software and re-run the install-afc.sh script.

This can be accomplished by commenting out the following lines in your printer.cfg file:

    [include AFC/*.cfg]
    
Once the plugin is updated, please uncomment the lines in your printer.cfg file (if applicable).

**Documentation**
Further documentation on the plugin, it's various commands and configuration references can be found here.
