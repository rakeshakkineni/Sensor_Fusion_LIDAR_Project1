# Sensor_Fusion_LIDAR_Project1
This project implements pipeline for converting the raw LIDAR sensor measurements into trackable object. It implements filtering, segmentation, clustering, boundbox routines. Filtering was performed using the PCL functions. Functions were implemented for segmentation and clustering. Following are the pipeline details. 

## PipeLine
- Read a PCD file.
- Filter the raw LIDAR data 
- Segment the filtered data to identify road and objects
- Clustering , from objects identify the clusters.
- For each cluster append a bounding box. 
- Rendering. Render the objects and road to the viewer. 

Following are the details for a few of the above steps. 

## Filtering
The raw LIDAR data is filtered , this helps in increasing the processing speed and false targets. Following list of operations were performed. 
 - Downsampling: points are converted to voxels to a given dimension. PCL function VoxelGrid was used for this operation.
 - Crop: Remove all the points that are outside the limits. PCL function CropBox was used for this operation. Limits were found by visually inspecting the scene. 
 - RoofCrop: Remove roof points , dimensions of roof are identified by visually inspecting the scene.PCL function CropBox was used for this operation.
 
## Segmentation
Filtered output is segmented. Segmentation divides the scene into plane and objects. Plane refers the road surface. This step helps in differetiating the drivable area from obstacles. RANSAC algorithm was used. Following steps were performed to realise thie function.
  - Randomly choose 3 points from the cloud, fit a plane using these points.
  - Loop through all the points in the cloud, for each of the point calculate
    - The distance to the plane created above. If the distance is below distanceTol then add the index to a temporary set
    - Store the temporary vector if the size is more than previously identified indices.
  - Repeat above steps for maxIterations
 maxIterations value was obtained by doing a couple of trails with different values, value that gives best result was choosen. 
 
 ## Clustering
 Clustering helps in identifying different objects in the scene. Euclidean Clustering mechanism was implemented. Euclidean Clustering uses KDTree , all the points in the cloud are used to form a KDTree of 3-Dimensions.Following steps are performed for realizing Euclidean clustering mechanism. 
 
   
    
 
 
