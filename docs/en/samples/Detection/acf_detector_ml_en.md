# Usage example of AcfDetector.m

## 1. Run Autoware
Run Autoware.  
![](../images/run_autoware.png)  

The Runtime Manager window is launched.  
![](../images/runtime_manager.png)  

## 2. Launch rviz
Launch the rviz by clicking the RViz button on the Runtime Manager.  
![](images/AcfDetector/click_rviz.png)  

## 3. Show imageViewerPlugin
When rviz starts, select ［Panels］-［Add New Panel］ from the menu.  
![](images/AcfDetector/add_new_pannel.png)  

Select "imageViewerPlugin".  
![](images/AcfDetector/select_image_viewer_plugin.png)  

Adjust the size of the imageViewerPlugin screen.  
For example, make the imageViewerPlugin screen float as follows.  
![](images/AcfDetector/move_image_viewer.png)  

Then adjust the screen size.  
![](images/AcfDetector/resize_image_viewer.png)  

## 4. Setting of rosbag file to play video
Open the Simulation tab of the Runtime Manager.  
Click the "Ref" button to set the rosbag file to play.  
![](images/set_rosbag.png)  

## 5. Connect MATLAB to Autoware (ROS Master)
Connect to the ROS master using the __rosinit__ command in MATLAB.  
Set the rosinit arguments according to your environment.  
```MATLAB
rosinit();
``` 

## 6. Start AcfDetector.m.
Add the folder containing the AcfDetector.m class file to MATLAB search path, 
create an instance of AcfDetector, and execute filtering.  
```MATLAB
acf_detector_folder = fullfile(autoware.getRootDirectory(), ...
                        'benchmark', 'computing', 'perception', 'detection', ...
                        'vision_detector', 'acf_detector');
addpath(acf_detector_folder);
acf_detector_obj = AcfDetector();
``` 

## 7. Play rosbag file
Open the Simulation tab of the Runtime Manager.  
Click the "Play" button to play rosbag.  
![](images/AcfDetector/play_simulation.png)

## 8. Topic setting of imageViewerPlugin  
1. Set the Image Topic of ImageViewerPlugin to "/image_raw".
1. Set Object Rect Topic of imageViewerPlugin to "/detection/vision_objects".
1. When a person is detected, the Boundary Box is displayed.    
![](images/AcfDetector/detect_people.png)  

The above figure uses the sample data provided in
[this book](http://www.ric.co.jp/book/contents/book_1187.html).  

Click
[here](images/AcfDetector/rosgraph_acf_detector_ml.png) to check the node graph when this 
example is executed.  
The node generated by AcfDetector.m is **/acf_detector_ml**.

## 9. Clean up
Execute the following command to finish.  
```MATLAB
acf_detector_obj.delete();
rosshutdown();
rmpath(acf_detector_folder);
clear acf_detector_obj acf_detector_folder;
```