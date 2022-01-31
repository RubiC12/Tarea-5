TAREA 5
================
Rubi
30/1/2022

##NIVEL 1:

``` r
library(climatol)
```

    ## Warning: package 'climatol' was built under R version 4.1.2

    ## Loading required package: maps

    ## Warning: package 'maps' was built under R version 4.1.2

    ## Loading required package: mapdata

    ## Warning: package 'mapdata' was built under R version 4.1.2

``` r
setwd("C:/Users/Rubi/OneDrive/Documentos/PROGRA CLIMATOL")
```

1.  Generar un diagrama de Walter y Lieth con la data de datcli, este
    debe llevar de título “Estación Campo de Marte”, a una altitud de 80
    msnm durante el año 2017, con los meses simbolizados por números.
    Las temperaturas deberán visualizarse de color verde; las
    precipitaciones, en naranja; los meses de congelación segura, en
    azul y los de congelación probable, en celeste. No trazar una línea
    suplementaria de precipitación.

``` r
data(datcli)
diagwl(datcli, "Estación Campo de Marte",alt=80,per="2017",mlab="otro",pcol="orange",tcol="green",pfcol="light blue",sfcol="blue")
```

![](TAREA-5-PROGRAMACIÓN_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

2)Recrea minuciosamente el siguiente diagrama de la rosa de los vientos
(pista: col=rainbow(8)).

``` r
data(windfr)
rosavent(windfr,fnum =6,fint=2,flab=1,ang=3*pi/8,col=rainbow(8),margen=c(0,0,0,0),uni="km/s")
```

![](TAREA-5-PROGRAMACIÓN_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

##NIVEL 2:

3)Convertir la data diaria de tmax en una data de medias mensuales.
Posteriormente, homogeneizar dichos datos mensuales con una
normalización por estandarización y gráficos de medias anuales y
correcciones aplicadas en el análisis exploratorio de datos (utilizar
dos decimales).

``` r
data(tmax)
#Exportamos archivos del database de R a nuestro equipo:
write.table(dat,"tmax_2001-2003.dat", row.names=F, col.names=F)
write.table(est.c, "tmax_2001-2003.est", row.names=F, col.names=F)

#Convertimos el database (.dat) diario a mensual:
dd2m("tmax",2001,2003,ndec=2,valm=2)
```

    ##   1  2  3
    ## 
    ## Monthly mean values saved to file tmax-m_2001-2003.dat 
    ##   (Months with more than 10 missing original daily data
    ##   have also been set to missing)

