📱 Build Android Apps on Your Phone — Termux + OpenCode
Without a laptop, using only your phone: Let OpenCode (AI) write your app and build the APK directly on your phone. One script, Termux only — no Ubuntu required.

Requirements: Android 7+, a phone with 6 GB+ RAM, ~4 GB free storage, WiFi (~1 GB download).

Step 0: Install Termux
⚠️ Do not download the Play Store version — it's outdated!
** Download Termux Here **👇 . Download Termux

** Install Code Editor ** Download Code Editor

Step 1: Run the Setup Script
Open Termux and run these two commands:


bash
curl -LO https://raw.githubusercontent.com/HunterisLive-1/Turmux-setup/main/hunter.sh

bash
bash hunter.sh
It will ask for a name → For the terminal banner (e.g., Hunter)
A storage permission popup will appear → Tap Allow
Time: ~10-15 minutes. No questions will be asked in between.
If something fails, the script will display the name of the failed component — run bash hunter.sh again, and completed steps will be skipped.
This installs:


What	Why
OpenCode (+ glibc-runner)	To write code using AI (including free models)
Java 17 + Gradle	To build APKs
Android SDK 35	Android libraries
aapt2, apksigner (phone-compatible versions)	Google's standard versions do not work on phones
zsh + p10k + rainbow banner	Beautiful terminal appearance
At the end, a test app will be created: Download/hello-hunter.apk — Open it using the Files app and install it. The screen will display: "This app was built directly on a phone!"

After everything is complete, close Termux and reopen it.

Step 2: Create an App Using OpenCode
Open the test project in Termux:


bash
cd ~/hello-hunter

bash
opencode
The first time, type /models and select a free model (with -free at the end of its name, e.g., deepseek-v4.1-flash-free) — no API key required. If you want to use your own API key, run opencode auth login outside OpenCode.

Then tell OpenCode what you want to build, for example:


Create a simple calculator app in this project. Only modify MainActivity.kt, do not add any new libraries.
Step 3: Build and Install the APK
Exit OpenCode and run:


bash
./gradlew assembleDebug

bash
cp app/build/outputs/apk/debug/app-debug.apk /sdcard/Download/
Files app → Download → app-debug.apk → Install.

New project? To add gradlew to its folder, run:


bash
addwrapper
Setup for Building APKs Only (Without zsh / OpenCode)
If you only need Java + Android SDK (for example, to build apps using Maya), this single command will do the job. It won't ask any questions:


bash
curl -sL https://raw.githubusercontent.com/HunterisLive-1/Turmux-setup/main/android-setup.sh | bash
If ANDROID_SETUP_OK appears at the end, you're ready.

🎨 Want to Change the Look?
The script installs The Hunter Ai's p10k look. Choose your own style:


bash
p10k configure
⚡ Aliases

Alias	Function
c	Clear the screen
update	Update everything
coding	Open the /sdcard/coding folder
addwrapper	Add gradlew to a project
🔧 Troubleshooting
❌ Long yellow "instant prompt" warning when opening Termux
The latest hunter.sh automatically disables it. If you have an older setup:


bash
echo 'typeset -g POWERLEVEL9K_INSTANT_PROMPT=off' >> ~/.zshrc
Then close Termux and reopen it.

❌ "File has unexpected size ... Mirror sync in progress?" during pkg update
hunter.sh automatically sets the default mirror. To do it manually:


bash
termux-change-repo
Select "Single mirror" → Choose "default".

❌ Gradle: "AAPT2 ... Daemon startup failed"
Gradle downloads the PC version of aapt2, which does not work on phones. Check:


bash
cat ~/.gradle/gradle.properties
It should contain the android.aapt2FromMavenOverride= line. If it's missing, run bash hunter.sh again.

❌ ./gradlew: No such file or directory
The project does not have gradlew. Run this inside the project folder:


bash
addwrapper
❌ Build is very slow / Phone gets hot
The first build taking 3-5 minutes is normal (everything is being downloaded). Keep other apps closed. 6 GB+ RAM is recommended.

❌ P10k icons are broken
Close Termux and reopen it (the font needs to load). If the problem persists, choose "No" for icons in:


bash
p10k configure
