AppBladeSDK PhoneGap Plugin
===================

Current supported Cordova versions : 2.5.0 - 2.9.0

Pending release: [3.0.0](https://github.com/AppBlade/SDK-PhoneGap-Plugin/tree/phonegap_v3.0)

For help, contact [AppBlade Support](https://support.appblade.com/).

###Organization
For each operating system currently supported by the SDK there is a folder in the `/Plugin` folder that contains the plugin, and a project in the `/Examples` folder which should help you get started.


##Manual Installation
Currently only the manual installation is supported. Plugman is going to be officially supported in the very near future (pending the release of our [3.0.0](https://github.com/AppBlade/SDK-PhoneGap-Plugin/tree/phonegap_v3.0) coverage).  

##Installation - iOS

1. Copy `AppBlade.js` into your `www/js` directory.
<br/> 
<br/>
2. Copy `AppBladePlugin.h` and `AppBladePlugin.m` into your Plugins folder.
<br/> 
<br/>
3. Add the AppBlade SDK to your project. 
<br/>*3a.* Drag the AppBladeSDK folder with the AppBlade.h and libAppBladeUniversal.a files into your PhoneGap project in Xcode. (Make sure "Copy items" is checked.)
<br/>*3b.* Under "Link Binary With Libraries" In your Target's "Build Phases" Click the "+" button and add the Library named "Security.Framework" to your project.
<br/>*3c.* Build the Project in Xcode to ensure that everything is running.
<br/>
<br/>
4. Ensure "appblade.com" is in Cordova's whitelist.
<br/>*4a.* Open your config.xml file and find the access element (the line `<access origin= ... />`). 
<br/>*4b.* If the `access` line is already `<access origin="*" />` Then nothing else needs to be done. ("*" means the whitelist is allowing all sources)
<br/>*4c.* If the `access` is not `<access origin="*" />` Then '<access origin="https://appblade.com" subdomains="true" />' will have to be added.
<br/>
<br/>
5. Add AppBlade to your list of plugins
<br/>*5a.* Open your config.xml file and find the plugins list element (the line `<plugins> ... </plugins>`). 
<br/>*5b.* Add `<plugin name="AppBlade" value="AppBladePlugin" />` inside your list of plugins.
<br/>
<br/>
6. Make AppBlade.js referenceable. 
<br/>*There are many ways to do this, as AppBlade.js can be treated just like  any other js file. This is just an example:* 
<br/>*6a.* In your `index.html` file add `<script type="text/javascript" src="js/AppBlade.js"></script>` after the "cordova-2.5.0.js" script reference and before the "js/index.js" script reference:

        <script type="text/javascript" src="cordova-[2.5.0+].js"></script>
        <script type="text/javascript" src="js/AppBlade.js"></script>
        <script type="text/javascript" src="js/index.js"></script>
<br/>
7. Link your PhoneGap project to AppBlade.com  
  *7a.* To use AppBlade features the app must first exist on AppBlade (click [+ New Project] after signing in). Get   your project keys by navigating to your AppBlade project and selecting "Reveal your API Keys".
<br/>*7b.* In your `index.js`, underneath the `app.receivedEvent('deviceready');` call the setup method with your SDK keys in the order they appear on the AppBlade site: UUID, token, secret, issued at.
The following example sets up the app blade plugin with API keys (actual values not used), sets up the crash reporter, and sets up feedback reporting. 

        onDeviceReady: function() {
          app.receivedEvent('deviceready');
          plugins.appBlade.setupAppBlade('[UUID]','[Token]', '[Secret]', '[Issued at]');
          plugins.appBlade.catchAndReportCrashes();
          plugins.appBlade.allowFeedbackReporting();
        },

See the Example projects included for examples using the other functions of the SDK.

##Installation - Android

1. Copy `AppBlade.js` into your `assets/www/js` directory.
<br/>*1a.* In your Package Explorer, expand your project and expand `assets` > `www` > `js`
<br/>*1b.* Drag `AppBlade.js` from the AppBlade Plugin Android folder into the `js` folder in your Package Explorer.
<br/>*1c.* Make sure "Copy files" is selected before selecting OK.
<br/>
<br/>
2. Copy `AppBladePlugin.java` into your project's package directory.
<br/>*2a.* In your Package Explorer, expand your project and expand src > [your.package.identifier] 
<br/>*2b.* Drag `AppBladePlugin.java` from the Android folder into the package in your `src` folder that you would like your plugin to be referenced from. This is usually the package that was created automatically ([your.package.identifier]). 
<br/>*2c.* Make sure "Copy files" is selected before selecting OK.
<br/>*2d.* In your project's copy of `AppBladePlugin.java`, change the package name from 'com.appblade.phonegappluginexample' to your package identifier.
<br/>
<br/>
3. Add the AppBlade SDK to your project. 
<br/>*(These directions are for adding the app blade framework jar, adding AppBlade source to a PhoneGap project is currently not supported)*
<br/>*3a.* Open your `libs` folder under your project in the Package Explorer. 
<br/>*3b.* Drag the included `appblade framework.jar` and `httpmime-4.1.2.jar` into the libs folder.
<br/>*3c.* Make sure "Copy files" is selected before selecting OK.
<br/>
<br/>
4. Ensure AppBlade.com is in Cordova's whitelist.
<br/>*4a.* Open your config.xml file and find the access element (the line `<access origin= ... />`). 
<br/>*4b.* If the `access` line is already `<access origin="*" />` Then nothing else needs to be done. ("*" means the whitelist is allowing all sources)
<br/>*4c.* If the `access` is not `<access origin="*" />` Then `<access origin="https://appblade.com" subdomains="true" />` will have to be added.
<br/>
<br/>
5. Add AppBlade to your list of plugins
<br/>*5a.* On Your Package Explorer, open your project's `config.xml` file in `res` > `xml` > `config.xml`
<br/>*5b.* Open the file with the text editor (right-click > `Open With...` > `Text Editor`, if necessary) and locate the plugins list element (the line `<plugins> ... </plugins>`). 
<br/>*5c.* Add `<plugin name="AppBlade" value="[your.package.identifier].AppBladePlugin"/>`  inside your list of plugins. `[your.package.identifier]` is where `AppBladePlugin.java` is stored in your project's packages.
<br/>
<br/>
6. Make AppBlade.js referenceable. 
<br/>*There are many ways to do this, as AppBlade.js can be treated jet like  any other js file. This is just an example:* 
<br/>*6a.* In your `index.html` file add `<script type="text/javascript" src="js/AppBlade.js"></script>` after the "cordova-2.5.0.js" script reference and before the "js/index.js" script reference:

        <script type="text/javascript" src="cordova-[2.5.0+].js"></script>
        <script type="text/javascript" src="js/AppBlade.js"></script>
        <script type="text/javascript" src="js/index.js"></script>
<br/>
7. Link your PhoneGap project to AppBlade.com  
  *7a.* To use AppBlade features the app must first exist on AppBlade (click [+ New Project] after signing in). Get   your project keys by navigating to your AppBlade project and selecting "Reveal your API Keys".
<br/>*7b.* In your `index.js`, underneath the `app.receivedEvent('deviceready');` call the setup method with your SDK keys in the order they appear on the AppBlade site: UUID, token, secret, issued at.
The following example sets up the app blade plugin with API keys (actual values not used), sets up the crash reporter, and sets up feedback reporting. 

        onDeviceReady: function() {
          app.receivedEvent('deviceready');
          plugins.appBlade.setupAppBlade('[UUID]','[Token]', '[Secret]', '[Issued at]');
          plugins.appBlade.catchAndReportCrashes();
          plugins.appBlade.allowFeedbackReporting();
        },

See the Example project included for examples using the other functions of the SDK.


##Resources:
###[AppBlade.com](https://appblade.com/)
###[AppBlade Support](https://support.appblade.com/)
###[License and Terms](https://appblade.com/terms_of_use)
