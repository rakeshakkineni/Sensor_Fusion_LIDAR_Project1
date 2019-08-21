# Sensor_Fusion_LIDAR_Project1
This project implements pipeline for converting the raw LIDAR sensor measurements into trackable objects. It implements filtering, segmentation, clustering, boundbox routines. Filtering was performed using the PCL functions. Functions were implemented for segmentation and clustering. Following are the pipeline details. 

## PipeLine 
Following are the steps for the pipeline
- Read a PCD file.
- Filter the raw LIDAR data 
- Segment the filtered data to identify road and objects
- Clustering: from objects identify the clusters.
- For each cluster append a bounding box. 
- Rendering:Render the objects and road to the viewer. 

Following are the details for a few of the above steps. 

## Filtering
The raw LIDAR data is filtered , this helps in increasing the processing speed and reduce false targets. Following list of operations were performed. 
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
 Clustering helps in identifying different objects in the scene. Euclidean Clustering mechanism was implemented. Euclidean Clustering uses KDTree , all the points in the cloud are used to form a 3-Dimensional KDTree. After forming KDTree a point is taken from the cloud and all the points that are within a distance to this point are identified, each of the identified points is used and its adjacent points that are with in a distance are identified this process is repeated untill there are no points that satisfy the distance criteria are left,all the identified points form a cluster, after that a new point that is not processed is picked and the process is left. All the clusters with number of points with in (minSize, maxSize) are retained rest are discarded. Each of these clusters form a distinct object. 

## Bounding Box 
 For each of the cluster a bounding box is fitted. To fit a box min and max coordinates of a cluster are used. Using renderbox function boxes are drawn. 
 
## Output
 Screen shots of output in different views are placed in Output folder.
   
    
 
 
