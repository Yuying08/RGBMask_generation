a)
Description:
This project involves combining three types of vector data (road bounds, road markings, and buildings) into a single raster RGB mask. Each feature is assigned a unique RGB value. The process also includes handling potential issues related to pixel value overlaps that can confuse machine learning models.

Python libraries:
numpy
rasterio
shapely
pyproj
osgeo

Usage
Prepare the environment:
Ensure that your environment has access to the required PROJ data files. Set the PROJ_LIB environment variable if needed.

Run the script:
The main script processes vector data and generates an RGB raster mask. Execute the script in your Jupyter notebook or Python environment.

Example code:
Replace the commented sections with your actual data and actual path:

Outputs
RGB Mask File: The output of the script is an RGB mask saved as a GeoTIFF file named output_mask.tif



b）When dealing with raster masks in a machine learning (ML) pipeline, particularly for tasks like semantic segmentation, issues often arise due to:
	Similar pixel values
The model may be confused to differentiate the feature with similar values, leading to the process broke down before the training could commence.
	Pixel value overlap: Pixel value overlap: values assigned to each feature intersect across different classes, leading to confusion for the model.
Road markings might be the likely culprits. 
	broken line: [0, 20, 10]
	cycle lane: [0, 40, 0]
	dashed line: [0, 45, 70]
	pedestrian crossing: [0, 100, 0]
	solid line: [0, 45, 0]
	stop line: [0, 85, 0]
As we can see, the pixel values among these classes are very close. Especially, the pixel values for "Cycle lane" and "Solid line" are very close ([0, 40, 0] and [0, 45, 0]). This can lead to confusion during training, as the model may struggle to distinguish between these two features effectively.

What we can do:
Assign distinct pixel values to classes that are not similar. For example, represent the cycle lane with [0, 40, 0] and the solid line with [0, 155, 0]. 
