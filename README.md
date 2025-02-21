# 📌 Firebase Integration Guide for Unity iOS

This guide provides step-by-step instructions for **editing the Podfile, installing dependencies, configuring Xcode, and running your Unity iOS project**.

---

## 🛠 Step 1: Edit the Podfile
1. Open **Terminal** and navigate to your **Unity iOS build folder**:
   ```sh
   cd /path/to/your/unity/ios/build/folder
   ```
2. Open the **Podfile** in a text editor (e.g., Nano or VS Code):
   ```sh
   nano Podfile
   ```
3. **Replace or add the following content:**
   ```ruby
   source 'https://cdn.cocoapods.org/'

   platform :ios, '12.0'
   use_frameworks! :linkage => :static 

   target 'UnityFramework' do
     pod 'Firebase/Auth', '8.10.0'
     pod 'Firebase/Core', '8.10.0'
     pod 'Firebase/Firestore', '8.10.0'
   end

   target 'Unity-iPhone' do
   end

   post_install do |installer|
     installer.pods_project.targets.each do |target|
       target.build_configurations.each do |config|
         config.build_settings['CLANG_CXX_LANGUAGE_STANDARD'] = 'c++17'
       end
     end
   end
   ```
4. **Save and exit the editor:**
   - If using **Nano**, press:
     ```
     CTRL + X → Y → Enter
     ```

---

## 🛠 Step 2: Install CocoaPods
1. In **Terminal**, navigate to the build folder:
   ```sh
   cd /path/to/your/unity/ios/build/folder
   ```
2. **Run `pod install`** to install dependencies:
   ```sh
   pod install
   ```
3. Wait for the installation to complete.

---

## 🛠 Step 3: Open Xcode and Configure Settings
1. **Open Xcode** by running:
   ```sh
   open Unity-iPhone.xcworkspace
   ```
2. In **Xcode**, navigate to:
   - **Project:** `Unity-iPhone`
   - **Target:** `Unity-iPhone`
3. **Adjust Build Settings**:
   - Go to **Build Settings**.
   - **Search** for `iOS Deployment Target` and **set it to 13.0**.
   - **Search** for `C++ Language Dialect` and **set it to C++17**.

---

## 🛠 Step 4: Modify `UnityAppController.mm` for Firebase
1. In Xcode, navigate to:
   ```
   Unity-iPhone → Classes → UnityAppController.mm
   ```
2. **Add the Firebase import at the top**:
   ```objc
   #import <Firebase.h>
   ```
3. **Initialize Firebase inside `didFinishLaunchingWithOptions`**:
   ```objc
   - (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions
   {
       [FIRApp configure];  // 🔹 Add this line to initialize Firebase
       return [super application:application didFinishLaunchingWithOptions:launchOptions];
   }
   ```

---

## 🛠 Step 5: Build and Run
1. **Click the "Run" button** in Xcode (`⌘R`).
2. The project should now build successfully and run on an **iOS device or simulator**.

---

### 🚀 Your Unity iOS project is now configured with Firebase! 【Not Really!!】
