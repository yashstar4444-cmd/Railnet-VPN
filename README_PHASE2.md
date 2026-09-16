# RailNet VPN - Phase 2 OpenVPN-ready project

## What is included

- Username/password screen
- Separate 6-digit OTP field
- Authentication flow from the existing Phase-1 API
- Android `VpnService` declaration
- Android VPN permission request
- A dedicated `RailNetVpnService` integration point

## Important

This project does **not** fake a successful VPN connection.

The uploaded OpenVPN profile uses a separate static OTP challenge. The production tunnel still needs an OpenVPN client core (OpenVPN 3 or another compatible Android OpenVPN core) connected to `RailNetVpnService`.

OpenVPN 3 is an official OpenVPN client library and exposes Android/Java bindings; Android's VPN layer is based on `VpnService`.

## Current environment limitation

The supplied build environment does not contain the Android SDK, Gradle wrapper/toolchain, or Android NDK, so a production APK cannot honestly be compiled here.

## Next build step on the Windows PC

1. Open this project in Android Studio.
2. Install Android SDK 35 and Android NDK through SDK Manager.
3. Add the OpenVPN core source/native libraries.
4. Bind the OpenVPN core's tunnel callbacks to `RailNetVpnService`.
5. Feed username, password and the separate static OTP challenge into the OpenVPN core.
6. Test against the supplied pfSense profile.
7. Build a signed release APK.

Do not put the real `.ovpn` profile or its embedded TLS material into a public repository. Anyone who obtains an APK can potentially extract packaged assets.
