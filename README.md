# Cordova Plugin for Start.io (ex. StartApp) Ads
### This if fork from <a href="https://github.com/lreiner/cordova-plugin-startapp-ads">Cordova Plugin for StartApp Ads</a>

### This version is incompleate. This plugin can only show banner ads. 
### If you able to find issue why this plugin is not showing Interstitial and Rewarded ads - I will be very grateful 
### At this moment this plugin is working on test mode. 

### 1. Installation
First you need to install the cordova plugin in your Cordova Project

```
cordova plugin add https://github.com/valesios/cordova-plugin-startio-ads.git
```

### 2. Setup the Plugin
To start declare the Plugin below your imports:
**NOTE: This must be declared in every Page where you want to use Start.io Ads!**
```javascript
var StartAppAds;
```
Now you need to init your Plugin with your App ID from Start.io first.
```javascript
this.platform.ready().then(() => {
  if(this.platform.is("android")) {
    StartAppAds.init("<your-android-app-id>");
  }
});
```
Now you can use StartAppAds everywhere in your project.

### 3. Show/Hide Banner Ads
Show a Banner Ad on the bottom of your app. 
```javascript
StartAppAds.showBanner();
```
Hide the Banner
```javascript
StartAppAds.hideBanner();
```
Events you can subscribe to (recommended to put it in the **constructor** of any page):
```javascript
document.addEventListener('startappads.banner.load', () => {
  //banner has been loaded and displayed.
  //do something here
});

document.addEventListener('startappads.banner.load_fail', () => {
  //banner failed to load
  //do something here
  //IMPORTANT: if banner failed to load dont use StartAppAds.showBanner(); again. 
  //StartAppAds will load a new one by itself!
});

document.addEventListener('startappads.banner.clicked', () => {
  //banner has been clicked
  //do something here. Usefull to hide banner to prevent click bombing.
});

document.addEventListener('startappads.banner.hide', () => {
  //banner has been removed
  //do something here
});
```
### 4. Show Interstitial Ads
Show a Interstitial Ad:
```javascript
StartAppAds.showInterstitial();
```
Events you can subscribe to (recommended to put it in the **constructor** of any page):
```javascript
document.addEventListener('startappads.interstitial.closed', () => {
  //interstitial closed by user
  //do something here
});

document.addEventListener('startappads.interstitial.displayed', () => {
  //interstitial showed up
  //do something here
});

document.addEventListener('startappads.interstitial.clicked', () => {
  //interstitial clicked by user
  //do something here
});

document.addEventListener('startappads.interstitial.not_displayed', () => {
  //interstitial loaded and ready but somehow not showed to user
  //do something here
});

document.addEventListener('startappads.interstitial.load_fail', () => {
  //interstitial failed to load
  //do something here
});
```
#### IMPORTANT:
```
Do not call `showInterstitial()` from within `load_fail` event. 
The SDK will automatically try to reload an ad upon a failure.
```

### 5. Show Rewarded Video Ads
Show a Rewarded Video Ad:
```javascript
StartAppAds.showRewardVideo();
```
Events you can subscribe to (recommended to put it in the **constructor** of any page):
```javascript
document.addEventListener('startappads.reward_video.reward', () => {
  //user watched video reward can be given now
  //do something here
});

document.addEventListener('startappads.reward_video.load', () => {
  //reward video finished loading
  //do something here
});

document.addEventListener('startappads.reward_video.closed', () => {
  //user closed video reward 
  //do something here
});

document.addEventListener('startappads.reward_video.clicked', () => {
  //user click on video reward 
  //do something here
});

document.addEventListener('startappads.reward_video.load_fail', () => {
  //reward video failed to load. Probably no Ads available at the moment
  //do something here
});
```
