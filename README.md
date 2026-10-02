# Xport Studio

Xport Studio is a private desktop app for musicians for voice conversion, stems, mastering, and live key and BPM, and it processes audio on your machine.

## Download

- [xportstudio.com](https://xportstudio.com)
- [Latest release on GitHub](https://github.com/xportstudio/xport-studio/releases/latest)

## Requirements

macOS 15 (Sequoia) or later on Apple Silicon, or Windows 10 or later.

- The Mac build is for Apple Silicon (arm64) only. macOS 14 and older are not supported.
- Current builds: Mac v2.0.0-alpha.42 and Windows v2.0.0-alpha.41. Windows stays on alpha.41 until the Windows alpha.42 build ships, so Listen Live, Voice Blender, and Studio Voice are on Mac only for now.
- Voice conversion and cloning need the voice pack (about 4.7 GB), downloaded once.

## Free vs Pro

**Listen Live (Mac, free)** is the live BPM and key reader, part of Key & BPM Finder. Pick a microphone or audio input under "Listening on", play music, and the key and BPM show up live. It locks in after about 8 seconds.

### Free forever

- Split Stems
- Key & BPM Finder, including Listen Live on Mac
- Noise Remover
- Mix & Master (beta). Classic audio processing: Pedalboard effect chains plus Matchering reference matching. It is not an AI model.
- Audio Converter
- Trimmer
- Library

### Pro: $79, one time, no subscription

These tools come with a 7-day free trial. After the trial they need Pro.

- AI voice conversion (Create)
- Text to Speech
- Train Clone
- Voice Blender (Mac, in Library): blends two voice models of the same RVC generation (v1 with v1, v2 with v2) into a new voice. The compatibility check is free; blending needs Pro after the trial.
- Studio Voice (Mac)

Founding is $399, only 100, and includes everything in Pro plus founding perks.

## Privacy and network use

### Optional telemetry (off by default)

The app asks once on first launch. Saying yes turns on both channels below. You can change either one any time in Settings, Privacy. Neither channel sends audio or projects.

1. **Usage ping**, once per launch: app version, OS, CPU type, language, trial days left, and a random install ID. Our server keeps a hashed copy of the IP address.
2. **Crash reporting through Sentry**: when something breaks, a stack trace and device details (app version, OS, CPU and GPU), plus a record of each app session.

### Other network use by the app

- **Updates and packs**: the app checks for and downloads updates and packs from GitHub, with downloads delivered through a Cloudflare worker.
- **License activation**: sends your license key to Lemon Squeezy's license API to confirm the purchase.
- **First-time downloads**: AI models and packages are downloaded the first time a tool needs them (public hosts such as Hugging Face, GitHub, the Python Package Index, and download.pytorch.org).
- **Feedback (optional)**: in-app feedback sends your message, app version, platform, and an optional email to our feedback server on Cloudflare.

### Listen Live and the microphone

The microphone is on only while Listen Live runs. Short audio windows are written briefly to a temporary file on your computer, analyzed there, and deleted. Nothing is uploaded or kept.

### Offline use

After the one-time downloads (the app, the packs, and the model each tool fetches the first time), the tools run offline.

### Website (xportstudio.com)

- **GoatCounter**: cookieless page analytics.
- **Kit**: email addresses entered in the download form.
- **FormSubmit.co**: the feedback and affiliate forms are emailed through FormSubmit. The affiliate form also subscribes you to Kit.
- **Google Fonts**: font files load from Google.
- **Vercel**: hosting.
- **Lemon Squeezy**: checkout.
- **Download worker (Cloudflare)**: logs each download click with country, browser user agent, referrer, and a daily-salted IP hash.

## Open-source software

Xport Studio includes open-source software components. Each component is licensed to you under its own license, not under the Xport Studio EULA or Terms of Service.

Nothing in our EULA or Terms limits the rights those licenses give you, including the right to study, modify, and redistribute those components. Where our EULA or Terms conflict with a component's license, that license controls for that component. Our restrictions on reverse engineering do not apply to the extent those licenses permit it. For components under the GNU Lesser General Public License, that includes modifying the component for your own use and reverse engineering to debug those modifications.

The tables below list the components whose licenses require us to offer source code. The versions are the ones in Xport Studio 2.0.0-alpha.42 for Mac, checked against the installed app on October 2, 2026. Other versions of the app, including the Windows version, may include different versions of these components. The written offer below covers every version we distribute, on every platform.

### Desktop app

| Component | Version | License | Source |
|---|---|---|---|
| pedalboard (includes JUCE, VST3 SDK, Rubber Band, FFTW, LAME, libgsm) | 0.9.23 | GPL-3.0 | [spotify/pedalboard at v0.9.23](https://github.com/spotify/pedalboard/tree/v0.9.23) (clone with `--recursive` to get the bundled libraries) |
| matchering | 2.0.6 | GPL-3.0 | [matchering-2.0.6.tar.gz](https://files.pythonhosted.org/packages/13/a2/8dd0e1f3da3a6f4d50d1f06f91117370844edb9e8cce1ff798a7cdc0cece/matchering-2.0.6.tar.gz) |
| phonemizer-fork | 3.3.2 | GPL-3.0-or-later | [phonemizer_fork-3.3.2.tar.gz](https://files.pythonhosted.org/packages/42/fa/9294d2f11890ca49d0bdac7a4da60cbe5686629bfd4987cae0ad75e051cc/phonemizer_fork-3.3.2.tar.gz) |
| eSpeak NG (packaged by espeakng-loader 0.2.4) | 1.52.0 | GPL-3.0-or-later | [espeak-ng 1.52.0](https://github.com/espeak-ng/espeak-ng/archive/refs/tags/1.52.0.tar.gz) |
| FFmpeg program (from imageio-ffmpeg 0.6.0, built with x264, x265 and other libraries) | 7.1 | GPL-2.0-or-later | [ffmpeg-7.1.tar.xz](https://ffmpeg.org/releases/ffmpeg-7.1.tar.xz). Sources for the built-in libraries: on request |
| TempoCNN deeptemp_k16 model. Modified by Xport: converted from Keras to ONNX format (in our code since May 2026) | deeptemp_k16 | AGPL-3.0 | Original model and code: [tempo-cnn v0.0.8](https://github.com/hendriks73/tempo-cnn/archive/refs/tags/v0.0.8.tar.gz). Our converted file: on request |
| PyInstaller bootloader | 6.20.0 | GPL-2.0-or-later with the bootloader exception | [pyinstaller-6.20.0.tar.gz](https://files.pythonhosted.org/packages/46/60/d03d52e6690d4e9caf333dcd14550cde634ce6c118b3bc8fa3112c3186fd/pyinstaller-6.20.0.tar.gz) |
| GCC runtime: libgfortran, libgcc_s (from the SciPy 1.13.0 wheel) | as built for SciPy 1.13.0 | GPL-3.0 with the GCC Runtime Library Exception | [GCC libgfortran source](https://gcc.gnu.org/git/?p=gcc.git;a=tree;f=libgfortran) |
| python-soxr (includes libsoxr) | 1.1.0 | LGPL-2.1-or-later | [soxr-1.1.0.tar.gz](https://files.pythonhosted.org/packages/ed/11/27cebce4a108f77afea7c80545115536b45e3f11ebfb914f638fdd9ba847/soxr-1.1.0.tar.gz) |
| libsndfile (via soundfile 0.13.1) | 1.2.2 | LGPL-2.1-or-later | [libsndfile-1.2.2.tar.xz](https://github.com/libsndfile/libsndfile/releases/download/1.2.2/libsndfile-1.2.2.tar.xz) |
| lameenc (includes LAME 3.100) | 1.8.2 | LGPL-3.0-or-later | [lameenc v1.8.2](https://github.com/chrisstaite/lameenc/archive/refs/tags/v1.8.2.tar.gz) and [LAME 3.100](https://sourceforge.net/projects/lame/files/lame/3.100/lame-3.100.tar.gz/download) |
| libquadmath (from the SciPy 1.13.0 wheel) | as built for SciPy 1.13.0 | LGPL-2.1-or-later | [GCC libquadmath source](https://gcc.gnu.org/git/?p=gcc.git;a=tree;f=libquadmath) |
| FFmpeg libraries inside Electron (Chromium build N-116067-gfecf1c679a) | Electron 31.7.7 | LGPL-2.1-or-later | [Chromium FFmpeg at fecf1c679a](https://chromium.googlesource.com/chromium/third_party/ffmpeg/+/fecf1c679a) |
| certifi | 2026.5.20 | MPL-2.0 | [certifi-2026.5.20.tar.gz](https://files.pythonhosted.org/packages/f3/ce/ee2ecad540810a79593028e88299baeae54d346cc7a0d94b6199988b89b1/certifi-2026.5.20.tar.gz) |
| tqdm | 4.67.3 | MPL-2.0 and MIT | [tqdm-4.67.3.tar.gz](https://files.pythonhosted.org/packages/09/a9/6ba95a270c6f1fbcd8dac228323f2777d886cb206987444e4bce66338dd4/tqdm-4.67.3.tar.gz) |
| orjson | 3.11.9 | MPL-2.0 and (Apache-2.0 or MIT) | [orjson-3.11.9.tar.gz](https://files.pythonhosted.org/packages/7e/0c/964746fcafbd16f8ff53219ad9f6b412b34f345c75f384ad434ceaadb538/orjson-3.11.9.tar.gz) |

### Free browser tools on xportstudio.com

| Component | Version | License | Source |
|---|---|---|---|
| essentia.js (its WebAssembly file includes the Essentia C++ library) | 0.1.3 | AGPL-3.0 | [essentia.js v0.1.3](https://github.com/MTG/essentia.js/archive/refs/tags/v0.1.3.tar.gz) and [Essentia](https://github.com/MTG/essentia) |
| ffmpeg.wasm core (FFmpeg 5.1.4, built with x264, x265 and other libraries) | 0.12.6 | GPL-2.0-or-later | [ffmpeg.wasm source for this build](https://github.com/ffmpegwasm/ffmpeg.wasm/archive/e0d4c62a229ba58ea0c6e6b881e289f2fefe97c4.tar.gz) |
| SoundTouchJS | 0.3.0 | LGPL-2.1 | [SoundTouchJS v0.3.0](https://github.com/cutterbl/SoundTouchJS/archive/refs/tags/v0.3.0.tar.gz) |

Our own code for the free tools is licensed under AGPL-3.0. License text: [xportstudio.com/freetools/LICENSE](https://xportstudio.com/freetools/LICENSE).

### Written offer for source code

For at least three years after we last distribute a version of Xport Studio that contains a component listed above, we will provide the complete corresponding source code for that component, for that version, to anyone who asks, at no charge. For the free browser tools, the same offer runs for at least three years after we last serve a component on xportstudio.com.

To ask, email [support@xportstudio.com](mailto:support@xportstudio.com) with your app version (or the tool's page) and the component you want.

### License texts

[GPL-3.0](https://www.gnu.org/licenses/gpl-3.0.html) · [GPL-2.0](https://www.gnu.org/licenses/old-licenses/gpl-2.0.html) · [AGPL-3.0](https://www.gnu.org/licenses/agpl-3.0.html) · [LGPL-3.0](https://www.gnu.org/licenses/lgpl-3.0.html) · [LGPL-2.1](https://www.gnu.org/licenses/old-licenses/lgpl-2.1.html) · [GCC Runtime Library Exception](https://www.gnu.org/licenses/gcc-exception-3.1.html) · [MPL-2.0](https://www.mozilla.org/en-US/MPL/2.0/)

## Support

Email [support@xportstudio.com](mailto:support@xportstudio.com) or visit [xportstudio.com/support](https://xportstudio.com/support).
