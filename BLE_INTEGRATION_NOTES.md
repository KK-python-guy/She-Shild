# SheShield BLE integration — Phase 1

This project now includes foreground BLE scanning/connection for the ESP32-C3 peripheral named `SheShield`.

## BLE protocol expected from ESP32
- Advertised device name: `SheShield`
- Service UUID: `12345678-1234-1234-1234-1234567890ab`
- Characteristic UUID: `abcdefab-1234-1234-1234-abcdefabcdef`
- Characteristic properties: READ + NOTIFY
- Notification payload: UTF-8 text `SOS`

## Run on Android
1. Keep the ESP32 powered and advertising.
2. From the project directory run `flutter pub get`.
3. Run `flutter run` on a physical Android phone (BLE is not available in a typical emulator).
4. Grant Nearby devices/Bluetooth permission when Android asks.
5. Tap **Connect** in the Safety band card.
6. When the status says `Connected · Listening for SOS`, press the wearable button.

## Current safety limitations (important)
- This phase listens while the Flutter app is open/active. It is not yet a guaranteed background or terminated-app listener.
- On receiving `SOS`, the app obtains location and opens the SMS composer addressed to the first saved emergency contact. The user must review and tap Send. The app does not silently send SMS.
- Android/iOS background BLE, local emergency notifications, robust reconnection, and verified delivery are separate phases and require physical-device testing.
- Do not rely on this prototype as an emergency service until all background, permissions, delivery, battery, and network-failure cases have been tested.