``` r
tmax_m<-read.table("tmax-m_2001-2003.dat",header=FALSE)

homogen("tmax",2001,2003,std=3,ndec=2,gp=3,expl=TRUE)
```

    ## 
    ## HOMOGEN() APPLICATION OUTPUT  (From R's contributed package 'climatol' 3.1.1)
    ## 
    ## =========== Homogenization of tmax, 2001-2003. (Sun Jan 30 22:57:15 2022)
    ## 
    ## Parameters: varcli=tmax anyi=2001 anyf=2003 suf=NA nm=NA nref=10,10,4 std=3 swa=NA ndec=2 dz.max=5 dz.min=-5 wd=0,0,100 snht1=0 snht2=0 tol=0.02 maxdif=0.005 mxdif=0.005 maxite=999 force=FALSE wz=0.001 trf=0 mndat=NA gp=3 ini=NA na.strings=NA vmin=NA vmax=NA nclust=100 cutlev=NA grdcol=#666666 mapcol=#666666 hires=TRUE expl=TRUE metad=FALSE sufbrk=m tinc=NA tz=UTC cex=1.2 verb=TRUE
    ## 
    ## Data matrix: 1095 data x 3 stations

    ## Computing inter-station distances:  1  2
    ## 
    ## 
    ## ========== STAGE 3 (Final computation of all missing data) ==========
    ## 
    ## Computing inter-station weights... (done)

    ## Computation of missing data with outlier removal
    ## (Suggested data replacements are provisional)
    ## 
    ## The following lines will have one of these formats:
    ##   Station(rank) Date: Observed -> Suggested (Anomaly, in std. devs.)
    ##   Iteration Max.data.difference (Station_code)
    ## 2 -0.1884 (S01)
    ## 3 -0.0407 (S01)
    ## 4 -0.0088 (S01)
    ## 5 -0.0019 (S01)
    ## 
    ## Last series readjustment (please, be patient...)

    ## 
    ## ======== End of the missing data filling process, after 0.85 secs 
    ## 
    ## ----------- Final computations:
    ## 
    ## ACmx: Station maximum absolute autocorrelations of anomalies
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##  0.4900  0.5050  0.5200  0.5167  0.5300  0.5400 
    ## 
    ## SNHT: Standard normal homogeneity test (on anomaly series)
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##   16.30   26.95   37.60   42.57   55.70   73.80 
    ## 
    ## RMSE: Root mean squared error of the estimated data
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##   3.544   3.642   3.739   3.699   3.776   3.814 
    ## 
    ## POD: Percentage of original data
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##   81.00   84.50   88.00   87.33   90.50   93.00 
    ## 
    ##   ACmx SNHT RMSE POD Code Name     
    ## 1 0.54 73.8 3.5  81  S01  La Vall  
    ## 2 0.52 37.6 3.7  88  S02  Lucent   
    ## 3 0.49 16.3 3.8  93  S03  Sunflower

    ## 
    ## ----------- Generated output files: -------------------------
    ## 
    ## tmax_2001-2003.txt :  This text output 
    ## tmax_2001-2003_out.csv :  List of corrected outliers 
    ## tmax_2001-2003_brk.csv :  List of corrected breaks 
    ## tmax_2001-2003.pdf :  Diagnostic graphics 
    ## tmax_2001-2003.rda :  Homogenization results. Postprocess with (examples):
    ##    dahstat('tmax',2001,2003) #get averages in file tmax_2001-2003-me.csv 
    ##    dahstat('tmax',2001,2003,stat='tnd') #get OLS trends and their p-values 
    ##    dahgrid('tmax',2001,2003,grid=YOURGRID) #get homogenized grids 
    ##    ... (See other options in the package documentation)

4)Recortar la data mensual de Ptest desde 1965 hasta 2005. Homogeneizar
dicha data mediante clústers o áreas rectangulares, con un ancho de
superposición de 0, mediante una estandarización y con gráficos de
totales anuales en el análisis exploratorio de datos. Mostrar las medias
de las series homogeneizadas en un archivo Excel que, además, mencione
los totales anuales y los datos de la latitud, longitud y nombre de cada
estación (utilizar dos decimales).

``` r
data(Ptest)
#Exportamos archivos del database de R a nuestro equipo:
write.table(dat,"Ptest_1951-2010.dat",row.names=F,col.names=F)
write.table(est.c,"Ptest_1951-2010.est",row.names=F,col.names=F)

#Recortamos el database (.dat) de 1951-2010 a 1965-2005:
datsubset("Ptest", 1951, 2010, 1965, 2005, 1)
```

    ## Subset data written to files Ptest_1965-2005.dat and Ptest_1965-2005.est

