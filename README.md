# factz-hello-world-

A safe Android media showcase app created with Kotlin and Jetpack Compose.

## Features
- Modern Material 3 UI
- Trending and category-based media cards
- Clean, responsive layout for phone screens
- Ready to open in Android Studio

## Run it
1. Open the project in Android Studio.
2. Let Gradle sync.
3. Run the app on an emulator or physical device.

This starter app is intentionally designed as a clean demo app and does not include explicit or inappropriate content.

workflows:
  android-debug:
    name: Android Debug APK
    max_build_duration: 60
    instance_type: linux_x2

    environment:
      java: 17

    scripts:
      - name: Set Android SDK location
        script: |
          echo "sdk.dir=$ANDROID_SDK_ROOT" > local.properties

      - name: Download Gradle
        script: |
          curl --fail --location --retry 3 \
            https://services.gradle.org/distributions/gradle-8.7-bin.zip \
            --output /tmp/gradle.zip
          unzip -q /tmp/gradle.zip -d /tmp
          /tmp/gradle-8.7/bin/gradle --version

      - name: Build debug APK
        script: |
          /tmp/gradle-8.7/bin/gradle --no-daemon assembleDebug

    artifacts:
      - app/build/outputs/**/*.apk
