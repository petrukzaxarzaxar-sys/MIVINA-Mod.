# MIVINA-Mod.

name: Build Mivina_Mod APK

on:
  workflow_dispatch:
  push:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Get source code
        uses: actions/checkout@v4

      - name: Set up Java
        uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: '17'

      - name: Build APK
        uses: android-actions/setup-android@v3

      - name: Assemble APK
        run: |
          chmod +x gradlew 2>/dev/null || true
          gradle --no-daemon assembleDebug

      - name: Save APK
        uses: actions/upload-artifact@v4
        with:
          name: Mivina_Mod-APK
          path: app/build/outputs/apk/debug/*.apk
          
