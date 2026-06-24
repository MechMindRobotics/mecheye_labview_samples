# LabVIEW Samples

This documentation provides descriptions of the other LabVIEW VI samples and instructions on using the demo VI samples to control a Mech-Eye Industrial 3D Camera.

## Sample List

The following VI samples are provided. These VI samples use C# Mech-Eye API to realize the corresponding functions. [Mech-Eye API Reference](https://docs.mech-mind.net/en/eye-3d-camera/latest/api/api-reference.html) provides explanations of Mech-Eye API.

* **BasicDemo**  
  (For LabVIEW Base) Demonstrates how to use some of the VI samples to connect to a camera, adjust parameters, and acquire the 2D image and depth map.
  > Note: This VI sample requires the NI-IMAQ driver to be installed.

* **Demo**  
  (For LabVIEW Full and Professional) Demonstrates how to use some of the VI samples to connect to a camera, adjust parameters, and acquire the 2D image, depth map, and point cloud.
  > Note: This VI sample requires the NI-IMAQ driver to be installed.
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
* **ShowError**
  Displays the error code and description when an error occurs.

## Use the demo VI Samples

The **BasicDemo** and **Demo** VI samples give an example of using some of the other VI samples to connect to the camera, adjust parameters, and acquire data.

You can run the **BasicDemo** or **Demo** VI sample first to get to know the basic functionalities of the samples, and then create your own VI based on the **BasicDemo** or **Demo** VI sample.

### Prerequisites

The following software products must be installed for the samples to be run successfully.

* Mech-Eye SDK: latest version

  > Note: Make sure you know where Mech-Eye SDK is installed. The installation directory is needed later on.

* LabVIEW: 64-bit application bitness and the NI-IMAQ driver are required

  > Note: Version 2023 Q3 has been tested.

### Instructions

Follow these steps to use the **BasicDemo** or **Demo** VI sample:

1. Open LabVIEW, and click the **Open Existing** button.
2. Navigate to *Mech-Eye SDK-x.x.x/API/samples/labview* and select the **BasicDemo** or **Demo** VI sample.
3. A **Find the .NET Assembly Named "MechEyeApiNet.dll"** window may pop up. Navigate to *Mech-Eye SDK-x.x.x/API/dll/net48* and select the **MechEyeApiNet** DLL file.
4. Once the VI sample is opened, click the right-pointing arrow button in the upper left to run it.
5. In the **IP** text box, enter the IP address of the camera to which you want to connect, and then click the **Connect** button.
6. Once the camera is connected, the current values of some of the parameters are obtained and displayed in the **Parameters** tab. The **BasicDemo** or **Demo** VI sample uses the **GetParameters** VI sample, so only the common parameters that all models have will be obtained.
7. In the **Parameters** tab, you can modify the parameter values, and then click the **Set Parameters** button in the lower right to set the values to the camera.

   > Note: The **Ultra M ProcessingParams** section in **BasicDemo** is only for the ULTRA M model. Parameters in this section are only available and will only take effect when connected to an ULTRA M camera. For all other camera models, these parameters should be left unchanged.
8. Go back to the **Connect & Capture** tab and click on the **Capture Once** button to obtain the 2D and 3D data once. The obtained data are displayed to the right.
9. Click the **Disconnect** button to disconnect from the camera. The VI sample is also stopped.

  > 💡 **If LabView cannot connect with the device and prompts Error 1172，try to copy the following files: MechEyeApi.dll, MechEyeApiWrapper.dll, MechEyeApiNet.dll, and SkiaSharp.dll, and paste them to the sample folder of LabView .vi files.**

### Notes for ULTRA M users

The **BasicDemo** front panel includes four additional **Group** controls in the **Parameters** tab:

* **Group Exposure Selector**
* **Group Scan3D Exposure Time**
* **Group Scan3D Gain**
* **Group DLP Power Level**

These four controls **only need to be set when using the ULTRA M series**. The **SetParameters** VI uses capability-first probing (via `GetAvailableParametersArr`) to detect whether the connected camera exposes the grouped parameter set. On any other camera model that does not expose these grouped parameters, the four controls are silently skipped and have no effect — there is no need to test or configure them.