``` r
dim(dat)<-c(720,20)
write(dat[481:720,1:20],"Ptest_1951-2010.dat")
write.table(est.c[1:20,1:5],"Ptest_1951-2010.est",row.names=FALSE,col.names=FALSE)
homogsplit("Ptest",1951,2010,2.9,39.6,0,0,std=3,ndec=2,gp=4,expl=TRUE)
```

    ## 
    ## HOMOGSPLIT() APPLICATION OUTPUT  (From R's contributed package 'climatol' 3.1.1)
    ## 
    ## =========== Homogenization of Ptest, 1951-2010. (Sun Jan 30 22:57:17 2022)
    ## 
    ## Parameters: varcli=Ptest anyi=1951 anyf=2010 xc=2.9 yc=39.6 xo=0 yo=0 maponly=FALSE suf=NA nm=4 nref=10,10,4 swa=NA std=3 ndec=2 dz.max=5 dz.min=-5 wd=0,0,100 snht1=25 snht2=25 tol=0.02 maxdif=NA mxdif=NA force=FALSE wz=0.001 trf=0 mndat=NA gp=4 ini=NA na.strings=NA maxite=999 vmin=NA vmax=NA nclust=100 grdcol=#666666 mapcol=#666666 hires=TRUE expl=TRUE metad=FALSE sufbrk=m tinc=NA tz=UTC cex=1.2 verb=TRUE x=NA
    ## 
    ## 
    ## ==================================================
    ## 
    ##               AREA  1 1 
    ## 
    ## ==================================================
    ## 
    ## Only 3 stations in this area:
    ## They will be included in the next selection.
    ## 
    ## ==================================================
    ## 
    ##               AREA  1 2 
    ## 
    ## ==================================================
    ## 
    ## 
    ## HOMOGEN() APPLICATION OUTPUT  (From R's contributed package 'climatol' 3.1.1)
    ## 
    ## =========== Homogenization of Ptest-1, 1951-2010. (Sun Jan 30 22:57:17 2022)
    ## 
    ## Parameters: varcli=Ptest-1 anyi=1951 anyf=2010 suf=NA nm=4 nref=10,10,4 std=3 swa=NA ndec=2 dz.max=5 dz.min=-5 wd=0,0,100 snht1=0 snht2=0 tol=0.02 maxdif=0.005 mxdif=0.005 maxite=999 force=FALSE wz=0.001 trf=0 mndat=NA gp=4 ini=NA na.strings=NA vmin=NA vmax=NA nclust=100 cutlev=NA grdcol=#666666 mapcol=#666666 hires=TRUE expl=TRUE metad=FALSE sufbrk=m tinc=NA tz=UTC cex=1.2 verb=TRUE
    ## 
    ## Data matrix: 240 data x 10 stations

    ## 
    ## NA's in similarity matrix: NO CLUSTER ANALYSIS

    ## Computing inter-station distances:  1  2  3  4  5  6  7  8  9
    ## 
    ## 
    ## ========== STAGE 3 (Final computation of all missing data) ==========
    ## 
    ## Computing inter-station weights... (done)

    ## There are stations with less than 5 data:
    ## Stations :    9   10 
    ## N of data:    0    0 
    ## These stations will be deleted in order to proceed:
    ## S015(9) Station_015  DELETED
    ## S100(10) Station_100  DELETED
    ## 
    ## Computation of missing data with outlier removal
    ## (Suggested data replacements are provisional)
    ## 
    ## The following lines will have one of these formats:
    ##   Station(rank) Date: Observed -> Suggested (Anomaly, in std. devs.)
    ##   Iteration Max.data.difference (Station_code)
    ## 2 -27.651 (S095)
    ## 3 -16.9618 (S095)
    ## 4 -10.0682 (S095)
    ## 5 -5.8966 (S095)
    ## 6 -3.4349 (S095)
    ## 7 -2.0008 (S095)
    ## 8 -1.1699 (S095)
    ## 9 -0.6887 (S095)
    ## 10 -0.4091 (S095)
    ## 11 -0.2457 (S095)
    ## 12 -0.1494 (S095)
    ## 13 -0.0921 (S095)
    ## 14 -0.0577 (S095)
    ## 15 -0.0366 (S095)
    ## 16 -0.0236 (S095)
    ## 17 -0.0155 (S095)
    ## 18 -0.0103 (S095)
    ## 19 -0.0069 (S095)
    ## 20 -0.0047 (S095)
    ## 
    ## Last series readjustment (please, be patient...)

    ## 
    ## ======== End of the missing data filling process, after 2.33 secs 
    ## 
    ## ----------- Final computations:
    ## 
    ## ACmx: Station maximum absolute autocorrelations of anomalies
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
    ##  0.1400  0.2150  0.2450  0.2975  0.4025  0.5000       2 
    ## 
    ## SNHT: Standard normal homogeneity test (on anomaly series)
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
    ##   1.300   2.450   3.300   4.925   5.475  13.400       2 
    ## 
    ## RMSE: Root mean squared error of the estimated data
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
    ##   24.32   28.29   32.45   34.19   37.81   49.90       2 
    ## 
    ## POD: Percentage of original data
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##    0.00   31.50   66.50   58.40   95.25   98.00 
    ## 
    ##    ACmx SNHT RMSE POD Code Name       
    ## 1  0.39  2.9 41.3 98  S031 Station_031
    ## 2  0.24  1.4 28.1 28  S095 Station_095
    ## 3  0.14  9.9 28.4 98  S039 Station_039
    ## 4  0.20 13.4 32.2 98  S034 Station_034
    ## 5  0.50  3.7 36.6 42  S088 Station_088
    ## 6  0.25  1.3 32.7 87  S055 Station_055
    ## 7  0.44  4.0 24.3 52  S075 Station_075
    ## 8  0.22  2.8 49.9 81  S038 Station_038
    ## 9    NA   NA   NA  0  S015 Station_015
    ## 10   NA   NA   NA  0  S100 Station_100

    ## 
    ## ----------- Generated output files: -------------------------
    ## 
    ## Ptest-1_1951-2010.txt :  This text output 
    ## Ptest-1_1951-2010_out.csv :  List of corrected outliers 
    ## Ptest-1_1951-2010_brk.csv :  List of corrected breaks 
    ## Ptest-1_1951-2010.pdf :  Diagnostic graphics 
    ## Ptest-1_1951-2010.rda :  Homogenization results. Postprocess with (examples):
    ##    dahstat('Ptest-1',1951,2010) #get averages in file Ptest-1_1951-2010-me.csv 
    ##    dahstat('Ptest-1',1951,2010,stat='tnd') #get OLS trends and their p-values 
    ##    dahgrid('Ptest-1',1951,2010,grid=YOURGRID) #get homogenized grids 
    ##    ... (See other options in the package documentation)
    ## 
    ## 
    ## ==================================================
    ## 
    ##               AREA  2 1 
    ## 
    ## ==================================================
    ## 
    ## Only 1 stations in this area:
    ## They will be included in the next selection.
    ## 
    ## ==================================================
    ## 
    ##               AREA  2 2 
    ## 
    ## ==================================================
    ## 
    ## 
    ## HOMOGEN() APPLICATION OUTPUT  (From R's contributed package 'climatol' 3.1.1)
    ## 
    ## =========== Homogenization of Ptest-2, 1951-2010. (Sun Jan 30 22:57:19 2022)
    ## 
    ## Parameters: varcli=Ptest-2 anyi=1951 anyf=2010 suf=NA nm=4 nref=10,10,4 std=3 swa=NA ndec=2 dz.max=5 dz.min=-5 wd=0,0,100 snht1=0 snht2=0 tol=0.02 maxdif=0.005 mxdif=0.005 maxite=999 force=FALSE wz=0.001 trf=0 mndat=NA gp=4 ini=NA na.strings=NA vmin=NA vmax=NA nclust=100 cutlev=NA grdcol=#666666 mapcol=#666666 hires=TRUE expl=TRUE metad=FALSE sufbrk=m tinc=NA tz=UTC cex=1.2 verb=TRUE
    ## 
    ## Data matrix: 240 data x 10 stations

    ## 
    ## NA's in similarity matrix: NO CLUSTER ANALYSIS

    ## Computing inter-station distances:  1  2  3  4  5  6  7  8  9
    ## 
    ## 
    ## ========== STAGE 3 (Final computation of all missing data) ==========
    ## 
    ## Computing inter-station weights... (done)

    ## There are stations with less than 5 data:
    ## Stations :    7    8    9 
    ## N of data:    0    0    0 
    ## These stations will be deleted in order to proceed:
    ## S042(7) Station_042  DELETED
    ## S007(8) Station_007  DELETED
    ## S036(9) Station_036  DELETED
    ## 
    ## Computation of missing data with outlier removal
    ## (Suggested data replacements are provisional)
    ## 
    ## The following lines will have one of these formats:
    ##   Station(rank) Date: Observed -> Suggested (Anomaly, in std. devs.)
    ##   Iteration Max.data.difference (Station_code)
    ## 2 -18.9028 (S097)
    ## 3 -10.8485 (S097)
    ## 4 -6.2469 (S097)
    ## 5 -3.5884 (S097)
    ## 6 -2.0621 (S097)
    ## 7 -1.189 (S097)
    ## 8 -0.6893 (S097)
    ## 9 -0.4021 (S097)
    ## 10 -0.2363 (S097)
    ## 11 -0.1398 (S097)
    ## 12 -0.0834 (S097)
    ## 13 -0.05 (S097)
    ## 14 -0.0302 (S097)
    ## 15 -0.0184 (S097)
    ## 16 -0.0112 (S097)
    ## 17 -0.0069 (S097)
    ## 18 -0.0043 (S097)
    ## 
    ## Last series readjustment (please, be patient...)

    ## 
    ## ======== End of the missing data filling process, after 1.86 secs 
    ## 
    ## ----------- Final computations:
    ## 
    ## ACmx: Station maximum absolute autocorrelations of anomalies
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
    ##  0.1600  0.2350  0.2600  0.2614  0.2950  0.3500       3 
    ## 
    ## SNHT: Standard normal homogeneity test (on anomaly series)
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
    ##   1.300   2.500   3.100   2.857   3.400   3.800       3 
    ## 
    ## RMSE: Root mean squared error of the estimated data
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
    ##   28.48   33.04   33.24   43.91   35.80   98.85       4 
    ## 
    ## POD: Percentage of original data
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##    0.00    9.75   89.50   61.00   97.00   99.00 
    ## 
    ##    ACmx SNHT RMSE POD Code Name       
    ## 1  0.16 3.8  33.0 96  S047 Station_047
    ## 2  0.22 3.1  36.6 97  S098 Station_098
    ## 3  0.35 2.0  33.2 83  S051 Station_051
    ## 4  0.26 3.0  33.3 99  S081 Station_081
    ## 5  0.29 1.3  28.5 97  S069 Station_069
    ## 6  0.30 3.7  98.8 99  S058 Station_058
    ## 7    NA  NA    NA  0  S042 Station_042
    ## 8    NA  NA    NA  0  S007 Station_007
    ## 9    NA  NA    NA  0  S036 Station_036
    ## 10 0.25 3.1    NA 39  S097 Station_097

    ## 
    ## ----------- Generated output files: -------------------------
    ## 
    ## Ptest-2_1951-2010.txt :  This text output 
    ## Ptest-2_1951-2010_out.csv :  List of corrected outliers 
    ## Ptest-2_1951-2010_brk.csv :  List of corrected breaks 
    ## Ptest-2_1951-2010.pdf :  Diagnostic graphics 
    ## Ptest-2_1951-2010.rda :  Homogenization results. Postprocess with (examples):
    ##    dahstat('Ptest-2',1951,2010) #get averages in file Ptest-2_1951-2010-me.csv 
    ##    dahstat('Ptest-2',1951,2010,stat='tnd') #get OLS trends and their p-values 
    ##    dahgrid('Ptest-2',1951,2010,grid=YOURGRID) #get homogenized grids 
    ##    ... (See other options in the package documentation)
    ## 
    ## 
    ## ======== End of homogenization of overlapping areas, after 4.3 secs 
    ## 
    ## ----------- Generated output files: -------------------------
    ## 
    ## Ptest_1951-2010.txt :  This text output
    ## Ptest_1951-2010_out.csv :  List of corrected outliers
    ## Ptest_1951-2010_brk.csv :  List of corrected breaks
    ## Ptest-*_1951-2010.pdf :  Diagnostic graphics (one file per area)
    ## Ptest_1951-2010-map.pdf :  Map of specified areas
    ## Ptest_1951-2010.rda :  Homogenization results. Postprocess with (examples):
    ##    dahstat('Ptest',1951,2010) #get averages in file Ptest_1951-2010-me.csv
    ##    dahstat('Ptest',1951,2010,stat='tnd') #get OLS trends and their p-values
    ##    dahgrid('Ptest',1951,2010,grid=YOURGRID) #get homogenized grids
    ##    ... (See other options in the package documentation)
