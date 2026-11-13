📱 Build Android Apps on Your Phone — Termux + OpenCode
No laptop needed. Build Android apps using only your phone: Let OpenCode (AI) write the code and build the APK directly on your phone.

One script, Termux only — no Ubuntu required.

Requirements: Android 7+, a phone with 6 GB+ RAM, approximately 4 GB of free storage, and WiFi (~1 GB download).

Step 0: Install Termux
⚠️ Do not download the Play Store version — it is outdated!
Download Termux here 👇

Download Termux

Install the Code Editor

Download Code Editor

Step 1: Run the Setup Script
Open Termux and run these two commands:


bash
curl -LO https://raw.githubusercontent.com/HunterisLive-1/Turmux-setup/main/hunter.sh

bash
bash hunter.sh
It will ask for a name → This name will appear in your terminal banner (e.g., Hunter).
A storage permission popup will appear → Tap Allow.
Time required: Approximately 10–15 minutes. No additional questions will appear during the process.
If something fails, the script will display the name of the failed component. Simply run bash hunter.sh again. Already completed steps will be skipped.
What does it install?

Component	Purpose
OpenCode (+ glibc-runner)	To write code using AI (including free models)
Java 17 + Gradle	To build APK files
Android SDK 35	Android development libraries
aapt2, apksigner (phone-compatible versions)	Standard Google versions do not work on phones
zsh + p10k + rainbow banner	A beautiful terminal appearance
At the end, a test app will be created:

Download/hello-hunter.apk

Open it using your Files app and install it.

The screen will display:

"This app was built directly on a phone!"

After everything is complete, close Termux and reopen it.

Step 2: Create an App Using OpenCode
Open the test project in Termux:


bash
cd ~/hello-hunter
Start OpenCode:


bash
opencode
The first time you launch it, type /models and select a free model (for example, a model ending in -free, such as deepseek-v4.1-flash-free).

No API key is required for these free models.

If you want to use your own API key, run opencode auth login outside OpenCode.

Now tell OpenCode what kind of app you want to create. For example:


Create a simple calculator app in this project. Only modify MainActivity.kt. Do not add any new libraries.
Step 3: Build and Install the APK
Exit OpenCode and run:


bash
./gradlew assembleDebug
Copy the generated APK to your Downloads folder:


bash
cp app/build/outputs/apk/debug/app-debug.apk /sdcard/Download/
Open your Files app → Download → app-debug.apk → Install.

Creating a New Project?
To add a gradlew wrapper to a new project, run:


bash
addwrapper
Setup for Building APKs Only (Without zsh / OpenCode)
If you only need Java + Android SDK (for example, to build apps using Maya), you can use this single command.

It will run without asking any questions:


bash
curl -sL https://raw.githubusercontent.com/HunterisLive-1/Turmux-setup/main/android-setup.sh | bash
If you see ANDROID_SETUP_OK at the end, your setup is ready.

🎨 Customize the Terminal Appearance
The script installs The Hunter AI's p10k terminal theme.

Want to change its appearance? Run:


bash
p10k configure
Choose your preferred terminal style.

⚡ Useful Aliases

Alias	Function
c	Clear the terminal screen
update	Update everything
coding	Open the /sdcard/coding folder
addwrapper	Add gradlew to a project
🔧 Troubleshooting
❌ Long yellow "instant prompt" warning when opening Termux
The latest hunter.sh script automatically disables this warning.

If you have an older setup, run:


bash
echo 'typeset -g POWERLEVEL9K_INSTANT_PROMPT=off' >> ~/.zshrc
Then close Termux and reopen it.

❌ "File has unexpected size ... Mirror sync in progress?" error during pkg update
The hunter.sh script automatically configures the default mirror.

To configure it manually:


bash
termux-change-repo
Select Single mirror → Choose default.

❌ Gradle: "AAPT2 ... Daemon startup failed"
Gradle downloads the PC version of aapt2, which does not work on phones.

Check the configuration:


bash
cat ~/.gradle/gradle.properties
It should contain the following line:


properties
android.aapt2FromMavenOverride=
If the line is missing, run bash hunter.sh again.

❌ ./gradlew: No such file or directory
Your project does not have a gradlew file.

Run this command inside your project folder:


bash
addwrapper
❌ Build is very slow / Phone gets hot
A first build taking 3–5 minutes is normal because all the required files are being downloaded.

Keep other apps closed while building.

A phone with 6 GB+ RAM is recommended for better performance.

❌ P10k icons are not displaying correctly
Close Termux and reopen it (the font needs to load).

If the problem persists, run:


bash
p10k configure
When asked about icons, select No.

Note: I have preserved your original technical instructions and code without changing them. The translation is language-only; I have not independently verified whether the setup script or its downloads are safe or currently working.
