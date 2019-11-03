# Mapping

Open source tools, tips and tricks for mapping lovers

## Cool Websites

- [QGIS 3](https://www.qgis.org/en/site/)
- [Arch Geo Tux](https://archgeotux.sourceforge.io/)

## Data Sources I use

- [Centro de descargas del IGM](http://centrodedescargas.cnig.es/CentroDescargas/)
- [Universidad de Extremadura](http://secad.unex.es/conocimiento/)
- [ICGC](https://www.icgc.cat/Descarregues)

## Adding support to ECW, JPEG2000 and MrSID file formats with GDAL in Arch Linux

- Uninstall GDAL if present

- Download the ERDAS ECW JP2 SDK v5.4 (or later) Linux
  - [Download the ERDAS ECW JP2 SDK v5.4 (or later) Linux](https://download.hexagongeospatial.com/downloads/ecw/erdas-ecw-jp2-sdk-v5-4-linux?result=true)
  - Unzip and run `./ERDAS_ECWJP2_SDK-5.4.0.bin`
  - At the menu, select 1 for "Desktop Read-Only Redistributable"
  - Accept the license agreement 
  - `sudo cp -r ~/hexagon/ERDAS-ECW_JPEG_2000_SDK-5.4.0/Desktop_Read-Only /usr/local/hexagon`
  - `sudo rm -r /usr/local/hexagon/lib/x64`
  - `sudo mv /usr/local/hexagon/lib/newabi/x64 /usr/local/hexagon/lib/x64`
  - `sudo cp /usr/local/hexagon/lib/x64/release/libNCSEcw* /usr/local/lib`
  - `sudo ldconfig /usr/local/hexagon`

- Download and install MrSID DSDK
  - Download [MrSID DSDK](https://www.extensis.com/support/developers) for linux 64 and GCC 5
  - Unzip and move the folder to home

- Build GDAL
  -  Download the source code [here](https://trac.osgeo.org/gdal/wiki/DownloadSource)
  -  Unzip and enter the folder
  -  Set your options `./configure CXXFLAGS=-D_GLIBCXX_USE_CXX11_ABI=0 --with-ecw=/usr/local/hexagon --with-mrsid=~/MrSID_DSDK-9.5.4.4709-rhel6.x86-64.gcc531/Raster_DSDK --with-mrsid_lidar=~/MrSID_DSDK-9.5.4.4709-rhel6.x86-64.gcc531/Lidar_DSDK --without-libtool`
  -  Remove old builds `make clean`
  -  Compile with all cores `make -j8`
  -  Install `sudo make install`

 Check the format is now supported:

`gdalinfo --formats | grep -i ecw mrsid`

## Arch Geo Tux repository

There is an [Arch Geo Tux](https://archgeotux.sourceforge.io/) repository with some useful packages. Add this repository to `/etc/pacman.conf`

```bash
[archgeotux]
SigLevel = Optional TrustAll
Server = https://downloads.sourceforge.net/project/archgeotux/$arch
```

Add the database file for this new repo `sudo pacman -Sy`

## 3D Printing topography maps with QGIS3

You need a digital elevation model (DEM) of the area you want to cover.

