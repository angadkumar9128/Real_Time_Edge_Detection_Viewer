# Real_Time_Edge_Detection_Viewer
 This project is a real-time edge detection Android app using OpenCV and C++ (NDK). It captures frames from the device camera, processes them natively with OpenCV for edge detection, and displays the result using OpenGL or Android views. It demonstrates efficient native image processing on mobile platforms.


# Android NDK OpenCV Camera App

An Android app that captures real-time camera frames using `GLSurfaceView`, passes them through the NDK using JNI, and applies image processing using OpenCV.

---

## ✅ Features Implemented

- 📷 Real-time camera preview using `GLSurfaceView`
- 🧠 Frame processing done in native C++ using OpenCV
- 🚀 Efficient data transfer between Java and native layers via JNI
- 🔄 Fixed preview orientation and mirroring (front/back camera support)
- 🧪 Placeholder for applying image filters (e.g., grayscale, edge detection)

---

## 📷 Processed Edge Detection Screenshots

# These images showcase the edge detection results processed by the native OpenCV C++ pipeline, demonstrating the app’s real-time image processing capability:

| Image 01                                                                                      | Image 02                                                                                      |
| --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| ![Image\_01](https://github.com/user-attachments/assets/6ffba916-65b7-49d4-91e4-af2ff7993395) | ![Image\_02](https://github.com/user-attachments/assets/abcb3090-2d8c-4933-8ee4-6d265af4e621) |

| Image 03                                                                                      | Image 04                                                                                      |
| --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| ![Image\_03](https://github.com/user-attachments/assets/862ccce0-ec89-4b8b-9404-ec50a76e69d0) | ![Image\_04](https://github.com/user-attachments/assets/e6d16d29-3281-4cf2-baa7-ac5eb3c07606) |

| Image 05                                                                                      |   |
| --------------------------------------------------------------------------------------------- | - |
| ![Image\_05](https://github.com/user-attachments/assets/636e9ea1-533d-4e14-8fb3-38325fed6864) |   |


---

## ⚙️ Setup Instructions

### Prerequisites

- Android Studio (Electric Eel or later recommended)
- Android NDK (version 23 or later)
- OpenCV Android SDK (tested with OpenCV 4.5+)

### Steps to Set Up

1. **Install NDK**  
   In Android Studio:  
   `Preferences > SDK Manager > SDK Tools > NDK (Side by side)`  
   Select and install it.

2. **Download and Link OpenCV**  
   - Download OpenCV Android SDK from:  
     [https://opencv.org/releases](https://opencv.org/releases)  
   - Unzip and copy the `sdk/native` folder to your project's root.
   - Update `CMakeLists.txt` to include OpenCV:

     ```cmake
     set(OpenCV_DIR ${CMAKE_SOURCE_DIR}/opencv/native/jni)
     find_package(OpenCV REQUIRED)
     include_directories(${OpenCV_INCLUDE_DIRS})
     target_link_libraries(native-lib ${OpenCV_LIBS})
     ```

3. **Sync Gradle and Build Project**  
   Build your project to ensure JNI and OpenCV are correctly linked.

---

## 🧠 Architecture and Frame Flow

### 🔄 Data Flow

Java Camera Frame → SurfaceTexture → GLSurfaceView
↓
Frame extracted as ByteBuffer
↓
Sent via JNI → C++ (native-lib.cpp)
↓
OpenCV processes frame (e.g., to grayscale)
↓
Output returned to Java or rendered


### 🧩 Components

- `MainActivity.java`: Initializes camera and OpenGL rendering surface
- `CameraRenderer.java`: Handles texture rendering and frame acquisition
- `native-lib.cpp`: Contains native JNI functions and OpenCV processing
- `CMakeLists.txt`: Configures build pipeline and OpenCV linking

---

## 📁 Directory Structure

├── app/
│ ├── src/
│ │ ├── main/
│ │ │ ├── cpp/ # Native C++ code
│ │ │ │ └── native-lib.cpp
│ │ │ ├── java/
│ │ │ │ ├── ... # Java code (Camera, Renderer)
│ │ │ └── res/ # Layouts and resources
│ ├── CMakeLists.txt # NDK build config
├── opencv/ # OpenCV SDK (native only)
│ └── native/ # JNI build libs
└── README.md


---

## 📌 Notes

- Ensure `externalNativeBuild` in `build.gradle` is configured for CMake.
- Some devices may require camera permission and NDK ABI filters (`armeabi-v7a`, `arm64-v8a`).
- Use `glPixelStorei(GL_UNPACK_ALIGNMENT, 1);` to avoid texture misalignment.

---