In addition, the **BasicDemo** front panel exposes a **Ultra M ProcessingParams** cluster (placed below the main controls) containing the seven ULTRA M point-cloud post-processing parameters:

* **DepthSmooth** (Off / Weak / Normal / Strong)
* **DepthHoleFilling** (Off / Weak / Normal / Strong)
* **DepthSurfaceNoiseRemoval** (Off / Weak / Normal / Strong)
* **LargeGradNoiseRemoval** (Off / Weak / Normal / Strong)
* **SpuriousPhaseRemoval** (Off / Weak / Normal / Strong)
* **PhaseClusterOutlierRemoval** (L0 ... L10, default L5)
* **PointCloudEdgePreservation** (Sharp / Normal / Smooth, default Normal)

These seven parameters share the same capability-first probing strategy as the four **Group** controls above: the **SetParameters** VI checks the available parameter list returned by `GetAvailableParametersArr` for the sentinel parameter `DepthSmooth`, and only when the sentinel is present (i.e. the connected camera is an ULTRA M running a firmware that exposes the post-processing parameter set) are all seven `SetEnumValue` calls executed inside a single guarded branch. On any other camera model the entire post-processing block is silently skipped and no `SHOW ERROR` dialogs are produced, keeping the BasicDemo behavior on non-ULTRA-M cameras unchanged. ULTRA M users with **Mech-Eye SDK 2.6.0 or later** can adjust the cluster values directly from the front panel before clicking **Set Parameters**.

### Notes for Mech-Eye SDK 2.6.0+ users

These VI samples are compiled and validated against **Mech-Eye SDK 2.5.4** (`MechEyeApiNet.dll` strong-name version `2.5.4.0`).

If you have installed **Mech-Eye SDK 2.6.0 or later** and need to connect to a camera that requires the 2.6.0+ runtime (for example, the ULTRA M series), the .NET assembly version reference inside each VI must match the installed `MechEyeApiNet.dll`. Otherwise the VI sample will fail to load with a *FileLoadException* / *Find the .NET Assembly* prompt.

Two options are available:

1. **Replace the four DLLs in the LabVIEW installation directory.**  
   Copy the following four files from `Mech-Eye SDK-2.6.x/API/dll/` (for `MechEyeApi.dll` and `MechEyeApiWrapper.dll`) and `Mech-Eye SDK-2.6.x/API/dll/net48/` (for `MechEyeApiNet.dll` and `SkiaSharp.dll`) into the LabVIEW installation directory (typically `C:\Program Files\National Instruments\LabVIEW <version>\`):

   * `MechEyeApi.dll`
   * `MechEyeApiWrapper.dll`
   * `MechEyeApiNet.dll`
   * `SkiaSharp.dll` (new dependency introduced in 2.6.0)

   Then patch the embedded strong-name version inside each affected VI file by replacing the ASCII byte sequence `2.5.4.0` with `2.6.0.0`. All VI files in this directory reference `MechEyeApiNet` and must be patched:

   * `BasicDemo.vi`, `Capture2D.vi`, `Capture2DAnd3D.vi`, `Capture3D.vi`, `Connect.vi`, `Demo.vi`, `GetLaserParameters.vi`, `GetParameters.vi`, `GetProjectorParameters.vi`, `GetUhpCaptureMode.vi`, `SetLaserParameters.vi`, `SetParameters.vi`, `SetProjectorParameters.vi`, `SetUhpCaptureMode.vi`, `ShowColor2DImage.vi`, `ShowDepthMap.vi`, `ShowError.vi`, `ShowTexturedPointCloud.vi`

   > Note: `2.5.4.0` and `2.6.0.0` have the same byte length, so the patch is an in-place binary replacement. After patching, restart LabVIEW.

2. **Re-link the .NET assembly inside each VI manually.**  
   Open each VI in LabVIEW, locate every .NET Constructor Node / Invoke Node that references `MechEyeApiNet`, and re-select the 2.6.0+ `MechEyeApiNet.dll` from the new SDK installation directory.
