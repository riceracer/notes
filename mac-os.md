# Improve terminal prompt

    vi ~/.bash_profile

    # in file:
    export PS1="\[\033[36m\]\u\[\033[m\]@\[\033[32m\]\h:\[\033[33;1m\]\w\[\033[m\] \$ "
    export CLICOLOR=1

# JAVA_HOME

in .bash_profile:

    export JAVA_HOME=$(/usr/libexec/java_home)

# Instal Gdal 2.x

From: https://www.karambelkar.info/2016/10/gdal-2-on-mac-with-homebrew/

Unlink gdal 1.x

    brew unlink gdal

Tap into osgeo4mac

    brew tap osgeo/osgeo4mac && brew tap --repair

Install gdal 2.x

    brew install jasper netcdf # gdal dependencies
    brew install gdal2 --with-armadillo --with-complete --with-libkml --with-unsupported

Link gdal 2.x

    brew link --force gdal2

Verify

    gdal-config --version
    #2.1.1
    gdal-config --libs
    #-L/usr/local/Cellar/gdal2/2.1.1/lib -lgdal
    gdal-config --cflags
    #-I/usr/local/Cellar/gdal2/2.1.1/include
