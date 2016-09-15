# ROS Wrapper around DSO: Direct Sparse Odometry

For more information see
[https://vision.in.tum.de/dso](https://vision.in.tum.de/dso)

### Related Papers

* **Direct Sparse Odometry**, *J. Engel, V. Koltun, D. Cremers*, In arXiv:1607.02565, 2016

* **A Photometrically Calibrated Benchmark For Monocular Visual Odometry**, *J. Engel, V. Usenko, D. Cremers*, In arXiv:1607.02555, 2016


# 1. Installation

1. Install DSO. We need DSO to be compiled with OpenCV (to read the vignette image), and with Pangolin (for 3D visualization).
2. adjust three absolute paths in CMakeLists.txt to point to your DSO.
3. run 

		rosmake
	

# 3 Usage
everything as described in the DSO project - only this is for real-time camera input.


		rosrun dso_ros dso_live image:=image_raw \
			calib=XXXXX/camera.txt \
			gamma=XXXXX/pcalib.txt \
			vignette=XXXXX/vignette.png \

Feel free to take it as example to set up your own camera input.



# 4 Dependencies

## 4.1 Pangolin
removing

	    fullSystem->outputWrapper = new IOWrap::PangolinDSOViewer(
	    		 (int)undistorter->getSize()[0],
	    		 (int)undistorter->getSize()[1]);

will allow you to use DSO compiled without Pangolin. However, then there is no 3D visualization.
You can also implement your own Output3DWrapper.


## 4.2 OpenCV
you can use DSO compiled without OpenCV. 
In that case, the vignette image will not be read, and no photometric calibration can be used. Also, there will not be any image visualizations / image saving.
You can also implement your own version of ImageRW.h / ImageDisplay.h, instead of the dummies.


