---
title: Lesson 3: Basic Project Setup
parent: Week 1: Setup
grand_parent: Part 1: Foundation
nav_order: 3
---

# Lesson 3: Basic Project Setup

This lesson creates your first empty Android app in Android Studio.

## What you will do
- Install Android Studio if needed.
- Create a new Empty Activity project.
- Run the app on a device or emulator.

## GUI steps (Android Studio)
1. Open Android Studio.
2. Click "New Project."
3. Choose the "Empty Activity" template.
4. Set the project name and location.
5. Keep the language as Java (see note below about Java vs Kotlin).
6. Keep the minimum SDK at the default.
7. Click "Finish."
8. Wait for Gradle sync to finish.
9. Select a device or emulator from the device dropdown.
10. Click "Run" and wait for the app to launch.

### Why Java for this course?

This course uses Java because many production Bitcoin wallets still use Java or a Java/Kotlin mix. The choice depends on your goals:

**For Android fundamentals and modern job market alignment:** Start with Kotlin. It is the dominant choice in newer native wallets (Phoenix, Unstoppable, Nunchuk, Green) and aligns with current Android patterns (coroutines, modern dependency injection, Compose, etc.).

**For conceptual clarity and "least magic" for beginners:** Java remains a defensible starting point. It is explicit, widely understood, and interoperates perfectly with Kotlin later. Many real Bitcoin wallets still carry substantial Java code (Muun, Mycelium), and Java fundamentals map cleanly to Kotlin concepts.

**For building cross-platform wallets quickly:** The industry often chooses cross-platform frameworks (React Native / TypeScript) or shared-core architectures (Kotlin Multiplatform, Rust, C) to avoid duplicating security logic. In this model, Android language choice becomes more about the UI shell than wallet correctness.

