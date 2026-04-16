---
title: Lesson 4: App Source Files
parent: Week 1: Setup
grand_parent: Part 1: Foundation
nav_order: 4
---

# Lesson 4: App Source Files

This lesson continues Track B from Lesson 3.
You will add the app source files and run the app.

#### Section 2: App Source Files

In VS Code, create these app files next.

#### File: `app/src/main/AndroidManifest.xml`

```xml
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
```

#### File: `app/src/main/java/com/example/bitcoinwallet/MainActivity.java`

```java
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
```

#### File: `app/src/main/res/layout/activity_main.xml`

```xml
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

### What success looks like (Track B)
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

[Back: Lesson 3 (Gradle Files)](lesson-3-basic-project-setup/){: .btn }
[Next: Week 1 Quiz](quiz/){: .btn .btn-primary }
