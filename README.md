# LabVIEW Samples

This documentation provides descriptions of the other LabVIEW VI samples and instructions on using the **Demo** VI sample to control a Mech-Eye Industrial 3D Camera.

## Sample List

The following VI samples are provided. These VI samples use C# Mech-Eye API to realize the corresponding functions. [Mech-Eye API Reference](https://docs.mech-mind.net/api-reference/eye-api-camera-cpp/latest/index.html) provides explanations of Mech-Eye API.

* **BasicDemo**
  Demonstrates how to use some of the VI samples to connect to a camera, adjust parameters, and acquire the 2D image and depth map.
  > Note: This VI sample requires the NI-IMAQ driver to be installed.
* **Demo**  
  Demonstrates how to use some of the VI samples to connect to a camera, adjust parameters, and acquire the 2D image, depth map, and point cloud.
  > Note: This VI sample requires LabVIEW full or professional development system and the NI-IMAQ driver to be installed.
* **Connect**  
  Connects to a camera based on the entered IP address.
* **Capture2D**  
  Obtains the 2D data from the camera.
* **Capture3D**  
  Obtains the 3D data from the camera.
* **CaptureAll2D3D**
  Obtains both the 2D and 3D data from the camera.
* **GetParameters**  
  Obtains the current values of the parameters common to all models from the camera.
* **SetParameters**  
  Sets the values of the parameters common to all models to the camera.
* **GetLaserParameters**  
  Obtains the current values of the parameters in the **Laser** category from the camera. This VI sample can only be used with laser cameras.
* **SetLaserParameters**  
  Sets the values of the parameters in the **Laser** category to the camera. This VI sample can only be used with laser cameras.
* **GetProjectorParameters**  
  Obtains the current values of the parameters in the **Projector** category from the camera. This VI sample can only be used with DLP cameras. Not all DLP cameras have all the parameters included in this VI sample. You can connect to the camera in Mech-Eye Viewer and check what parameters are available for the camera you use.
* **SetProjectorParameters**  
  Sets the values of the parameters in the **Projector** category to the camera. This VI sample can only be used with DLP cameras. Not all DLP cameras have all the parameters included in this VI sample. You can connect to the camera in Mech-Eye Viewer and check what parameters are available for the camera you use.
* **GetUhpParameters**  
  Obtains the current values of the parameters in the **UHP** category from the camera. This VI sample can only be used with the UHP series.
* **SetUhpParameters**  
  Sets the values of the parameters in the **UHP** category to the camera. This VI sample can only be used with the UHP series.
* **ShowColor2DImage**  
  Displays the obtained 2D data as a 2D image.
* **ShowDepthMap**  
  Displays the obtained 3D data as a depth map.
* **ShowColorPointCloud**  
  Displays the obtained 2D and 3D data as a textured point cloud.
  > Note: This VI sample requires LabVIEW full or professional development system.
* **ShowError**
  Displays the error code and description when an error occurs.

## Use the Demo VI Sample

The **Demo** VI sample gives an example of using some of the other VI samples to connect to the camera, adjust parameters, and acquire the 2D image, depth map, and point cloud.

You can run the **Demo** VI sample first to get to know the basic functionalities of the samples, and then create your own VI based on the **Demo** VI sample.

### Prerequisites

The following software products must be installed for the samples to be run successfully.

* Mech-Eye SDK: latest version

  > Note: Make sure you know where Mech-Eye SDK is installed. The installation directory is needed later on.

* LabVIEW: 64-bit full or professional development application and the NI-IMAQ driver are required

  > Note: Version 2023 Q3 has been tested.

### Instructions

Follow these steps to use the **Demo** VI sample:

1. Open LabVIEW, and click the **Open Existing** button.
2. Navigate to *Mech-Eye SDK-x.x.x/API/samples/labview* and select the **Demo** VI sample.
3. A **Find the .NET Assembly Named "MechEyeApiNet.dll"** window may pop up. Navigate to *Mech-Eye SDK-x.x.x/API/dll* and select the **MechEyeApiNet** DLL file.
4. Once the VI sample is opened, click the right-pointing arrow button in the upper left to run it.
5. In the **IP** text box, enter the IP address of the camera to which you want to connect, and then click the **Connect** button.
6. Once the camera is connected, the current values of some of the parameters are obtained and displayed in the **Parameters** tab. The **Demo** VI sample uses the **GetParameters** VI sample, so only the common parameters that all models have will be obtained.
7. In the **Parameters** tab, you can modify the parameter values, and then click the **Set Parameters** button in the lower right to set the values to the camera.
8. Go back to the **Connect & Capture** tab and click on the **Capture Once** button to obtain the 2D and 3D data once. The obtained data are displayed as a 2D image, depth map, and point cloud to the right.
9. Click the **Disconnect** button to disconnect from the camera. The VI sample is also stopped.
