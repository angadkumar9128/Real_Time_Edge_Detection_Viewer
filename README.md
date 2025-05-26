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

## 📷 Screenshots

# Native Frame Processing 

Image_01 :
![WhatsApp Image 2025-05-26 at 14 08 48_ccf92696](https://github.com/user-attachments/assets/e80d53b3-8bc3-428d-8c53-d23629b03ec5)

Image_02 :
![WhatsApp Image 2025-05-26 at 14 08 49_b4c2768c](https://github.com/user-attachments/assets/8b7191c0-2ab4-4fdd-8ba7-46995db2e661)

Image_03 :
![WhatsApp Image 2025-05-26 at 14 08 50_6b369c0c](https://github.com/user-attachments/assets/f4f5db95-7a94-462e-8aac-cab183d03ff0)

Image_04 : 
![WhatsApp Image 2025-05-26 at 14 08 50_a98b90de](https://github.com/user-attachments/assets/6af885ec-3f36-4c97-99f5-79ee5d9a673d)

Image_05 :
![WhatsApp Image 2025-05-26 at 14 08 50_25f84a11](https://github.com/user-attachments/assets/510a30e3-58f0-44a9-93f9-16bd9d2aa1be)


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

## 📃 License

MIT License. Use it freely and contribute back if you improve it!

