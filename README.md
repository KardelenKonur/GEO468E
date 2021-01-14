![itulogo](itulogo.jpeg)
# SPECIAL TOPICS IN REMOTE SENSING
## *Changes of Akşehir Lake Water Extent in 1997 and 2013*

In this study, the changes in the water surface area of Akşehir Lake in 1997 and 2013  were analyzed and interpreted with remote sensing data. For this, images of two years were obtained from Landsat 5 TM and Landsat 8 OLI / TIRS satellites. NDWI were used to monitor the changes in water areas during the analysis phase. NDWI was applied and the images dated 1997 and 2013 were subtracted from each other and the changes between the years were tried to be monitored.

```Python
#plot band 3 2013
plot.show(band3_2013)
#plot band 5 2013
plot.show(band5_2013)
#plot band 2 1997
plot.show(band2_1997)
#plot band 4 1997
plot.show(band4_1997)
- fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(12, 6))
plot.show(band3_2013, ax=ax1, cmap='Greys') #green
plot.show(band5_2013, ax=ax2, cmap='Greys') #nir
fig.tight_layout()

- fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(12, 6))
plot.show(band2_1997, ax=ax1, cmap='Greys') #green
plot.show(band4_1997, ax=ax2, cmap='Greys') #nir
fig.tight_layout()
- green2013 = band3_2013.read(1).astype("float64")
nir2013 = band5_2013.read(1).astype("float64")
green1997 = band2_1997.read(1).astype("float64")
nir1997= band4_1997.read(1).astype("float64")
- ndwi2013 = np.where(
    (green2013+nir2013)==0., 
    0, 
    (green2013-nir2013)/(green2013+nir2013))
ndwi2013[:10,:10]

- ndwi1997 = np.where(
    (green1997+nir1997)==0., 
    0, 
    (green1997-nir1997)/(green1997+nir1997))
ndwi1997[:10,:10]
- ndwiImage2013 = rasterio.open("C:/Users/w10/Desktop/geo468E/water/ndwiImage2013.tiff","w",driver="Gtiff",
                          width=band3_2013.width, 
                          height = band3_2013.height, 
                          count = 1, crs=band3_2013.crs, 
                          transform=band3_2013.transform, 
                          dtype="float64")
ndwiImage2013.write(ndwi2013,1)
ndwiImage2013.close()

ndwi2013 = rasterio.open("C:/Users/w10/Desktop/geo468E/water/ndwiImage.tiff")
fig = plt.figure(figsize=(18,12))
plot.show(ndwi2013)
- ndwiImage1997 = rasterio.open("C:/Users/w10/Desktop/geo468E/water/ndwiImage1997.tiff","w",driver="Gtiff",
                          width=band2_1997.width, 
                          height = band2_1997.height, 
                          count = 1, crs=band2_1997.crs, 
                          transform=band2_1997.transform, 
                          dtype="float64")
ndwiImage1997.write(ndwi1997,1)
ndwiImage1997.close()

ndwi1997 = rasterio.open("C:/Users/w10/Desktop/geo468E/water/ndwiImage1997.tiff")
fig = plt.figure(figsize=(18,12))
plot.show(ndwi1997)
- def image_histogram(ndwi2013):
    from rasterio.plot import show_hist

    co, ce =show_hist(ndwi2013)
    fig = plt.figure(figsize=(10,7))
    fig.set_facecolor('white')
    plt.plot(ce[1::], co[1::])
    plt.show()
- %matplotlib inline
image_histogram(ndwi2013)
- def image_histogram(ndwi1997):
    from rasterio.plot import show_hist

    co, ce =show_hist(ndwi1997)
    fig = plt.figure(figsize=(10,7))
    fig.set_facecolor('white')
    plt.plot(ce[1::], co[1::])
    plt.show()
- %matplotlib inline
image_histogram(ndwi1997)
- ndwi2013=np.where(
    (green2013+nir2013)==0., 
    0, 
    (green2013-nir2013)/(green2013+nir2013))
ndwi2013[1:1:1]

ndwi1997=np.where(
    (green1997+nir1997)==0., 
    0, 
    (green1997-nir1997)/(green1997+nir1997))
ndwi1997[1:1:1]

plot.show(ndwi2013[:1000,:1000])
plot.show(ndwi1997[:1000,:1000])

fig = plt.figure(figsize=(18,12))
ndwi_difference=(plot.show(ndwi1997[:1000,:1000]-ndwi2013[:1000,:1000]))
```
