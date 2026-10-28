# futigo-lgpl-fribidi

Complete corresponding source code of **GNU FriBidi** as shipped inside the **Futigo** mobile app (iOS and Android), starting with app version 2.0.0.

License: **LGPL-2.1-or-later**.

GNU FriBidi is under the GNU LGPL version 2.1 or later.

This repository contains only unmodified upstream source code, the media-kit build scripts (no patches are applied to FriBidi), and the license texts. It contains no Futigo code.

## Source files

All files are attached to the GitHub release **`app-2.0.0-sources`** of this repository, together with `SHA256SUMS`.

| Component / version | Platform | License | Original source URL | Release file | SHA-256 |
|---|---|---|---|---|---|
| FriBidi 1.0.13 | iOS | LGPL-2.1-or-later | https://github.com/fribidi/fribidi/releases/download/v1.0.13/fribidi-1.0.13.tar.xz | `fribidi-1.0.13.tar.xz` | `7fa16c80c81bd622f7b198d31356da139cc318a63fc7761217af4130903f54a2` |
| FriBidi 1.0.12 (tag v1.0.12, commit 6428d8469e536bcbb6e12c7b79ba6659371c435a) | Android | LGPL-2.1-or-later | https://github.com/fribidi/fribidi/archive/refs/tags/v1.0.12.tar.gz | `fribidi-1.0.12.tar.gz` | `2e9e859876571f03567ac91e5ed3b5308791f31cda083408c2b60fa1fe00a39d` |

- `fribidi-1.0.13.tar.xz`: official release tarball; SHA-256 equals `downloads.lock` of libmpv-darwin-build v0.6.0.
- `fribidi-1.0.12.tar.gz`: the Android build clones tag `v1.0.12`; GitHub archive of that exact tag (commit id checked in the archive).

## Build scripts (how the binaries were made)

| Build repository | Platform | Original URL | Release file | SHA-256 |
|---|---|---|---|---|
| media-kit/libmpv-darwin-build, tag v0.6.0 (commit 4286f5557bdccc0747030e3c376ce5cd160a96a0) | iOS | https://github.com/media-kit/libmpv-darwin-build/archive/refs/tags/v0.6.0.tar.gz | `libmpv-darwin-build-0.6.0.tar.gz` | `afade6a15e001700c6d92860bb33eba43020450001e7464595717ab9a222d28a` |
| media-kit/libmpv-android-video-build, tag v1.1.7 (commit fe8c3ac1a91c09aa6fb1deccbc833f1bafa54768) | Android | https://github.com/media-kit/libmpv-android-video-build/archive/refs/tags/v1.1.7.tar.gz | `libmpv-android-video-build-1.1.7.tar.gz` | `6624ea32232f7a8d6d07ab7a7bc7b42c16f85fc50c4e3ecfd174b52636d9252a` |

Where it is used: text direction for subtitles, used by libass inside libmpv. iOS: separate dynamic framework. Android: linked into `libmpv.so`.

The app ships the **prebuilt media-kit binaries unchanged**:

- iOS: Flutter package `media_kit_libs_ios_video` 1.1.4, which downloads `libmpv-xcframeworks_v0.6.0_ios-universal-video-default.tar.gz` built by libmpv-darwin-build v0.6.0 (variant `video`, flavor `default`). Exact source versions and checksums are in `downloads.lock` of that build repository.
- Android: Flutter package `media_kit_libs_android_video` 1.3.8, which downloads `default-<abi>.jar` from the v1.1.7 release of libmpv-android-video-build, built by libmpv-android-video-build v1.1.7 (`buildscripts/include/depinfo.sh`, `buildscripts/include/download-deps.sh`, `buildscripts/flavors/default.sh`).

No patches: FriBidi is used unmodified.

## How to rebuild

iOS (macOS host):

```sh
tar -xzf libmpv-darwin-build-0.6.0.tar.gz
cd libmpv-darwin-build-0.6.0
brew install cmake golang meson ninja
VERSION=v0.6.0 make
# result: build/output/libmpv-xcframeworks_v0.6.0_ios-universal-video-default.tar.gz
```

The build downloads the sources listed in `downloads.lock` (the same files as in this release) and verifies their SHA-256. To build offline, place the release tarballs where the build expects its downloads.

Android (Linux host, see the build repository's own workflow):

```sh
tar -xzf libmpv-android-video-build-1.1.7.tar.gz
cd libmpv-android-video-build-1.1.7/buildscripts
./bundle_default.sh   # download.sh + patch.sh + build.sh with flavors/default.sh
```

To replace the library in the app with a modified version, rebuild it and put the resulting framework / `libmpv.so` in place of the one in the app (iOS: the dynamic framework inside `Futigo.app/Frameworks`; Android: `lib/<abi>/libmpv.so` in the APK).

## Source on request

You can also ask for a copy of this source code: **info@futigo.app**. This offer is valid for at least 3 years from the last distribution of the app version that contains the library.

## Licenses

- [`licenses/LGPL-2.1.txt`](licenses/LGPL-2.1.txt)

---

## Po polsku (skrót)

To repozytorium zawiera pełny kod źródłowy biblioteki GNU FriBidi (LGPL-2.1-or-later) w wersjach używanych w aplikacji Futigo (iOS i Android), od wersji 2.0.0: niezmienione źródła autorów i skrypty budowania media-kit (bez poprawek). Aplikacja zawiera gotowe, niezmienione pliki binarne media-kit. Pliki są w wydaniu (release) `app-2.0.0-sources`, z sumami kontrolnymi `SHA256SUMS`. Kod źródłowy można też otrzymać na prośbę: **info@futigo.app** (co najmniej 3 lata od ostatniej dystrybucji danej wersji aplikacji).
