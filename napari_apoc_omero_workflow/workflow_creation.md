# Creating a Segmentation Workflow with napari-apoc and OMERO

## Logging into OMERO

Log in to the OMERO server using the OMERO Insight application. If you haven't installed it yet, please refer to the first page of this book.
Once you are logged in, you should see the following interface:

![](apoc_omero_2.png)

Click on "Display Groups" and check the "RegBioMed" group and "All Members" to get access to the images you will be using during the course. On the left pane, you should be able to expand the "RegBioMed" group and see the Project "Segmentation with ML" and 2 Datasets.

![](apoc_omero_3.png)

## Loading images from OMERO with napari-omero

### Activate the course environment

Open a terminal (preferably Miniforge Prompt, but not necessarily) and run the following command to activate the course environment:

```bash
mamba activate amhct
```

And start napari:

```bash
napari
```

```{image} ./apoc_omero_4.png
:alt: napari
:width: 300px
:align: center
```

### Loading images from OMERO

In the napari window, go to the menu bar and select `Plugins > napari-omero > OMERO Browser`.

```{image} ./apoc_omero_5.png
:alt: OMERO Browser
:width: 400px
:align: center
```

This will open the OMERO Browser panel on the right side of the napari window. Enter your ZIH credentials and the server address `omero-int.biotec.tu-dresden.de` in the OMERO Browser panel. Click on "Connect".

```{image} ./apoc_omero_6.png
:alt: OMERO Browser
:width: 400px
:align: center
```

Once you are connected, change the "Group" to "RegBioMed" and set the "User" to "Marcelo Leomil Zoccoler" or "All". This will give you access to the images you will be using during the course. You should see the Project "Segmentation with ML".

```{image} ./apoc_omero_7.png	
:alt: OMERO Browser
:width: 300px
:align: center
```

Expand the Project tree and the "Exercise_DataSet" tree. Click on the image to load it to the napari canvas.

![](apoc_omero_8.png)

You can close the OMERO Browser panel by clicking on the "X" button on the top left corner of the panel. 

```{image} ./apoc_omero_9.png
:alt: OMERO Browser
:width: 300px
:align: center
```

### Handling the Image Dimensions

OMERO always stores images as 5D arrays (X, Y, Z, C, T). Therefore, even if you load a single-channel 2D image, it will be loaded as a 5D array with the dimensions (1, 1, 1, Y, X). But since napari splits channels into different layers, you actually end up with dimensions (1, 1, Y, X) for the image.
You can check the dimensions of the image by clicking on `Tools > Utilities > Layer Details` in the menu bar. This will open a panel with information about the selected layer.

```{image} ./apoc_omero_10.png
:alt: Layer Details
:width: 450px
:align: center
```

```{image} ./apoc_omero_11.png
:alt: Layer Details
:width: 300px
:align: center
```

We can and should remove the first two dimensions (1, 1) from the image. To do this, go to `Tools > Transforms > Remove axes of length 1` in the menu bar.

```{image} ./apoc_omero_12.png
:alt: Remove axes of length 1
:width: 500px
:align: center
```

This will open a small widget where you can select the layer to remove the axes from. Select the image layer and click on "Run".

```{image} ./apoc_omero_13.png
:alt: Remove axes of length 1
:width: 300px
:align: center
```

Check the dimensions of the image again by clicking on `Tools > Utilities > Layer Details` in the menu bar. You should see that the dimensions of the image are now (Y, X).

```{image} ./apoc_omero_14.png
:alt: Layer Details
:width: 300px
:align: center
```

Please delete the original image layer to avoid creating layer with these unit dimensions. To do this, select the image layer and click on the trash can icon on the top right corner of the layer list.

```{image} ./apoc_omero_15.png
:alt: Delete layer
:width: 400px
:align: center
```

## Object Segmentation with napari-apoc

