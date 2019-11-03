# Mapping

Open source tools, tips and tricks for mapping lovers

## Cool Websites

- [QGIS 3](https://www.qgis.org/en/site/)
- [Arch Geo Tux](https://archgeotux.sourceforge.io/)

## Data Sources I use

- [Centro de descargas del IGM](http://centrodedescargas.cnig.es/CentroDescargas/)
- [Universidad de Extremadura](http://secad.unex.es/conocimiento/)
- [ICGC](https://www.icgc.cat/Descarregues)

## Opening ECW files with GDAL in Arch Linux

### Option A manual install

- Install the AUR `libecwj2` package
- Download and compile GDAL
  -  Download the source code [here](https://trac.osgeo.org/gdal/wiki/DownloadSource)
  -  Unzip and enter the folder
  -  Set your options `./configure --with-ecw`
  -  Compile with `make`
  -  Install `sudo make install`
  
 and check the format is now supported:

`gdalinfo --formats | grep -i ecw`

### Option B add archgeotux repository

There is an [Arch Geo Tux](https://archgeotux.sourceforge.io/) repository. Add this repository to `/etc/pacman.conf`

```bash
[archgeotux]
SigLevel = Optional TrustAll
Server = https://downloads.sourceforge.net/project/archgeotux/$arch
```

Add the database file for this new repo `sudo pacman -Sy`

~~and install with `pacman -S gdal-ecw`~~ package no longer available

## 3D Printing topography maps with QGIS3

You need a digital elevation model (DEM) of the area you want to cover.

