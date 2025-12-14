# vibe-player
name: Build VibePlayer APK

on:
  push:
    branches: [ "main" ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout project
      uses: actions/checkout@v4

    - name: Setup JDK 17
      uses: actions/setup-java@v4
      with:
        distribution: 'temurin'
        java-version: '17'

    - name: Grant execute permission
      run: chmod +x ./gradlew

    - name: Build Release APK
      run: ./gradlew assembleRelease

    - name: Upload APK
      uses: actions/upload-artifact@v4
      with:
        name: VibePlayer-APK
        path: app/build/outputs/apk/release/*.apk