Use the Object Segmentation from the napari-apoc plugin to segment the image. You should open the Object Segmentation widget via `Tools > Segmentation/labeling > Object Segmentation (APOC)`.

 Check more details on how to do this again in the [Interactive pixel classification and object segmentation in Napari](https://biapol.github.io/AMHCT_Bio_Image_Analysis_2025/interactive_pixel_classification/readme.html) section. 

![](apoc_omero_16.png)

## Saving Model and Predictions to OMERO

### Saving Layers

To save napari layers locally, select the layer you want to save, then go to `File > Save Selected Layers...`.

```{image} ./apoc_omero_17.png
:alt: Save layers
:width: 300px
:align: center
```

### Uploading Images to OMERO

The napari-omero plugin has a fuctionality to upload segmetation results as OMERO ROIs. We will not use this functionality in this course, mainly because the download of ROIs is not available yet, but you can check the plugin documentation for more details.

Instead we will upload the segmentation results as new images. In OMERO Insight, open the Importer by clicking on the Importer icon in the top left corner of the window.

```{image} ./apoc_omero_18.png
:alt: Upload to OMERO
:width: 300px
:align: center
```

In the Importer window, navigate to the folder where you saved the layers. Select the image files you want to upload and click on the `>` button to prepare them for upload.

![](apoc_omero_19.png)

This will pop-up a window where you can select the project and the dataset to upload the images to. Select the "Exercise_DataSet" dataset and click on "Add to the Queue".

```{image} ./apoc_omero_20.png
:alt: Upload to OMERO
:width: 400px
:align: center
```

This will add the images to the upload queue (right panel). You can add more images to the queue by repeating the previous step. 

![](apoc_omero_21.png)

Once you have added all the images you want to upload, click on the "Import" button in the bottom right corner of the Importer window.

Go back to the OMERO Insight main window and click on the refresh button in the top left corner of the window. You should see the images you just uploaded in the "Exercise_DataSet" dataset.

![](apoc_omero_22.png)

### Annotating Images in OMERO

After selecting an image, you can annotate it with key-value pairs to, for example, indicate the image ID containing the predictions. Below, in the original image, we defined the key "Predictions" and the value "38547", which is the image ID of the predictions we just uploaded.

```{image} ./apoc_omero_23.png
:alt: Annotate images in OMERO
:width: 400px
:align: center
```

We can also add tags to the image. Tags are useful to group images with similar characteristics so that they can be easily filtered later. For example, we can add the tag "Predictions" to the segmentation image to indicate that it contains predictions. Once we click on the `+` button, we can choose the tag we want to add to the image and click on the `>` button to add it.

![](apoc_omero_24.png) | ![](apoc_omero_25.png)
--- | ---

We can filter the images by tags by clicking on "filter images" dropdown box at the top of the OMERO Insight window. This will open a panel where you can select the properties you want to filter by. Select the "Tags" property and write the tag you want to filter by (e.g. "Predictions"). Only images with this tag will be displayed in the OMERO Insight window.

```{image} ./apoc_omero_26.png
:alt: Annotate images in OMERO
:width: 500px
:align: center
```

### Saving the Model to OMERO

If we want to save the model we trained in napari-apoc to OMERO, we can do this by uploading the `ObjectSegmenter.cl` file as an attachement to the image. To do this, select the image you want to upload the model to and click on the "Attachments" tab in the right panel. Click on the `+` button to add a new attachment. This will open a file browser where you can select the `ObjectSegmenter.cl` file. Select the file and click on "Open". The file will be uploaded as an attachment to the image.

```{image} ./apoc_omero_26b.png
:alt: Upload to OMERO
:width: 400px
:align: center
```

## Conclusion

This page showed you how to create a segmentation workflow with napari-apoc from images loaded from OMERO and how to store the model and predictions back to OMERO.

## Exercise

Take notes of which information is necessary to make your workflow reproducible adn where you can find it. Share a brief summary of your workflow with a colleague, who will try to reproduce it.

In the next section, we show you one possible way to reproduce the workflow we just created.