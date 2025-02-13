### lookforsAndroid
- setJavaScriptEnabled(true)
- 

### lookforsIOS
#### Deeplinks
Universal Links were introduced in iOS to address the issues that arose with URL Schemes. URL Schemes allowed any application to use the same deep link, even if it belonged to another app, leading to confusion and potential security concerns like phishing. For instance, if the Reddit app has a URL scheme of reddit://, other apps can use the same scheme, leading to ambiguity. However, Universal Links use App Links or Deep Link URIs, such as https://reddit.com, which must be defined on the app’s domain in the Application Site Association, such as https://www.reddit.com/.well-known/apple-app-site-association. The App Site Association is an iOS feature that enables your app to handle incoming deep links associated with your website.

- Apple App Site Association
    - `.well-known/apple-app-site-association`
- Rename and unzip .ipa to get `Payload` folder (contains bundles, docs, lib, plist file)
- plutil -convert xml1 Info.plist (key-value pairs for app-specifics, userprefs, metadata)
    - CFBBundleURLComponents, CFBundleComponentPath (URL path) and CFBunndleURLComponentQueryItems (params), CFBundleURLSchemes (schemes xx://)
- Universal links (located on the .entitlements, starts with `applinks:`)
    - Look for key `com.apple.developer.associated-domains`
    - grep -iRn `applinks:`
- For compiled iPA, use radare2 (https://github.com/radareorg/radare2)
    - `r2 -qc 'izz~PropertyList' ./App`
- If no source code of the app / Xcode installed, view AppDelegate.swift file using terminal

- If black/grey box (only IPA, AppStore Link)
    - Get unencrypted with FridaiOSDump / iMazing
        - `strings DVIA-v2 | grep -E '.*\/.*'`
    - `frida-trace -U -m "*[* application:*openURL:*]" DVIA-v2`
    - https://gist.githubusercontent.com/grepharder/7a6c1b64f5e8eecf78ca076140ac09ec/raw/b7f8fe3cd5b02242d2ee6a4f07ebe6a9671c658b/universal_links.js (`frida -U -f ph.telegra.Telegraph -l universal_links.js`)
#### References
https://github.com/teknogeek/get_schemas
https://grepharder.github.io/blog/0x03_learning_about_universal_links_and_fuzzing_url_schemes_on_ios_with_frida.html
