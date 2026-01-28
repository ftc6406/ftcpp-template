# Code Source
- [FTCpp](https://github.com/flemmii/FTCpp)
- [Official FTC SDK](https://github.com/FIRST-Tech-Challenge/FtcRobotController)

# What is this?

This is a project that makes it possible to program in C++ in FTC. This is also 100%
competition legal cause it still uses the SDK, it just accesses it from C++ via the
Java Native Interface (JNI).

This repository contains the public FTC SDK for the DECODE (2025-2026) competition season. (But in C++)

## Advantages
- Faster execution (Exact data from the [Test Results](https://github.com/flemmii/FTCpp-SDK/blob/Tests/TeamCode/src/main/java/org/firstinspires/ftc/teamcode/tests/TestResults.md))
- No forced object orientation
- Compiler statements
- Access to OpenCV as a native library
- Access to other C++ libraries
- You can still use Java and use this project just as an extension

## Disadvantages
- Not every feature from the SDK is included yet
- More difficult debugging
- No access to Java libraries such as Roadrunner

## Requirements
To use this Android Studio project, you will need Android Studio Ladybug (2024.2) or later.

## Who should use this?
As you see above as a rookie team I wouldn't suggest you to use this. It is rather designed for
more experienced teams who want to try something new and who want to push their software to the
limit to get the best loop times possible.

# Downloading this project

To download this repository, simply run the following command in your terminal:

```bash
git clone https://github.com/flemmii/FTCpp-SDK.git
```

After cloning you need to execute the build process once so after that everything is set up
and you can download the code normally to your robot. Also after a clean you need to
execute the build process once before downloading. (This will get changed later)

Also make sure that you have node installed, otherwise [download it here](https://nodejs.org/en/download/prebuilt-installer)

Remember you need to merge this repository into your own repository to get the latest
updates.

## Excluding the example from downloading

If you don't want the example to be downloaded to your repository ever time you pull you can
you can just run this command in the root of your project:

```bash
git update-index --assume-unchanged TeamCode/src/main/cpp/teamcode/header/example.h
git update-index --assume-unchanged TeamCode/src/main/cpp/teamcode/sources/example.cpp
```

# The different folders

You can find these folders in TeamCode/src/main/cpp

## createOpModeJava

This folder contains two template files that are used to create the equivalent OpMode in Java.
It also has the JavaScript file that creates the files in Java.

You do not need to do anything in this folder.

## external_libraries

This folder contains the external libraries that are used in the project:

- [OpenCV](https://github.com/opencv/opencv)
- [Apriltag](https://github.com/AprilRobotics/apriltag)

The sources of these projects are already included by the FTC SDK.

If you want to add any of other libraries put the header files in there.

## sdk

This folder contains the C++ framework of the SDK that is used to communicate with the
robot controller.

You can add your own sensors, motors or whatever you need. If you do so it'd be nice if you
could open a pull request on GitHub on the FTCpp repo to share your code with others.

## Version 11.1 (20251231-104637)

### Enhancements

* Gamepad triggers can now be accessed as booleans and have edge detection supported.
* GoBildaPinpointDriver now supports Pinpoint v2 functionality
* Adds webcam calibrations for goBILDA's USB camera.

### Bug Fixes
* Fixes issue [1654](https://github.com/FIRST-Tech-Challenge/FtcRobotController/issues/1654) in GoBildaPinpointDriver that caused error if resolution was set in other than MM
* Fixes issue [1628](https://github.com/FIRST-Tech-Challenge/FtcRobotController/issues/1628) Blocks editor displays incorrect Java code for gamepad edge detection blocks.
* Fixes possible race condition issue [1884](https://github.com/FIRST-Tech-Challenge/FtcRobotController/issues/1884) on Driver Station startup when Driver Station name doesn't match the Robot Controller name.
* Fixes issue [1863](https://github.com/FIRST-Tech-Challenge/FtcRobotController/issues/1863) - Incorrect package paths in samples.
* Fixes an issue where an OnBotJava filename that begins with a lowercase character would fail to properly rename the file if the user tried to rename it so that it begins with an uppercase character.

## Version 11.0 (20250827-105138)

### Enhancements

* OnBotJava now has the concept of a project.  
  A project is a collection of related files.  A project may be chosen by selecting 'Example Project'
  from the 'File type:' dropdown.  Doing so will populate the dropdown to the immediate right with 
  a list of projects to choose from.
  When selecting a project all of the related files appear in the left pane of the workspace 
  underneath a directory with the chosen project name.
  This is useful for example for ConceptExternalHardwareClass which has a dependency upon
  RobotHardware.  This feature simplifies the usage of this Concept example by automatically
  pulling in dependent classes.
* Adds support for AndyMark ToF, IMU, and Color sensors.
* The Driver Station app indicates if WiFi is disabled on the device.
* Adds several features to the Color Processing software:
  * DECODE colors `ARTIFACT_GREEN` and `ARTIFACT_PURPLE`
  * Choice of the order of pre-processing steps Erode and Dilate
  * Best-fit preview shape called `circleFit`, an alternate to the existing `boxFit`
  * Sample OpMode `ConceptVisionColorLocator_Circle`, an alternate to the renamed `ConceptVisionColorLocator_Rectangle`
* The Driver Station app play button has a green background with a white play symbol if
  * the driver station and robot controller are connected and have the same team number
  * there is at least one gamepad attached
  * the timer is enabled (for an Autonomous OpMode)
* Updated AprilTag Library for DECODE. Notably, getCurrentGameTagLibrary() now returns DECODE tags.
  * Since the AprilTags on the Obelisk should not be used for localization, the ConceptAprilTagLocalization samples only use those tags without the name 'Obelisk' in them.
* OctoQuad I2C driver updated to support firmware v3.x 
  * Adds support for odometry localizer on MK2 hardware revision
  * Adds ability to track position for an absolute encoder across multiple rotations
  * Note that some driver APIs have changed; minor updates to user software may be required
  * Requires firmware v3.x. For instructions on updating firmware, see
    https://github.com/DigitalChickenLabs/OctoQuad/blob/master/documentation/OctoQuadDatasheet_Rev_3.0C.pdf


## Version 10.3 (20250625-090416)

### Breaking Changes
* The behavior of setGlobalErrorMsg() is changed.  Note that this is an SDK internal method that is not 
  meant to be used by team software or third party libraries.  Teams or libraries using this method should
  find another means to communicate failure.  The design intent of setGlobalErrorMsg() is to report an 
  error and force the user to restart the robot, which in certain circumstances when used inappropriately
  could cause a robot to continue running while Driver Station controls are disabled.  To prevent this,
  processing of a call to setGlobalErrorMsg() is deferred until the robot is in a known safe state.  This may
  mean that a call to setGlobalErrorMsg() that does not also result in stopping a running OpMode will appear
  as though nothing happened until the robot is stopped, at which point, if clearGlobalErrorMsg() has not 
  been called the message will appear on the Driver Station and a restart will be required.
  Addresses issue [1381](https://github.com/FIRST-Tech-Challenge/FtcRobotController/issues/1381)
* Fixes getLatestResult in Limelight3A so if the Limelight hasn't provided data yet, it still returns an LLResult but valid will be false
  * If you previously used to check and see if this was `null` to see if the Limelight had been contacted, you now need to use `isValid()` on the result.  That is because now it always returns an LLResult even before it talks to the Limelight, but if it doesn't have valid data, the `isValid()` will be `false`.
* Changed all omni samples to use front_left_drive, front_right_drive, back_left_drive, back_right_drive
  * This is only breaking for you if you copy one of the changed samples to your own project and expect to use the same robot configuration as before.

### Known Issues
* The redesigned OnBotJava new file workflow allows the user to use a lowercase letter as the first character of a filename.
  This is a regression from 10.2 which required the first character to be uppercase.  Software will build, but if the user tries
  to rename the file, the rename will fail.

### Enhancements
* Improved the OBJ new file creation flow workflow. The new flow allows you to easily use samples, craft new custom OpModes and make new Java classes.
* Added support for gamepad edge detection.
  * A new sample program `ConceptGamepadEdgeDetection` demonstrates its use.
* Adds a blackboard member to the Opmode that maintains state between opmodes (but not between robot resets).  See the ConceptBlackboard sample for how to use it.
* Updated PredominantColorProcessor to also return the predominant color in RGB, HSV and YCrCb color spaces.  Updated ConceptVisionColorSensor sample OpMode to display the getAnalysis() result in all three color spaces.
* Adds support for the GoBilda Pinpoint 
  * Also adds `SensorGoBildaPinpoint` sample to show how to use it
* Added `getArcLength()` and `getCircularity()` to ColorBlobLocatorProcessor.Blob.  Added BY_ARC_LENGTH and BY_CIRCULARITY as additional BlobCriteria.
* Added `filterByCriteria()` and `sortByCriteria()` to ColorBlobLocatorProcessor.Util.
  * The filter and sort methods for specific criteria have been deprecated.
  * The updated sample program `ConceptVisionColorLocator` provides more details on the new syntax.
* Add Help menu item and Help page that is available when connected to the robot controller via Program and Manage. The Help page has links to team resources such as [FTC Documentation](https://ftc-docs.firstinspires.org/), [FTC Discussion Forums](https://ftc-community.firstinspires.org), [Java FTC SDK API Documentation](https://javadoc.io/doc/org.firstinspires.ftc), and [FTC Game Information](https://ftc.game/).
* Self inspection changes:
  * List both the Driver Station Name and Robot Controller Name when inspecting the Driver Station.
  * Report if the team number portion of the device names do not match.
  * -rc is no longer valid as part of a Robot Controller name, must be -RC.
  * Use Robot Controller Name or Driver Station Name labels on the inspection screens instead of WIFI Access Point or WIFI Direct Name.

### Bug Fixes
* Fixes issue [1478](https://github.com/FIRST-Tech-Challenge/FtcRobotController/issues/1478) in AnnotatedHooksClassFilter that ignored exceptions if they occur in one of the SDK app hooks.
* Fix initialize in distance sensor (Rev 2m) to prevent bad data in first call to getDistance.
* Fixes issue [1470](https://github.com/FIRST-Tech-Challenge/FtcRobotController/issues/1470) Scaling a servo range is now irrespective of reverse() being called.  For example, if you set the scale range to [0.0, 0.5] and the servo is reversed, it will be from 0.5 to 0.0, NOT 1.0 to 0.5.
* Fixes issue [1232](https://github.com/FIRST-Tech-Challenge/FtcRobotController/issues/1232), a rare race condition where using the log rapidly along with other telemetry could cause a crash.

## Version 10.2 (20250121-174034)

### Enhancements
* Add ability to upload the pipeline for Limelight3A which allows teams to version control their limelight pipelines.


### Bug Fixes

* Fix an internal bug where if the RUN_TO_POSITION run mode was specified before a target position, recovery would require a power cycle. A side effect of this fix is that a stack trace identifying the location of the error is always produced in the log. Fixes issue [1345](https://github.com/FIRST-Tech-Challenge/FtcRobotController/issues/1345).
* Throws a helpful exception if region of interest is set to null when building a PredominantColorProcessor. Also sets the default RoI to the full frame. Addresses issue [1076](FIRST-Tech-Challenge/FtcRobotController#1076)
* Throws a helpful exception if user tries to construct an ImageRegion with malformed boundaries.  Addresses issue [1078](FIRST-Tech-Challenge/FtcRobotController#1078)

## Version 10.1.1 (20241102-092223)

### Breaking Changes

* Support for Android Studio Ladybug.  Requires Android Studio Ladybug.  

### Known Issues

* Android Studio Ladybug's bundled JDK is version 21.  JDK 21 has deprecated support for Java 1.8, and Ladybug will warn on this deprecation.
  OnBotJava only supports Java 1.8, therefore, in order to ensure that software developed using Android Studio will 
  run within the OnBotJava environment, the targetCompatibility and sourceCompatibility versions for the SDK have been left at VERSION_1_8.
  FIRST has decided that until it can devote the resources to migrating OnBotJava to a newer version of Java, the deprecation is the 
  lesser of two non-optimal situations.

### Enhancements

* Added `toString()` method to Pose2D
* Added `toString()` method to SparkFunOTOS.Pose2D

## Version 10.1 (20240919-122750)

## teamcode

This module, teamcode, is the place where you will write/paste the code for your team's
robot controller App. This module has currently only one example but the
process for adding OpModes is straightforward.

## Creating your own OpModes

The easiest way to create your own OpMode is to copy a Example OpMode and make it your own.

But if you want to create a new OpMode from scratch you can use the following steps:

- Create a new file in the header folder with the name of your OpMode
- Create a new file in the source folder with the name of your OpMode
- Add the following code to the header file:

```cpp
#include <jni.h>
#include "sdk.h"

// Your OpMode annotation shown below
    
extern "C" void Example();
```

- Add the following code to the source file:

```cpp
extern "C" void Example() {
    // Your code here
}
```

- Change the path to your OpMode by just changing the
  Java_org_firstinspires_ftc_teamcode_opmodes_teleop_Example_opMode to your path.
    - The penultimate part of the path is the name of the Java file and Class
    - The last part is the name of the method in there

### Annotations

You got the same annotations as in Java, the only difference is that they need to be in a
comment in you header file of your OpMode in the header folder.

```
 @TeleOp(name="Example", group="Example")
 @Disabled
```

The name that will appear on the driver station's "opmode list" is defined by the code:
``name="Template: Linear OpMode"``
You can change what appears between the quotes to better describe your opmode.
The "group=" portion of the code can be used to help organize your list of OpModes.

As shown, the current OpMode will NOT appear on the driver station's OpMode list because of the
``@Disabled`` annotation which has been included.
This line can simply be deleted to make the OpMode visible.

### Changing the folder structure

If you want to move your header to another folder simply head to the createOpModeJava/index.js
file and change the folder name in line 36 to the path of your desire.
Also change the path in the CMakelists.txt in line 70 to the same path.

If you want to move your sources to another folder you just need to change the path in the
CMakelists.txt in line 18 to the path of your desire.

# Troubleshooting

You can always open an issue on GitHub or write me on Discord (flemmii) if you have any problems.
But please try to solve the problem yourself first.

## Build fails

You get normal error messages in the terminal, so you can see what went wrong.

## Code crashes on robot

You can only see the errors in logcat, so nothing will be shown on the Driver Hub.
If you want to log anything additional to logcat simply include the sdk/extras/utils.h file
and use the log function.

<details close>
  <summary> How a log looks like </summary>
  <span style="color:Red">
  JNI DETECTED ERROR IN APPLICATION: JNI NewGlobalRef called with pending exception java.lang.IllegalArgumentException: Unable to find a hardware device with name "test" and type DcMotorEx  
  at java.lang.Object com.qualcomm.robotcore.hardware.HardwareMap.get(java.lang.Class, java.lang.String) (HardwareMap.java:213)
  at void org.firstinspires.ftc.teamcode.opmodes.autonomous.AutoTest.opMode() (AutoTest.java:-2)
  at void org.firstinspires.ftc.teamcode.opmodes.autonomous.AutoTest.runOpMode() (AutoTest.java:15)
  at void com.qualcomm.robotcore.eventloop.opmode.LinearOpMode.internalRunOpMode() (LinearOpMode.java:199)
  at void com.qualcomm.robotcore.eventloop.opmode.OpModeInternal.lambda$internalInit$1$com-qualcomm-robotcore-eventloop-opmode-OpModeInternal() (OpModeInternal.java:181)
  at void com.qualcomm.robotcore.eventloop.opmode.OpModeInternal$$ExternalSyntheticLambda1.run() (D8$$SyntheticClass:-1)
  at void com.qualcomm.robotcore.util.ThreadPool.logThreadLifeCycle(java.lang.String, java.lang.Runnable) (ThreadPool.java:737)
  at void com.qualcomm.robotcore.eventloop.opmode.OpModeInternal.lambda$internalInit$2$com-qualcomm-robotcore-eventloop-opmode-OpModeInternal() (OpModeInternal.java:179)
  at void com.qualcomm.robotcore.eventloop.opmode.OpModeInternal$$ExternalSyntheticLambda2.run() (D8$$SyntheticClass:-1)
  at void java.util.concurrent.ThreadPoolExecutor.runWorker(java.util.concurrent.ThreadPoolExecutor$Worker) (ThreadPoolExecutor.java:1133)
  at void java.util.concurrent.ThreadPoolExecutor$Worker.run() (ThreadPoolExecutor.java:607)
  at void com.qualcomm.robotcore.util.ThreadPool$ThreadFactoryImpl$1.run() (ThreadPool.java:793)
  at void java.lang.Thread.run() (Thread.java:761)
  in call to NewGlobalRef
  from void org.firstinspires.ftc.teamcode.opmodes.autonomous.AutoTest.opMode()
  "OpModeThread" prio=5 tid=58 Runnable
  | group="main" sCount=0 dsCount=0 obj=0x137fc280 self=0x782599e200
  | sysTid=3589 nice=0 cgrp=default sched=0/0 handle=0x781fdf0450
  | state=R schedstat=( 0 0 0 ) utm=106 stm=2 core=2 HZ=100
  | stack=0x781fcee000-0x781fcf0000 stackSize=1037KB
  | held mutexes= "mutator lock"(shared held)
  native: #00 pc 000000000047ef3c  /system/lib64/libart.so (_ZN3art15DumpNativeStackERNSt3__113basic_ostreamIcNS0_11char_traitsIcEEEEiP12BacktraceMapPKcPNS_9ArtMethodEPv+220)
  native: #01 pc 000000000047ef38  /system/lib64/libart.so (_ZN3art15DumpNativeStackERNSt3__113basic_ostreamIcNS0_11char_traitsIcEEEEiP12BacktraceMapPKcPNS_9ArtMethodEPv+216)
  native: #02 pc 0000000000452fc4  /system/lib64/libart.so (_ZNK3art6Thread9DumpStackERNSt3__113basic_ostreamIcNS1_11char_traitsIcEEEEbP12BacktraceMap+480)
  native: #03 pc 00000000002f04a4  /system/lib64/libart.so (_ZN3art9JavaVMExt8JniAbortEPKcS2_+1136)
  native: #04 pc 00000000002f0bb4  /system/lib64/libart.so (_ZN3art9JavaVMExt9JniAbortVEPKcS2_St9__va_list+124)
  native: #05 pc 0000000000102798  /system/lib64/libart.so (_ZN3art11ScopedCheck6AbortFEPKcz+156)
  native: #06 pc 00000000001021a8  /system/lib64/libart.so (_ZN3art11ScopedCheck11CheckThreadEP7_JNIEnv+536)
  native: #07 pc 00000000000ffce8  /system/lib64/libart.so (_ZN3art11ScopedCheck5CheckERNS_18ScopedObjectAccessEbPKcPNS_12JniValueTypeE+1124)
  native: #08 pc 0000000000103a7c  /system/lib64/libart.so (_ZN3art8CheckJNI6NewRefEPKcP7_JNIEnvP8_jobjectNS_15IndirectRefKindE+624)
  native: #09 pc 0000000000014648  /data/app/com.qualcomm.ftcrobotcontroller-1/lib/arm64/libsdk.so (_ZN7_JNIEnv12NewGlobalRefEP8_jobject+40)
  native: #10 pc 000000000001c7f0  /data/app/com.qualcomm.ftcrobotcontroller-1/lib/arm64/libsdk.so (_ZN3sdk12hardware_map3getEP7_jclassRKNSt6__ndk112basic_stringIcNS3_11char_traitsIcEENS3_9allocatorIcEEEE+236)
  native: #11 pc 0000000000070f04  /data/app/com.qualcomm.ftcrobotcontroller-1/lib/arm64/libteamcode.so (Java_org_firstinspires_ftc_teamcode_opmodes_autonomous_AutoTest_opMode+3036)
  native: #12 pc 000000000011e230  /data/app/com.qualcomm.ftcrobotcontroller-1/oat/arm64/base.odex (Java_org_firstinspires_ftc_teamcode_opmodes_autonomous_AutoTest_opMode__+124)
  </span>
</details>
&nbsp;

This looks like a lot but if you look at specific lines you can find out where the issue is.
The last line (this is just the last line in this excerpt it will be in somewhere hidden in the error normally) shows this: Java_org_firstinspires_ftc_teamcode_opmodes_autonomous_AutoTest_opMode__+124 and by that you can see that the error is in the AutoTest_opMode. The type of error and error description is at the top of the error.

If it says anything with JNI and you have done nothing with JNI, its probably an error in the sdk.
If that happens please open an issue on GitHub or write me on Discord (flemmii).
Please send me what you tried to do, so the code you used and the error message.

# Contributing

If you want to contribute to this project, you can simply open a pull request on GitHub.
It doesn't matter if you want to add a new feature, fix a bug, add an example or just improve
the documentation.

If you want to help me even further consider to DM me on Discord (flemmii), so
I can add you to the project and you don't need to open pull request every time.

## Feature requests

If you have any feature requests, you can open an issue on GitHub or write me on Discord (flemmii).
I will try to implement them as soon as possible. You can also try to implement them yourself, if
you do so please open a pull request on GitHub to share your code with others.
