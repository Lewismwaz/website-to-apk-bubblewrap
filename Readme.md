### **STEP 1: Manifest.json file**
- Before starting, verify your website (e.g., `echopitch.co.ke`) has a PWA (Progressive Web App) manifest:
1. Visit: `https://echopitch.co.ke/manifest.json`
2. If you see "Page not found" or similar, you need to create one
> [!IMPORTANT]
> This works for hosted websites (with a domain)

## **What Is `manifest.json`?**
It is a file that:
- tells your browser how your PWA should behave
- controls the app name and icon
- controls the splash screen colors
- lets users "install" your website like a real app
- is required for Bubblewrap to convert a website into a Play Store APK
---
- You can also create your own customized `manifest.json` + `apk` quite easily using the site: [https://www.pwabuilder.com](https://www.pwabuilder.com) (Opensource)


> [!IMPORTANT]
> 1. Create a file called `manifest.json` on your website with content inside the code block below `manifest.json`:
> 2. Create a new directory inside `public_html` (the root directory) called `../assets/images/App` and add the image resources (logos). Refer to the code block below. NB: ALSO, AFTER REPLACING WITH YOUR VALUES, REMOVE UNNECESSARY COMMENTS to ensure the file looks clean.
> - Refer to https://romannurik.github.io/AndroidAssetStudio/  for setting up the right icon logo(s)
- Try logo sizes ranging from 512x512px to 1024x1024px (Recommended)

## **📌 Where to Put `manifest.json`?**
- Usually inside:
```
public_html/manifest.json
```

- Your manifest.json file should look like this:
*manifest.json*
```json
{
  // Full name of your app – appears on install prompts
  "name": "EchoPitch",

  // Short name used under the app icon on Android home screen
  "short_name": "EchoPitch",

  // What your web app is about – helps Play Store & users understand purpose
  "description": "A Kenyan football platform where players, fans, and coaches connect, showcase talent, and discover opportunities.",

  // Language of the app (English, Kenya variant)
  "lang": "en-KE",

  // Text direction – ltr = left-to-right
  "dir": "ltr",

  // Where the PWA should start when launched from home screen
  // Use UTM to track app opens in analytics
  "start_url": "/index.php?utm_source=web_app",

  // Defines how far the app can navigate
  // "/" means full website
  "scope": "/",

  // Display mode: standalone = looks like a real app (no browser UI)
  "display": "standalone",

  // Forces browsers to respect "standalone"
  "display_override": ["standalone"],

  // Locks the app to portrait mode for a better mobile experience
  "orientation": "portrait",

  // Browser address bar color
  "theme_color": "#FF770A",

  // Splash screen background color
  "background_color": "#FFFFFF",

  // Your app’s unique ID (package identifier)
  // IMPORTANT: Must match Bubblewrap package ID
  "id": "ke.co.echopitch.app",

  // Helps app stores categorize your PWA
  "categories": ["social", "sports"],

  // App icons for Android install (multiple sizes required)
  "icons": [
    {
      // Path to your 192px icon
      "src": "/assets/images/App/android-192.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      // Optional larger icon (256px)
      "src": "/assets/images/App/android-256.png",
      "sizes": "256x256",
      "type": "image/png"
    },
    {
      // Optional 384px icon
      "src": "/assets/images/App/android-384.png",
      "sizes": "384x384",
      "type": "image/png"
    },
    {
      // Main install icon required by Bubblewrap (512px)
      // "purpose": "any maskable" ensures icons fit rounded shapes
      "src": "/assets/images/App/android-512.png",
      "sizes": "512x512",
      "type": "image/png",
      "purpose": "any maskable"
    }
  ]
}
```

### **STEP 2: Install Node.js**
1. **Download Node.js**
    - Go to [nodejs.org](https://nodejs.org/)
    - Download **LTS version** (recommended for most users)
    - Run the installer (Windows/Mac/Linux)
2. **Verify Installation** (Command Prompt/Terminal)
```bash
  node --version
  npm --version
```
- You should see version numbers (e.g., v18.x.x)

### **Step 3: Install Bubblewrap**
- Open **Command Prompt** (Windows) or **Terminal** (Mac/Linux):
### Install Bubblewrap globally
```bash
npm install -g @bubblewrap/cli
```
### Verify installation
```bash
bubblewrap --version
```
- **If you get permission errors:**
- **Windows:** ***Run Command Prompt as Administrator***
- **Mac/Linux:** Use `sudo`
```sudo
sudo npm install -g @bubblewrap/cli
```


### **STEP 4: Install necessary Dependencies
- Bubblewrap + Android SDK **cannot run without JDK 17** (NOT Java 8, NOT Java 11).
## **(a)
#### (a) (i) — Download Command-line Tools
1. Go to the official Android download page:  
    **https://developer.android.com/studio#command-tools**
2. Scroll to the bottom until you find **“`Command line tools only`”**
3. Download:  
    **Windows: commandlinetools-win-xxxx_latest.zip**
4. Extract it somewhere (e.g., Desktop/Downloads).  
    Inside the ZIP you will see a folder named:
`cmdline-tools`

### **(ii) — Move the Folder Into Your Bubblewrap SDK Folder**
- Move the extracted `cmdline-tools` folder into e.g.,:
```
C:\Users\LEWIS\.bubblewrap\android_sdk\
```

You should end up with:
`C:\Users\LEWIS\.bubblewrap\android_sdk\cmdline-tools\latest\bin\`

 > [!IMPORTANT] 
 > Rename the folder correctly

Inside the ZIP, the folder name is usually:
```
cmdline-tools     
    └── bin
```

DO THIS:
> [!IMPORTANT]
> Rename `cmdline-tools` to `latest`

So you end up with something like:
`C:\Users\LEWIS\.bubblewrap\android_sdk\cmdline-tools\latest\`

### **NB: Folder Structure MUST Look Exactly Like This**
```
.android_sdk/
    build-tools/
    platform-tools/
    platforms/
    cmdline-tools/
        latest/
            bin/
            lib/
            NOTICE.txt
```
If any of those are missing, Bubblewrap cannot work.

## **(b)**
### **1 — Install JDK 17 (the ONLY version Bubblewrap supports)**
Download JDK 17 (LTS) for Windows:
🟦 **Adoptium Temurin JDK 17**  
[https://adoptium.net/temurin/releases/?version=17](https://adoptium.net/temurin/releases/?version=17)

Download:
- **Windows x64 MSI Installer** (Recommended)

Install it normally.
After installation, check that this folder exists:
`C:\Program Files\Eclipse Adoptium\jdk-17.*`
(Version numbers may vary)


### **2 — Set JAVA_HOME (VERY IMPORTANT)**
#### (b) (i) Open **Windows Search → type "Environment Variables"**

Choose:  
**Edit the system environment variables**
#### (ii) Click: **Environment Variables…**

#### (iii) Under _System variables_ → click **New…**
 - **Variable name:** `JAVA_HOME`
- **Variable value:**  
```
C:\Program Files\Eclipse Adoptium\jdk-17.x.x
``` 
(Paste your exact path)

Click **OK**.
#### (iv) Still in System variables, find `Path` → Edit
Click **New** → Add:
```
%JAVA_HOME%\bin
```
Press **OK** on all windows.

### **3 — Restart PowerShell**

- Then, RUN:
```bash
java -version
```

It MUST output something like:
```bash
openjdk version "17.0.10" …
```
If yes → Java is installed correctly.✅

###  **4 — SDK Manager
### **(iii) — Install ZIPALIGN + Build Tools (Now That sdkmanager Exists)**
- Navigate back:
```bash
cd C:\Users\LEWIS\.bubblewrap\android_sdk\cmdline-tools\latest\bin
```

Run:
```bash
./sdkmanager --licenses
```

Accept all licenses.
Then install Build Tools 33.0.2 and 34.0.0 (the correct versions for Windows):
```bash
./sdkmanager "build-tools;33.0.2"
./sdkmanager "build-tools;34.0.0"

```

This will create: `C:\Users\LEWIS\.bubblewrap\android_sdk\build-tools\33.0.2\` and `C:\Users\LEWIS\.bubblewrap\android_sdk\build-tools\34.0.0\`

```bash
./sdkmanager --licenses
```
You should now see:
`7/7 licenses accepted...`



### **STEP 5: Setup Your TWA Project**
- Run
```bash
mkdir echopitch-twa
cd echopitch-twa
```

### **Step 6: Initialize Your TWA Project**
### Initialize with your website URL
```bash
bubblewrap init --manifest=https://echopitch.co.ke/manifest.json
```

**During initialization, you'll be asked:**
1. **Application ID:** `ke.co.echopitch.app` (this is your package name)
2. **Application Name:** `EchoPitch` (Should be a short name)
3. **Display Mode:** Choose `standalone`
4. **Theme Color:** Enter hex code (e.g., `#000000`)
5. **Background Color:** Enter hex code (e.g., `#ffffff`)
6. **Enable notifications?** Usually `n` (no)
7. **Shortcuts:** Usually `n` (no)
8. **Signing Key:** Press Enter to generate new
    - Enter passwords when prompted
    - **SAVE THESE PASSWORDS!** You'll need them later

> [!IMPORTANT]  
> **Use one password for BOTH keystore + alias** (so Bubblewrap will never fail)

> [!NOTE]
-  If you run into a problem, delete the key:
```bash
del C:\Users\LEWIS\echopitch-twa\android.keystore
```

Recreate a fresh one by running:
```bash
keytool -genkeypair -v ^  -keystore C:\Users\LEWIS\echopitch-twa\android.keystore ^  -alias unique_key ^  -keyalg RSA -keysize 2048 -validity 10000
```

> [!NOTE]
> After entering generated password, project directory generated successfully at: ./**twa-manifest.json**

### **Step 7: Configuring the twa-manifest.json**
- Before configuring the twa-manifest.json file, you need to generate a SHA256 key (**Required for Google Play approval**)
#### (i). **Digital Asset Links Setup**
- Generate your SHA-256 fingerprint by running:
```bash
keytool -list -v -keystore android.keystore -alias echopitchkey
```

> [!NOTE] 
> `echopitch` is the signing key created earlier with 2 (keystore & alias) passwords. Replace it with your correct one.
- Enter your keystore password:
- After entering the correct password, you should see an output similar to:

```bash
Alias name: echopitchkey
Creation date: Dec 5, 2025
Entry type: PrivateKeyEntry
Certificate chain length: 1
Certificate[1]:
Owner: CN=John Doe, OU=IT Department, O=Main Devs, C=US
Issuer: CN=John Doe, OU=IT Department, O=Main Devs, C=US
Serial number: 6caf5177905bb133
Valid from: Fri Dec 05 02:09:52 EAT 2025 until: Sat Sep 07 02:09:52 EAT 2080
Certificate fingerprints:
         SHA1: 8A:83:B0:22:9F:0A:B3:54:A2:D7:F1:4C:22:DE:1D:76:6E:DA:33:C3
         SHA256: F6:EB:2C:0B:F3:90:94:25:AB:3B:5D:3C:21:2A:18:2A:16:CE:F7:F1:DE:26:4C:17:C6:F4:34:63:6B:72:94:FF
Signature algorithm name: SHA256withRSA
Subject Public Key Algorithm: 2048-bit RSA key
Version: 3

Extensions:

#1: ObjectId: 2.6.19.14 Criticality=false
SubjectKeyIdentifier [
KeyIdentifier [
0000: 0E 84 E6 EB C3 D4 1E 62   64 49 D1 B6 11 63 A6 1C  .t.....adY...c..
0020: CD 58 11 E4                                        .X1.
]
]
```

#### (ii). **Create `assetlinks.json` inside the root project directory (echopitch-twa):**
```json
[{
  "relation": ["delegate_permission/common.handle_all_urls"],
  "target": {
    "namespace": "android_app",
    "package_name": "com.echopitch.mobile",
    "sha256_cert_fingerprints": [
      "YOUR_SHA256"
    ]
  }
}]
```

- In this case, YOUR_SHA256=`F6:EB:2C:0B:F3:90:94:25:AB:3B:5D:3C:21:2A:18:2A:16:CE:F7:F1:DE:26:4C:17:C6:F4:34:63:6B:72:94:FF`

#### (iii). **Upload to your website:
- File must be at: `https://echopitch.co.ke/.well-known/assetlinks.json`
> [!NOTE]

> NB: To view hidden files (CPANEL), also known as "dotfiles" (because their names start with a dot, like `.well-known, .htaccess`), in cPanel's File Manager:
> - **Log in to your cPanel account.**
> - **Navigate to the File Manager.** This is typically found under the "Files" section on the cPanel homepage.
> - **Open the File Manager settings.** In the File Manager interface, locate and click the "Settings" button, usually found in the top right corner.
> - **Enable "Show Hidden Files (dotfiles)".** In the Preferences window that appears, check the box next to the option labeled "Show Hidden Files (dotfiles)".
> - **Save the changes.** Click the "Save" button to apply your settings.
- *After saving, the File Manager will refresh, and you will now be able to see all hidden files, including dotfiles, within the selected directory.*
- Now open the `.well-known` and click upload, then browse and upload the `assetlinks.json`.
- DON'T FORGET TO HIDE THE `.dot` files after you're done to prevent accidental changes.

#### (iv). Set up twa-manifest.json
- Now right-click on `twa-manifest.json` inside the root directory and select `edit with Notepad`.
- Modify it to look like the one below. ALSO, AFTER REPLACING WITH YOUR VALUES, REMOVE UNNECESSARY COMMENTS to ensure the file looks clean:
```json
  {
  // The unique Android package name for your TWA app.
  // Format: country.domain.appname (must match Play Store requirements)
  "packageId": "ke.co.echopitch.app",

  // The website domain that your TWA will load.
  // Must match EXACTLY the site that has the manifest.json.
  "host": "echopitch.co.ke",

  // App name displayed under your app icon.
  "name": "EchoPitch",

  // Name displayed in the Android launcher (can be same as "name").
  "launcherName": "EchoPitch",

  // How the app appears: "standalone" = looks like a real native app.
  "display": "standalone",

  // UI theme (light mode).
  "themeColor": "#FF770A",

  // UI theme (dark mode).
  "themeColorDark": "#FF770A",

  // Navigation bar color (light mode).
  "navigationColor": "#FF770A",

  // Navigation bar color (dark mode).
  "navigationColorDark": "#FF770A",

  // Navigation divider strip color (light mode).
  "navigationDividerColor": "#FF770A",

  // Navigation divider strip color (dark mode).
  "navigationDividerColorDark": "#FF770A",

  // App background color used during startup.
  "backgroundColor": "#FFFFFF",

  // Allow browser push notifications via TWA.
  "enableNotifications": true,

  // The site URL the app should open when launched.
  "startUrl": "/index.php?utm_source=web_app",

  // Icon used for Android (512px recommended).
  "iconUrl": "https://echopitch.co.ke/assets/images/App/android-512.png",

  // Maskable icon for adaptive shapes (circle, squircle, etc.).
  "maskableIconUrl": "https://echopitch.co.ke/assets/images/App/android-256.png",

  // Single-color icon used for Android monochrome UI.
  "monochromeIconUrl": "https://echopitch.co.ke/assets/images/App/monochrome-384.png",

  // Controls how long the splash screen fades out.
  "splashScreenFadeOutDuration": 300,

  // Android signing key information — REQUIRED for building a real APK/AAB.
  "signingKey": {
    // Path to your keystore file on your computer.
    "path": "C:\\Users\\LEWIS\\echopitch-twa\\android.keystore",
    
    // Alias inside your keystore (must match what you created).
    "alias": "echopitchkey"
  },

  // Version name shown to users.
  "appVersionName": "v1.00",

  // Version code (MUST increase when uploading to Play Store).
  "appVersionCode": 1,

  // App shortcuts shown on long-press (your app currently has none).
  "shortcuts": [],

  // Auto-generated by Bubblewrap; do not modify.
  "generatorApp": "bubblewrap-cli",

  // Link to the LIVE web manifest.json on your website.
  // This must always be reachable.
  "webManifestUrl": "https://echopitch.co.ke/manifest.json",

  // If TWA fails, fallback to Chrome Custom Tabs.
  "fallbackType": "customtabs",

  // Features your TWA is allowed to delegate to the browser.
  "features": {
    "locationDelegation": {
      // Enables geolocation (GPS access).
      "enabled": true
    }
  },

  // Bubblewrap alpha dependencies — always false.
  "alphaDependencies": {
    "enabled": false
  },

  // Removes “Site Settings” shortcut inside Android app menu.
  "enableSiteSettingsShortcut": false,

  // App is NOT restricted to ChromeOS (Chromebooks).
  "isChromeOSOnly": false,

  // Not a Meta Quest (VR) app.
  "isMetaQuest": false,

  // Full domain scope allowed for the TWA.
  "fullScopeUrl": "https://echopitch.co.ke/",

  // Minimum Android SDK supported (21 = Android 5.0).
  "minSdkVersion": 21,

  // Lock the screen orientation.
  "orientation": "portrait",

  // SHA256 fingerprint required by Digital Asset Links.
  // Replace "YOUR_SHA256" with your actual fingerprint from:
  // keytool -list -v -keystore android.keystore
  "fingerprints": [
    {
      "value": "YOUR_SHA256"
    }
  ],

  // Trusted origins allowed to work inside the TWA.
  "additionalTrustedOrigins": [],

  // Not used by most apps.
  "retainedBundles": [],
  "protocolHandlers": [],
  "fileHandlers": [],

  // Launch mode (default empty).
  "launchHandlerClientMode": "",

  // Required by Chrome — overrides display mode.
  "displayOverride": [
    "standalone"
  ],

  // Same as appVersionName; some versions of Bubblewrap require this.
  "appVersion": "v1.00"
}
```


### **Step 8: Build Your APK**
#### Build the APK (release version)
```bash
bubblewrap build
```

You'll be asked for:
1. **Keystore password:** (Enter a unique password)
2. **Key password:** Your alias password
3. **Output location:** Press Enter for default

### **Step 9: Find Your APK**
- After build completes, find your APK:
- Look in your-project-folder "``echopitch-twa``"
The APK will be in the same folder or a subfolder called "build"

#### Navigate to build folder (Terminal)
```bash
cd ./build
```
### List files
- Run: 
>`dir`   for Windows
> ls -la for Mac/Linux
- Look for: `app-release-signed.apk` 

### **Step 10: Test Your APK**
1. **Transfer to Android phone:**
    - Email it to yourself
    - Use USB cable
    - Upload to Google Drive
    - Send to WhatsApp
2. **Install on Android:**
    - Open File Manager on phone
    - Tap the APK file
    - Allow "Install from unknown sources" if prompted
    - Install and test

### **Step 10: Updating Your APK**
- Any time you make new changes to your app (*NOT THE WEBSITE!*), simply open terminal in the project directory, in this case `echopitch-twa` and run the commands below in order:
```bash
bubblewrap update
bubblewrap build
```


You should get an output similar the one below:
```bash
PS C:\Users\LEWIS\echopitch-twa> bubblewrap build
,-----.        ,--.  ,--.  ,--.
|  |) /_,--.,--|  |-.|  |-.|  |,---.,--.   ,--,--.--.,--,--.,---.
|  .-.  |  ||  | .-. | .-. |  | .-. |  |.'.|  |  .--' ,-.  | .-. |
|  '--' '  ''  | `-' | `-' |  \   --|   .'.   |  |  \ '-'  | '-' '
`------' `----' `---' `---'`--'`----'--'   '--`--'   `--`--|  |-'
                                                           `--'
Please, enter passwords for the keystore C:\Users\LEWIS\echopitch-twa\android.keystore and alias echopitchkey.

? Password for the Key Store: ************
? Password for the Key: ************

Building the Android App...
        - Generated Android APK at ./app-release-signed.apk
        - Generated Android App Bundle at ./app-release-bundle.aab
PS C:\Users\LEWIS\echopitch-twa> bubblewrap update
,-----.        ,--.  ,--.  ,--.
|  |) /_,--.,--|  |-.|  |-.|  |,---.,--.   ,--,--.--.,--,--.,---.
|  .-.  |  ||  | .-. | .-. |  | .-. |  |.'.|  |  .--' ,-.  | .-. |
|  '--' '  ''  | `-' | `-' |  \   --|   .'.   |  |  \ '-'  | '-' '
`------' `----' `---' `---'`--'`----'--'   '--`--'   `--`--|  |-'
                                                           `--'
? versionName for the new App version: v1.106
Upgraded app version to versionName: v1.106 and versionCode: 11
Generating Android Project.
 >> [████████████████████████████████████████] 100%

Project updated successfully.
Build it by running bubblewrap build
PS C:\Users\LEWIS\echopitch-twa> bubblewrap build
,-----.        ,--.  ,--.  ,--.
|  |) /_,--.,--|  |-.|  |-.|  |,---.,--.   ,--,--.--.,--,--.,---.
|  .-.  |  ||  | .-. | .-. |  | .-. |  |.'.|  |  .--' ,-.  | .-. |
|  '--' '  ''  | `-' | `-' |  \   --|   .'.   |  |  \ '-'  | '-' '
`------' `----' `---' `---'`--'`----'--'   '--`--'   `--`--|  |-'
                                                           `--'
Please, enter passwords for the keystore C:\Users\LEWIS\echopitch-twa\android.keystore and alias echopitchkey.

? Password for the Key Store: ************
? Password for the Key: ************

Building the Android App...
        - Generated Android APK at ./app-release-signed.apk
        - Generated Android App Bundle at ./app-release-bundle.aab
```  



## **Optional Enhancement - Create App Screenshot:** (Recommended)

Take a screenshot of your homepage and upload to:
```
https://echopitch.co.ke/assets/images/App/screenshot-1.jpg
```
This helps app stores and makes it feel more like a real app.



# **Adding Offline Detection Support**
## **1. Create/Update `.htaccess` for offline support:**
- Create a file `.htaccess` in your website root (or update your existing one):  

```text
RewriteEngine On

# Force HTTPS
RewriteCond %{HTTPS} off
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]

# Service Worker Headers
<IfModule mod_headers.c>
  # Enable Service Worker for entire domain
  Header set Service-Worker-Allowed "/"
  
  # Cache manifest for 1 day
  <Files "manifest.json">
    Header set Cache-Control "public, max-age=86400"
    Header set Content-Type "application/json"
  </Files>
  
  # Service worker - no cache
  <Files "sw.js">
    Header set Cache-Control "no-cache, no-store, must-revalidate"
    Header set Service-Worker-Allowed "/"
    Header set Content-Type "application/javascript"
  </Files>
  
  # Offline page - cache for 1 year
  <Files "offline.html">
    Header set Cache-Control "public, max-age=31536000"
  </Files>
</IfModule>

# Ensure proper MIME types
AddType application/manifest+json .json
AddType application/javascript .js

# BEGIN cPanel-generated php ini directives, do not edit
# Manual editing of this file may result in unexpected behavior.
# To make changes to this file, use the cPanel MultiPHP INI Editor (Home >> Software >> MultiPHP INI Editor)
# For more information, read our documentation (https://go.cpanel.net/EA4ModifyINI)
<IfModule php8_module>
   php_value date.timezone "Africa/Nairobi"
</IfModule>
<IfModule lsapi_module>
   php_value date.timezone "Africa/Nairobi"
</IfModule>
# END cPanel-generated php ini directives, do not edit
```

### **2. Create `offline.html` in root directory**
```html
<!DOCTYPE html>
<html lang="en-KE">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="theme-color" content="#FF770A">
    <title>EchoPitch - Connection Required</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
            background-color: #f8f9fa;
            color: #333;
            line-height: 1.6;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 20px;
            text-align: center;
        }
        
        .container {
            max-width: 500px;
            width: 100%;
            padding: 40px 30px;
            background: white;
            border-radius: 16px;
            box-shadow: 0 8px 30px rgba(0, 0, 0, 0.08);
            border: 1px solid #eaeaea;
        }
        
        .logo {
            margin-bottom: 30px;
        }
        
        .logo-img {
            height: 60px;
            width: auto;
            margin-bottom: 15px;
        }
        
        .logo-text {
            font-size: 28px;
            font-weight: 700;
            color: #FF770A;
            letter-spacing: -0.5px;
        }
        
        .logo-subtext {
            font-size: 14px;
            color: #666;
            font-weight: 400;
            margin-top: 5px;
        }
        
        .status-icon {
            width: 80px;
            height: 80px;
            margin: 0 auto 25px;
            background: #f0f7ff;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: #4285f4;
            font-size: 36px;
        }
        
        h1 {
            font-size: 24px;
            font-weight: 600;
            color: #202124;
            margin-bottom: 15px;
        }
        
        .message {
            color: #5f6368;
            font-size: 16px;
            margin-bottom: 30px;
            padding: 0 10px;
        }
        
        .tips {
            background: #f8f9fa;
            border-radius: 12px;
            padding: 20px;
            margin-bottom: 30px;
            text-align: left;
        }
        
        .tips h3 {
            font-size: 16px;
            color: #202124;
            margin-bottom: 12px;
            font-weight: 600;
        }
        
        .tips ul {
            list-style: none;
            padding-left: 0;
        }
        
        .tips li {
            padding: 8px 0;
            color: #5f6368;
            font-size: 14px;
            position: relative;
            padding-left: 24px;
        }
        
        .tips li:before {
            content: "•";
            color: #FF770A;
            font-size: 20px;
            position: absolute;
            left: 0;
            top: 5px;
        }
        
        .actions {
            display: flex;
            gap: 15px;
            justify-content: center;
        }
        
        .btn {
            padding: 14px 28px;
            border-radius: 8px;
            font-size: 15px;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.2s ease;
            border: none;
            min-width: 140px;
        }
        
        .btn-primary {
            background: #FF770A;
            color: white;
        }
        
        .btn-primary:hover {
            background: #e66a00;
            transform: translateY(-1px);
            box-shadow: 0 4px 12px rgba(255, 119, 10, 0.2);
        }
        
        .btn-secondary {
            background: #f1f3f4;
            color: #5f6368;
            border: 1px solid #dadce0;
        }
        
        .btn-secondary:hover {
            background: #e8eaed;
            transform: translateY(-1px);
        }
        
        .connection-status {
            margin-top: 25px;
            padding: 12px;
            background: #f8f9fa;
            border-radius: 8px;
            font-size: 14px;
            color: #5f6368;
        }
        
        .status-indicator {
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }
        
        .status-dot {
            width: 10px;
            height: 10px;
            border-radius: 50%;
            background: #dc3545;
            animation: pulse 2s infinite;
        }
        
        .status-dot.online {
            background: #34a853;
            animation: none;
        }
        
        @keyframes pulse {
            0% { opacity: 1; }
            50% { opacity: 0.5; }
            100% { opacity: 1; }
        }
        
        @media (max-width: 480px) {
            .container {
                padding: 30px 20px;
            }
            
            .actions {
                flex-direction: column;
            }
            
            .btn {
                width: 100%;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Logo Section -->
        <div class="logo">
            <!-- Using your app icon as logo -->
            <img src="/assets/images/logo-s.png" alt="EchoPitch" class="logo-img" onerror="this.style.display='none'">
            <div class="logo-text">EchoPitch</div>
            <div class="logo-subtext">"Your Game. Your glory"</div>
        </div>
        
        <!-- Status Icon -->
        <div class="status-icon">
            📡
        </div>
        
        <!-- Main Message -->
        <h1>Connection Required</h1>
        <div class="message">
            EchoPitch needs an active internet connection to provide real-time updates, match data, and team coordination.
        </div>
        
        <!-- Help Tips -->
        <div class="tips">
            <h3>Quick Troubleshooting</h3>
            <ul>
                <li>Check your Wi-Fi or mobile data connection</li>
                <li>Switch between Wi-Fi and mobile data</li>
                <li>Restart your device or router</li>
                <li>Move to an area with better signal</li>
            </ul>
        </div>
        
        <!-- Action Buttons -->
        <div class="actions">
            <button class="btn btn-primary" onclick="retryConnection()">
                Try Again
            </button>
            <button class="btn btn-secondary" onclick="goToSettings()">
                Network Settings
            </button>
        </div>
        
        <!-- Connection Status -->
        <div class="connection-status">
            <div class="status-indicator">
                <span class="status-dot" id="statusDot"></span>
                <span id="statusText">Checking connection...</span>
            </div>
        </div>
    </div>

    <script>
        // Update connection status
        function updateConnectionStatus() {
            const statusDot = document.getElementById('statusDot');
            const statusText = document.getElementById('statusText');
            
            if (navigator.onLine) {
                statusDot.className = 'status-dot online';
                statusText.textContent = 'Connected - Redirecting...';
                
                // Redirect to login after 1 second
                setTimeout(() => {
                    window.location.href = '/login.php?utm_source=web_app&reconnected=1';
                }, 1000);
            } else {
                statusDot.className = 'status-dot';
                statusText.textContent = 'No internet connection';
            }
        }
        
        // Retry connection
        function retryConnection() {
            updateConnectionStatus();
            if (!navigator.onLine) {
                window.location.reload();
            }
        }
        
        // Open network settings (Android intent)
        function goToSettings() {
            // Try to open Android settings
            if (window.Android && typeof window.Android.openSettings === 'function') {
                window.Android.openSettings();
            } else {
                // Fallback for web
                alert('Please check your device network settings');
            }
        }
        
        // Monitor connection changes
        window.addEventListener('online', updateConnectionStatus);
        window.addEventListener('offline', updateConnectionStatus);
        
        // Auto-check every 3 seconds
        setInterval(updateConnectionStatus, 3000);
        
        // Initial check
        document.addEventListener('DOMContentLoaded', updateConnectionStatus);
        
        // Prevent caching of this page
        if (window.performance && window.performance.navigation.type === window.performance.navigation.TYPE_RELOAD) {
            console.log('Offline page was reloaded');
        }
    </script>
</body>
</html>
```

### **3. Create `sw.js` in root directory:**
```javascript
// EchoPitch Service Worker - Aggressive Caching
const CACHE_NAME = 'echopitch-app-v1';
const OFFLINE_URL = '/offline.html';

// Install - Cache critical files immediately
self.addEventListener('install', event => {
  console.log('[SW] Installing EchoPitch Service Worker');
  event.waitUntil(
    caches.open(CACHE_NAME)
      .then(cache => cache.addAll([
        OFFLINE_URL,
        '/login.php',
        '/manifest.json',
        '/assets/images/App/android-192.png'
      ]))
      .then(() => {
        console.log('[SW] Installation complete');
        return self.skipWaiting();
      })
  );
});

// Activate - Take control immediately
self.addEventListener('activate', event => {
  console.log('[SW] Activating and claiming clients');
  event.waitUntil(self.clients.claim());
});

// Fetch - Handle ALL requests
self.addEventListener('fetch', event => {
  const request = event.request;
  
  // Skip non-GET requests
  if (request.method !== 'GET') return;
  
  // Handle navigation requests specially
  if (request.mode === 'navigate') {
    event.respondWith(
      fetch(request)
        .catch(async () => {
          console.log('[SW] Offline navigation detected');
          const cache = await caches.open(CACHE_NAME);
          const cached = await cache.match(OFFLINE_URL);
          return cached || new Response('Offline', { status: 503 });
        })
    );
    return;
  }
  
  // For all other requests: Cache first, then network
  event.respondWith(
    caches.match(request)
      .then(cached => {
        // Return cached version if available
        if (cached) {
          console.log('[SW] Serving from cache:', request.url);
          return cached;
        }
        
        // Otherwise fetch from network
        return fetch(request)
          .then(response => {
            // Cache successful responses
            if (response.ok) {
              const clone = response.clone();
              caches.open(CACHE_NAME)
                .then(cache => cache.put(request, clone))
                .catch(err => console.warn('[SW] Cache put failed:', err));
            }
            return response;
          })
          .catch(error => {
            console.log('[SW] Network failed:', error);
            // For images, return fallback
            if (request.destination === 'image') {
              return caches.match('/assets/images/App/android-192.png');
            }
            // Return empty responses for CSS/JS to prevent errors
            if (request.destination === 'style' || request.destination === 'script') {
              return new Response('', { 
                headers: { 'Content-Type': request.destination === 'style' ? 'text/css' : 'application/javascript' }
              });
            }
          });
      })
  );
});

// Listen for messages from the app
self.addEventListener('message', event => {
  if (event.data === 'skipWaiting') {
    self.skipWaiting();
  }
});

console.log('[SW] EchoPitch Service Worker loaded');
```


### **4. Update `login.php` or and `index.php` with Service Worker Registration:**

- Add this to the `<head>` in meta section:
  ```php
<meta name="mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-capable" content="yes">
  ```   
  
- Add this to the bottom of `login.php` or `index.php` (before `</body>`):
```php
<script>
    (function () {
      if (!('serviceWorker' in navigator)) return;
    
      window.addEventListener('load', function () {
        navigator.serviceWorker.register('/sw.js', { scope: '/' })
          .then(function (registration) {
    
            // Activate new SW immediately
            if (registration.waiting) {
              registration.waiting.postMessage('skipWaiting');
            }
    
            // Listen for updates
            registration.addEventListener('updatefound', function () {
              const newWorker = registration.installing;
              if (!newWorker) return;
    
              newWorker.addEventListener('statechange', function () {
                if (newWorker.state === 'installed' && navigator.serviceWorker.controller) {
                  newWorker.postMessage('skipWaiting');
                }
              });
            });
    
          })
          .catch(function (error) {
            console.error('Service Worker registration failed:', error);
          });
      });
    
      // Connection state tracking (safe for TWA)
      function updateConnectionState() {
        document.body.classList.toggle('offline', !navigator.onLine);
      }
    
      window.addEventListener('online', updateConnectionState);
      window.addEventListener('offline', updateConnectionState);
      updateConnectionState();
    })();
    </script>
```



### **5. Create `robots.txt` in root directory** (Optional but recommended)
- This file Controls Search Engine Access. 
- It tells search engine crawlers which pages or files on your website they can or cannot request.
- It also helps search engines find all your pages
```text
User-agent: *
Allow: /

# Service worker and PWA files
Allow: /sw.js
Allow: /sw-v2.js
Allow: /manifest.json
Allow: /offline.html
Allow: /.well-known/assetlinks.json

# Block search from sensitive areas (if they exist)
Disallow: /admin/
Disallow: /cgi-bin/
Disallow: /tmp/
Disallow: /private/

# Crawl delay (optional - prevents server overload)
Crawl-delay: 2

# Sitemap (create this later)
# Sitemap: https://echopitch.co.ke/sitemap.xml
```

- - `User-agent: *` = Applies to all search engines (Google, Bing, etc.)
- `Allow: /` = Allows crawling of entire site
- `Disallow: /admin/` = Blocks crawling of admin section


### **6. Update `twa-manifest.json`**
```json
{
  "packageId": "ke.co.echopitch.app",
  "host": "echopitch.co.ke",
  "name": "EchoPitch",
  "launcherName": "EchoPitch",
  "display": "standalone",
  "themeColor": "#FF770A",
  "themeColorDark": "#FF770A",
  "navigationColor": "#FF770A",
  "navigationColorDark": "#FF770A",
  "navigationDividerColor": "#FF770A",
  "navigationDividerColorDark": "#FF770A",
  "backgroundColor": "#FFFFFF",
  "enableNotifications": true,
  "startUrl": "/login.php?app_mode=1",
  "iconUrl": "https://echopitch.co.ke/assets/images/App/android-512.png",
  "maskableIconUrl": "https://echopitch.co.ke/assets/images/App/android-256.png",
  "monochromeIconUrl": "https://echopitch.co.ke/assets/images/App/monochrome-384.png",
  "splashScreenFadeOutDuration": 300,
  "signingKey": {
    "path": "C:\\Users\\LEWIS\\echopitch-twa\\android.keystore",
    "alias": "echopitchkey"
  },
  "appVersionName": "v1.21",
  "appVersionCode": 1,
  "shortcuts": [],
  "generatorApp": "bubblewrap-cli",
  "webManifestUrl": "https://echopitch.co.ke/manifest.json",
  "fallbackType": "customtabs",
  "features": {
    "locationDelegation": {
      "enabled": true
    }
  },
  "alphaDependencies": {
    "enabled": false
  },
  "enableSiteSettingsShortcut": false,
  "isChromeOSOnly": false,
  "isMetaQuest": false,
  "fullScopeUrl": "https://echopitch.co.ke/",
  "minSdkVersion": 21,
  "orientation": "portrait",
  "fingerprints": [
    {
      "value": "YOUR_SHA256"
    }
  ],
  "additionalTrustedOrigins": [],
  "retainedBundles": [],
  "protocolHandlers": [],
  "fileHandlers": [],
  "launchHandlerClientMode": "",
  "displayOverride": [
    "standalone"
  ],
  "appVersion": "v1.21"
}
```


### **7. Update `manifest.json`**
```json
{
  "name": "EchoPitch",
  "short_name": "EchoPitch",
  "description": "A Kenyan football platform where players, fans, and coaches connect, showcase talent, and discover opportunities.",
  "lang": "en-KE",
  "dir": "ltr",
  "start_url": "/login.php?app_mode=1",
  "scope": "/",
  "display": "standalone",
  "display_override": ["standalone", "fullscreen"],
  "orientation": "portrait",
  "theme_color": "#FF770A",
  "background_color": "#FFFFFF",
  "id": "ke.co.echopitch.app",
  "categories": ["social", "sports"],
  "screenshots": [
    {
      "src": "/assets/images/App/screenshot-1.jpg",
      "sizes": "720x1640",
      "type": "image/jpeg",
      "form_factor": "narrow"
    }
  ],
  "icons": [
    { 
      "src": "/assets/images/App/android-192.png", 
      "sizes": "192x192", 
      "type": "image/png" 
    },
    { 
      "src": "/assets/images/App/android-256.png", 
      "sizes": "256x256", 
      "type": "image/png" 
    },
    { 
      "src": "/assets/images/App/android-384.png", 
      "sizes": "384x384", 
      "type": "image/png" 
    },
    { 
      "src": "/assets/images/App/android-512.png", 
      "sizes": "512x512", 
      "type": "image/png", 
      "purpose": "any maskable" 
    }
  ]
}
```


#### **STEP 8. REBUILD APK**
- Open terminal in the project directory, in this case `echopitch-twa` and run the commands below in order:
```bash
bubblewrap update
bubblewrap build
```


You should get an output similar the one below:
```bash
PS C:\Users\LEWIS\echopitch-twa> bubblewrap build
,-----.        ,--.  ,--.  ,--.
|  |) /_,--.,--|  |-.|  |-.|  |,---.,--.   ,--,--.--.,--,--.,---.
|  .-.  |  ||  | .-. | .-. |  | .-. |  |.'.|  |  .--' ,-.  | .-. |
|  '--' '  ''  | `-' | `-' |  \   --|   .'.   |  |  \ '-'  | '-' '
`------' `----' `---' `---'`--'`----'--'   '--`--'   `--`--|  |-'
                                                           `--'
Please, enter passwords for the keystore C:\Users\LEWIS\echopitch-twa\android.keystore and alias echopitchkey.

? Password for the Key Store: ************
? Password for the Key: ************

Building the Android App...
        - Generated Android APK at ./app-release-signed.apk
        - Generated Android App Bundle at ./app-release-bundle.aab
PS C:\Users\LEWIS\echopitch-twa> bubblewrap update
,-----.        ,--.  ,--.  ,--.
|  |) /_,--.,--|  |-.|  |-.|  |,---.,--.   ,--,--.--.,--,--.,---.
|  .-.  |  ||  | .-. | .-. |  | .-. |  |.'.|  |  .--' ,-.  | .-. |
|  '--' '  ''  | `-' | `-' |  \   --|   .'.   |  |  \ '-'  | '-' '
`------' `----' `---' `---'`--'`----'--'   '--`--'   `--`--|  |-'
                                                           `--'
? versionName for the new App version: v1.22
Upgraded app version to versionName: v1.22 and versionCode: 2
Generating Android Project.
 >> [████████████████████████████████████████] 100%

Project updated successfully.
Build it by running bubblewrap build
PS C:\Users\LEWIS\echopitch-twa> bubblewrap build
,-----.        ,--.  ,--.  ,--.
|  |) /_,--.,--|  |-.|  |-.|  |,---.,--.   ,--,--.--.,--,--.,---.
|  .-.  |  ||  | .-. | .-. |  | .-. |  |.'.|  |  .--' ,-.  | .-. |
|  '--' '  ''  | `-' | `-' |  \   --|   .'.   |  |  \ '-'  | '-' '
`------' `----' `---' `---'`--'`----'--'   '--`--'   `--`--|  |-'
                                                           `--'
Please, enter passwords for the keystore C:\Users\LEWIS\echopitch-twa\android.keystore and alias echopitchkey.

? Password for the Key Store: ************
? Password for the Key: ************

Building the Android App...
        - Generated Android APK at ./app-release-signed.apk
        - Generated Android App Bundle at ./app-release-bundle.aab
```




### *WHAT'S NEXT...*
# 🎯 PUBLISHING APP ON GOOGLE PLAY STORE
- To publish on Google Play: 
- Am assuming you have a `Google Play Console` Account—One-time $25 Payment.
### **Google Play Console Steps**
1. Create a **New App**
2. Upload:
    - App icon
    - Screenshots
    - Description
3. Upload your **AAB** file under "Production"
4. Fill Data Safety & Content Rating
5. Submit for review
Publishing takes 1–3 hours typically.

# 📌 Important Google Play Rules
> [!IMPORTANT]
> Even for WebView apps:
> ✔ **App must have**:
> - Description
> - Screenshots
> - App icon
> - Feature graphic
> - Privacy Policy URL
> - App category
> - Content Rating
> - Data Safety info

> [!CAUTION]
> ✔ **Your website must:**
> - Not look exactly like a normal website
> - Have proper mobile UI
> - Provide genuine value
>  - Load fast
> - Not collect user data without disclosure