| Project | Repo | GitHub language breakdown (percent of repo) |
| --- | --- | --- |
| Muun | [https://github.com/muun/apollo](https://github.com/muun/apollo) | Java **32.1%**, Kotlin **31.6%**, Go **21.4%**, Rust **14.7%**, Shell **0.1%**, Dockerfile **0.1%** |
| Mycelium | [https://github.com/mycelium-com/wallet-android](https://github.com/mycelium-com/wallet-android) | Kotlin **50.8%**, Java **49.0%**, Other **0.2%** |
| BitBanana | [https://github.com/michaelWuensch/BitBanana](https://github.com/michaelWuensch/BitBanana) | Java **99.0%**, Other **1.0%** |
| Phoenix (ACINQ) | [https://github.com/ACINQ/phoenix](https://github.com/ACINQ/phoenix) | Kotlin **53.5%**, Swift **46.2%**, Other **0.3%** |
| AirGap Vault | [https://github.com/airgap-it/airgap-vault](https://github.com/airgap-it/airgap-vault) | TypeScript **89.3%**, Kotlin **4.1%**, Swift **3.6%**, Java **1.7%**, HTML **0.4%**, Other **0.9%** |
| Unstoppable Wallet (Android) | [https://github.com/horizontalsystems/unstoppable-wallet-android](https://github.com/horizontalsystems/unstoppable-wallet-android) | Kotlin **100.0%** |
| Bitkey | [https://github.com/proto-at-block/bitkey](https://github.com/proto-at-block/bitkey) | Kotlin **41.5%**, C **38.0%**, Rust **14.9%**, HCL **1.5%**, Python **1.3%**, Swift **1.0%**, Other **1.8%** |
| Zeus | [https://github.com/ZeusLN/zeus](https://github.com/ZeusLN/zeus) | TypeScript **96.0%**, JavaScript **2.5%**, Kotlin **0.8%**, Swift **0.4%**, Java **0.2%**, Objective-C **0.1%** |
| Nunchuk (Android) | [https://github.com/nunchuk-io/nunchuk-android](https://github.com/nunchuk-io/nunchuk-android) | Kotlin **99.9%**, Other **0.1%** |
| Blockstream Green (Android) | [https://github.com/Blockstream/green_android](https://github.com/Blockstream/green_android) | Kotlin **94.7%**, Java **4.6%**, Other **0.7%** |
| Edge (React GUI) | [https://github.com/EdgeApp/edge-react-gui](https://github.com/EdgeApp/edge-react-gui) | TypeScript **84.5%**, JavaScript **13.5%**, HTML **2.0%** |

#### Reproducibility and language choice

For Bitcoin wallets, reproducibility (or at least deterministic, auditable builds) is often more important than the Java vs Kotlin debate.

**What language choice affects (and what it does not):**

Java vs Kotlin generally does not determine reproducibility by itself. Both compile to JVM bytecode and are packaged by the same Android toolchain (Gradle + Android Gradle Plugin + D8/R8).

Language can influence build determinism indirectly through:
- Dependency ecosystem choices (common Kotlin libraries vs older Java libs).
- Build plugins (KSP/KAPT, Compose tooling).
- Generated code paths and annotation processing.

**What matters more for reproducible Android builds:**

Regardless of language, reproducibility improves when you:
- Pin toolchains (Gradle wrapper, Android Gradle Plugin, JDK version, NDK if used).
- Pin dependencies (lockfiles / version catalogs, avoid dynamic versions, avoid "latest").
- Avoid nondeterministic build inputs (timestamps embedded in assets, build IDs, unstable codegen).
- Use a consistent environment (containerized builds, documented SDK packages, deterministic CI).

**Practical guidance for this course:**

This course will eventually teach "wallets you can verify." We frame language as a UI implementation detail, and reproducibility as a discipline: "We can write UI in Java or Kotlin; correctness and reproducibility come from pinned toolchains and a verifiable build pipeline."

## If something fails
- Check that the Android SDK is installed.
- Check that your emulator or device is connected.
- Check that a device is selected in the toolbar.

## What success looks like (GUI)
You see the app on the selected device.
The screen shows the default "Hello World" text.
The Run tool window shows "BUILD SUCCESSFUL."
The app appears in the device app list.

## CLI steps (Optional)
These steps mirror the Android Studio flow.  
They use only the terminal.  

## CLI tools you need
Install the Android SDK command line tools first.  
Use the official setup guide: [Android command line tools](https://developer.android.com/studio#command-tools).  
Pick the "Command line tools only" package for your OS.  
On Linux, unzip into `~/Android/Sdk/cmdline-tools/latest/`.  
On Windows, unzip into `%LOCALAPPDATA%\Android\Sdk\cmdline-tools\latest\`.  
The Linux zip name looks like `commandlinetools-linux-*_latest.zip`.  

### Recommended packages
Install the latest stable versions.  
Use the newest build tools, platform, and emulator.  
Example versions are shown below.  

Required:
- Command line tools (latest).  
- Platform Tools (latest).  
- Emulator (latest).  
- Build Tools (example: 34.0.0).  
- Android platform (example: Android 14 / API 34).  
- System image (example: Android 14, Google APIs, x86_64).  

Optional:
- Sources for the Android platform (for docs and source).  

`sdkmanager` installs SDK platforms and system images.  
It also manages licenses for SDK packages.  

`avdmanager` creates and manages emulator devices.  
It is included with the command line tools.  

`emulator` runs a virtual Android device.  
It comes from the Android Emulator package.  

`adb` connects your computer to devices.  
It installs and launches your app.  

### Example commands (Linux)
Adjust paths and versions to match the latest packages.  

```bash
export ANDROID_HOME="$HOME/Android/Sdk"
export PATH="$ANDROID_HOME/cmdline-tools/latest/bin:$ANDROID_HOME/platform-tools:$ANDROID_HOME/emulator:$PATH"
export ANDROID_AVD_HOME="$HOME/.config/.android/avd"

sdkmanager --install "platform-tools" "emulator"
sdkmanager --install "platforms;android-34" "build-tools;34.0.0"
sdkmanager --install "system-images;android-34;google_apis;x86_64"
sdkmanager --licenses
```

### Troubleshooting: sdkmanager not found
This means the command line tools are not installed.  
Download the "Command line tools only" package for Linux.  
Unzip into `~/Android/Sdk/cmdline-tools/latest/`.  
Confirm `~/Android/Sdk/cmdline-tools/latest/bin/sdkmanager` exists.  
Re-run your `export` commands.  
Then run `sdkmanager --version`.  

### Troubleshooting: unzip path errors
Use `-d` to set the output folder.  
Make sure the folder exists first.  

```bash
mkdir -p ~/Android/Sdk/cmdline-tools/latest
unzip commandlinetools-linux-13114758_latest.zip -d ~/Android/Sdk/cmdline-tools/latest
```

If you see a nested `cmdline-tools` folder, move its contents up.  

```bash
mv ~/Android/Sdk/cmdline-tools/latest/cmdline-tools/* ~/Android/Sdk/cmdline-tools/latest/
rmdir ~/Android/Sdk/cmdline-tools/latest/cmdline-tools
```

### 1) Install tools and set paths
Set your SDK path.  
Then install the tools and a system image.  

```bash
export ANDROID_HOME="$HOME/Android/Sdk"
export PATH="$ANDROID_HOME/cmdline-tools/latest/bin:$ANDROID_HOME/platform-tools:$ANDROID_HOME/emulator:$PATH"
sdkmanager --install "platform-tools" "platforms;android-34" "build-tools;34.0.0" "emulator" "system-images;android-34;google_apis;x86_64"
sdkmanager --licenses
```

### 2) Create and start an emulator
Create an AVD.  
Then start it.  

```bash
avdmanager create avd -n wallet_api_34 -k "system-images;android-34;google_apis;x86_64"
emulator -avd wallet_api_34 -no-snapshot
```

> Tip: A successful run shows the emulator window with the Android UI shortly after the command starts.  
> If it does not, check system virtualization, emulator config, ADB/device connection, and graphics backend.  
> Read the emulator logs and focus on the first error line.  
> Apply one change at a time, then rerun.  
{: .note }

### Troubleshooting: AVD not found
List AVDs to confirm the name.  
Use `emulator -list-avds` or `avdmanager list avd`.  
If the list is empty, create the AVD again.  
If the AVD path is not under `~/.android/avd`, set `ANDROID_AVD_HOME`.  

```bash
export ANDROID_AVD_HOME="$HOME/.config/.android/avd"
```

### Troubleshooting: /dev/kvm is not found
This means hardware acceleration is off.  
Enable VT in BIOS.  
Install and load KVM on Linux.  
See: https://developer.android.com/studio/run/emulator-acceleration#vm-linux  

### 3) Confirm the device
Check that the device is listed.  

```bash
adb devices
```

### 4) Create a minimal project
Make the folders.
Then create the Gradle and app files.

> Note: The versions shown below are current as of January 2026. For the latest versions, check:
> - Android Gradle Plugin: [developer.android.com/build/releases/gradle-plugin](https://developer.android.com/build/releases/gradle-plugin)
> - AndroidX AppCompat: [developer.android.com/jetpack/androidx/releases/appcompat](https://developer.android.com/jetpack/androidx/releases/appcompat)
> - Material Components: [github.com/material-components/material-components-android/releases](https://github.com/material-components/material-components-android/releases)
{: .note }  

```bash
mkdir -p bitcoin-wallet/app/src/main/java/com/example/bitcoinwallet
mkdir -p bitcoin-wallet/app/src/main/res/layout
cd bitcoin-wallet
cat > settings.gradle <<'EOF'
pluginManagement {
    repositories {
        google()
        mavenCentral()
        gradlePluginPortal()
    }
}
dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        google()
        mavenCentral()
    }
}
rootProject.name = "bitcoin-wallet"
include(":app")
EOF
cat > build.gradle <<'EOF'
plugins {
    id "com.android.application" version "8.13.2" apply false
}
EOF
cat > app/build.gradle <<'EOF'
plugins {
    id "com.android.application"
}

android {
    namespace "com.example.bitcoinwallet"
    compileSdk 34

    defaultConfig {
        applicationId "com.example.bitcoinwallet"
        minSdk 24
        targetSdk 34
        versionCode 1
        versionName "1.0"
    }

    buildTypes {
        release {
            minifyEnabled false
        }
    }
}

dependencies {
    implementation "androidx.appcompat:appcompat:1.7.1"
    implementation "com.google.android.material:material:1.14.0"
}
EOF
cat > app/src/main/AndroidManifest.xml <<'EOF'
<manifest package="com.example.bitcoinwallet" xmlns:android="http://schemas.android.com/apk/res/android">
    <application
        android:label="Bitcoin Wallet"
        android:theme="@style/Theme.AppCompat.Light.NoActionBar">
        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
</manifest>
EOF
cat > app/src/main/java/com/example/bitcoinwallet/MainActivity.java <<'EOF'
package com.example.bitcoinwallet;

import android.os.Bundle;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}
EOF
cat > app/src/main/res/layout/activity_main.xml <<'EOF'
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:padding="24dp">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello from the CLI." />
</FrameLayout>
EOF
```

### 5) Build and run
Create the Gradle wrapper.  
Build the app.  
Install it on the emulator.  

```bash
gradle wrapper
./gradlew assembleDebug
adb install -r app/build/outputs/apk/debug/app-debug.apk
adb shell am start -n com.example.bitcoinwallet/.MainActivity
```

If you already use Android Studio, you can skip this.  

### What success looks like (CLI)
Gradle prints `BUILD SUCCESSFUL`.  
`adb install` prints `Success`.  
The emulator opens the app.  
You see the "Hello from the CLI." message.  
The app appears in the launcher list.  

### Expected folder layout
The user's project folder should look like this.  

```
bitcoin-wallet/
├── build.gradle
├── settings.gradle
├── gradle/
│   └── wrapper/
│       ├── gradle-wrapper.jar
│       └── gradle-wrapper.properties
├── gradlew
├── gradlew.bat
└── app/
    ├── build.gradle
    ├── build/
    │   └── outputs/
    │       └── apk/
    │           └── debug/
    │               └── app-debug.apk
    └── src/
        └── main/
            ├── AndroidManifest.xml
            ├── java/
            │   └── com/
            │       └── example/
            │           └── bitcoinwallet/
            │               └── MainActivity.java
            └── res/
                └── layout/
                    └── activity_main.xml
```

[Next: Week 1 Quiz](quiz/){: .btn .btn-primary }
