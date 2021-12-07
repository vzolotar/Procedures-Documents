## Cordova installation on Windows 10 (for android only)  

### 1. Install Git for Windows
-   Browse to the [Git for Windows homepage](https://git-for-windows.github.io/).
-   Select the big Download button 
- Install with all of the default options.

### 2. Installing Java
**Note: Make sure you use jdk1.8.0x**

•	Go to the [Java download page](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
To check that Java was installed correctly, open a terminal window and type **java -version** in command prompt . You should see the Java version printed to the terminal.

### 3. Installing Android command line tools
•	Go to the [Android SDK Command Line tools installation page](https://developer.android.com/studio/index.html#command-tools)

-   When it has finished downloading, open the Windows File Explorer.
-   Navigate to the C:\ drive folder. You should see a few folders here, including Program Files.
-   Create a new folder in the C:\ drive names android.
-   Unzip the downloaded file to this new folder. This will take a few minutes.

When you are done, you should have a new folder at C:\android\tools. C:\android\cmdline-tools\tools

### 4. Installing the SDK

We’ll now use the Command Line tools to install the SDK and other necessary tools.

-   Open the Git Bash app.
-   Type the following commands:
````markdown
cd C:/android/cmdline-tools/tools/bin

./sdkmanager.bat "build-tools;25.0.3"  "emulator"  "extras;intel;Hardware_Accelerated_Execution_Manager"  "platforms;android-25"  "platform-tools"  "system-images;android-25;google_apis;x86" --verbose

./avdmanager.bat -v create avd -n x86 -k "system-images;android-25;google_apis;x86" -g "google_apis"
````

Make sure to accept the license agreement. Once these commands have completed, your android folder should contain a whole bunch of new directories, including:

-   **build-tools** - these are the tools used by Cordova to build your Android app.
-   **emulator** - this is the Android emulator that will be used later to preview the app on your computer.
-   **platforms** - this is the Android SDK, separated by platform version. These correspond to the releases of Android: Nougat, Marshmallow, etc. The command above has downloaded the most recent platform version (25).
-   **platform-tools** - more tools that are used to administer Android devices on the command line.
-   **system-images** - these are images used by the emulator.

### 5. Installing Gradle

Gradle is a tool that is required by the Android SDK to build Android apps. It used to be included with the Android SDK, but now it must be downloaded and configured manually.

-   Go to the [gradle releases page](https://gradle.org/releases).
-   Find the binary-only version of the latest release and select it to begin the download.
-   When the download has finished, unzip the file.
-   Rename the resulting folder to just gradle.
-   Move this gradle folder to the android folder that was created above.

### 6. Configuration

In order to make this dizzying array of tools available to Cordova, and to us when using Git Bash, we need to set some environment variables. To do this:

-   Select the Search box in the bottom left hand corner of the screen.
-   Type _environment_ then select _Edit the system environment variables_.
-   The _System Properties_ pane will appear. Select the _Environment Variables…_ button.

We need to set three environment variables in total.

1) **JAVA_HOME**

-   Under the _System variables_ section, click the _New…_ button.
-   In the _Variable Name_ box, type JAVA_HOME.
-   Select the _Browse Directory_ button. In the resulting folder browser pane, expand _This PC_ -> _WINDOWS (C:)_ -> _Program Files_ -> _Java_ and choose the folder beginning with jdk. Select OK.

-   Select _OK_ to create the environment variable.

2) **ANDROID_HOME**

-   Under the _System variables_ section, click the _New…_ button.
-   In the _Variable Name_ box, type ANDROID_HOME.
-   In the _Variable Value_ box, type C:\android.
-   Select _OK_ to create the environment variable.

3) **Path**

-   Select the Path item under the _System variables_ section and click the _Edit…_ button. You should see a pane named _Edit environment variable_.
-   Using the _New_ button, add the following four items to the list:

%ANDROID_HOME%\emulator
%ANDROID_HOME%\gradle\bin
%ANDROID_HOME%\platform-tools
%ANDROID_HOME%\tools\bin

-   Click _OK_ and then _OK_ again to close the panes.

To test that all of this has worked, try typing the following into the terminal window:

    adb version
    gradle -v

After running each command, you should see the respective tool print its version number. If any of these commands results in a **command not found**, the environment has not yet been setup correctly. Please double check that the above steps have been carried out before continuing.
### 7. Install the Cordova CLI

**Install node.js**

The Cordova CLI requires node.js. If you have already installed node, you can skip to the next section.

Otherwise:

-   Go to the [node.js download page](https://nodejs.org/en/download).
-   Click on the ‘Windows Installer’ box to download the LTS version of node for Windows.
-   When the file has downloaded, click on it to run the installer.
-   When it has finished, **close and re-open Git Bash** and type **node -v**. Node should print out its version number.

**Install Cordova**

-   In a Git Bash window, type **npm install -g cordova**. This command may take a few minutes to complete. There may be nothing printed to the window for a short while - be patient, it is working!

When this finished, you should be able to run the command **cordova -v** which should print the cordova version to the terminal.

**Create a sample app**

We’ll now create a sample app which we can deploy to the emulator and device.

Open Git Bash and change to a folder where you are happy for code to live. The commands below will generate a new cordova project in a subdirectory of whichever folder you are currently in.

For example, if you have code living in folders at **C:\Users\<username>\Code**, change to this directory before running the commands below.

Once you are in the correct directory, run the following:

    cordova create cordova-hello-world
    cd cordova-hello-world
    cordova platform add android
    cordova build


These commands will create a new cordova project, add the Android platform, and build the respective files for deployment to Android. It might take a while!

_Note_: you may need to click through to allow various programs access to restricted parts of the system, such as the firewall.

Before continuing, please ensure that the commands above all worked correctly, with no errors. If there were any errors, you’ll need to go back and check that the Android SDK was installed correctly, and that you’ve set the environment variables correctly.

**How create new project:**

In the command propmt go to the directory where the source files will be: (is empty now)
C:\XXXXXXX\my-new-project\

**cordova create my-new-project** <-this will create directory structure

Copy the source files to this directory

Update icons – logo.png

    cd my-new-project
    cordova platform add android
    cordova build

Get apk

**C:\XXXXXXX\my-new-project\platforms\android\app\build\outputs\apk\debug\app-debug.apk**

Open **APK Icon Editor** and replace icons and app if needed
Open **APK Editor Studio** and replace remaining logos
