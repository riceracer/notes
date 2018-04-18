## Apt / Fix bad packages

If 

    sudo apt-get install -f

is failing due to broken dependencies and I cannot uninstall the packages using those dependencies through apt, then use dpkg to remove them:

    sudo dpkg -r gdal proj

After that you may be able to then use the package manager and re-install dependencies:

    sudo apt-get update
    sudo apt-get install -f