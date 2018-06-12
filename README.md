# Jamun-Volley

A set of Custom Classes with UI components for network programming, integration and transaction handling in a better and standard way. This will help developers for making quality use of volley library.

### Introduction

* In this Library Jamun-Volley, we provide you a package of custom Volley Classes which ease your work while working with API calls.
* You just need to setup all the configuration stuff (Like Header Meta-Data, Singleton Declarations this will be shown with example later in the documnet) at one place so that you don't have to write same piece of code again and again. For example, MyApplication Class.<br>
* Jamun-Volley library has been developed keeping many parameters in mind by default the library support many auto-configuration like LUR-Cache, Request and ImageLoader Objects. But in case if you need To Edit Something We have also provided you to edit Definations and setting up new configuration parameters.<br>
* One of the main benifit of using Jamun-Volley LIbrary is that you can Post Any type of data and Retrive response in another format which wasn't possible in traditional Volley Library.<br>
* THis Library also provide you File Downloading and Uploading classes which were upsent in Traditional Volley. With the help of this Library you can also manage of your file Downloading/Uploading progress easliy with Data Statistics.<br>
* Library's most attractives UI Feature is that you are provided with CircularNetworkImageView with the help of which you can display your image in Attractive Circullar View. By Just using CircularNetworkImageView.
* Library also provide you a UI Component to Show progress Data Statistics in Notification. But this also provide you a set of Function which help in Customization.<br>

### What's New? (0.0.1)
* Stable **Official Version** for Developers and Live Apps.
* Custom UI components for **Progress Notifications** with Infinite and Counted progress bar. Also have data analytics.
* Easy Calling Mechanism with **Instant reply** via Listeners and Return Functions
* **Lite version** for minimal code calls with maximum Auto APIs Calling features
* Need less calls with many customs methods to reach maximum developer satisfaction.

### Quality Measures? for (0.0.1)

The following apps are using this library without facing any kind of Bugs.

* **[SimplyBlood](https://play.google.com/store/apps/details?id=com.simplyblood)**
* **[ZINI](https://play.google.com/store/apps/details?id=ai.zini)**,
* **[USEonRENT](https://play.google.com/store/apps/details?id=ai.zini)** 
* **[Jumboo](https://play.google.com/store/apps/details?id=ai.jumboo)**
* **[USEonRENT](https://play.google.com/store/apps/details?id=com.useonrent)**
* **[QR/Barcode Scanner](https://play.google.com/store/apps/details?id=ai.scanners)** 
* **[Wall-E](https://play.google.com/store/apps/details?id=ai.hdwallpapers)**
* **[SaveBloodIndia](https://play.google.com/store/apps/details?id=com.savebloodindia)**
* **[Rectangle India](https://play.google.com/store/apps/details?id=com.rectangleindia.blooddonation)**
* **[Jeevan Rakshak](https://play.google.com/store/apps/details?id=com.jeevanrakshak)**

------

## Gradle Configuration

**Add the dependency**

```java
dependencies {
        compile 'tk.jamun:volley:0.0.1'
}
```

## Maven Config

```xml
<dependency>
  <groupId>tk.jamun</groupId>
  <artifactId>volley</artifactId>
  <version>0.0.1</version>
  <type>aar</type>
</dependency>
```
------

### Features and Functionalities

As you all familiar with Basic calls Required in Accessing JSON Data of Type,

* **JSONObject Request**
* **JSONArray Request**
* **String Request**

But this Library Provide you :

* **Network Response Request**
* **Response Request with Response in String and Network**

**Uploading**

* **Multipart Request for Payload**
* **HTTPConnection Request for Payload with Notifcaion**

**Downloading**

* **File Download Request for Payload**
* **Image Download Request for Image**
* **HTTPConnection Request for Payload with Notifcaion**

Also for used in Background Services like Services, IntentServices, AsynTasks

**Background Service Tasks** 

* **For Payload with Notifcaion**
* **For JSONObject**
* **For JSONArray**
* **For String**

Last but not Lease :
**Error Response**

* **With Status Code**
* **With Predefined Status Replies**

------

# How to Implement

Once the project has been added to gradle, You can use these lines of code to configure pickers...

## Step 1. Volley Setup

Library provide you a Better Approach and Efficent way to setup Google Volley Library, now you don't need to create Volely singleton or create a Setup of LRU Cache for File buffering or caching or many more things developer need to set first to start volley.
And last but not least, no need of creating header again and again for each APIs calls, this will done automatically with one function call define in  **Application** class for Global Access.

But here, these things are automate by calling some methods in **Application** class

```
 @Override
 public void onCreate() {
        super.onCreate();
        VolleySingleton.setInstance(mInstance);
        setAndRefreshVolleyHeaderCredentials();
 }
 // this function call required to setup or refresh your Header AuTH details from one place for whole further api calls.
 public void setAndRefreshVolleyHeaderCredentials() {
        VolleyNeeds.getInstance().setUpHeaders(ClassSharedPreference.getInstance().getHeaderCredentials());
 }
 
 //If you want to setup LRU cache Size
 VolleySingleton.setLruCacheSize(int lruCacher);
 
```

Method define in Sharepreference class for accessing AUth header Details.
Example after login or registeration, setup your auth Fundamental in SharedPrefrence and push refresh to set for Global Use 

```
public ArrayList<ModelHeader> getHeaderCredentials() {
    ArrayList<ModelHeader> headerArrayList = new ArrayList<>();
    headerArrayList.add(new ModelHeader(KEY_USER_ID, sharedPreferences.getString(KEY_USER_ID, null)));
    headerArrayList.add(new ModelHeader(KEY_TOKEN, sharedPreferences.getString(KEY_TOKEN, null)));
    headerArrayList.add(new ModelHeader(TAG,DATA));
    headerArrayList.add(new ModelHeader(TAG,DATA));
    headerArrayList.add(new ModelHeader(TAG,DATA));
    return headerArrayList;
}
```
Thats it. Your all setup is now Done in Two lines.

## Step 1. APIs integration with Jamun-Volley

As you all familiar with Basic calls Required in Accessing JSON Data, as you seen it have similar calling structure for Developer to feel familiar but with full advance automation,

* No need of Extra header calls
* No Need of Priority setup 
* No Need of Retry Policy Calls

* **JSONObject Request**
```
VolleyJsonObjectRequest jsonObjectRequest = new VolleyJsonObjectRequest(Request.Method.POST, url,
               @Nullable body, new VolleyResponse.Listener<JSONObject>() {
            @Override
            public void onResponse(JSONObject response) {
            }
        }, new VolleyResponse.ErrorListener() {
            @Override
            public void onErrorResponse(int statusCode, String errorMessage) {
                MySnackBar.showSnackBarForMessage(activity, statusCode, errorMessage);
            }
        });
        VolleyNeeds.getInstance().setVolleyExtraCalls(jsonObjectRequest);  
        
// for Get Request
VolleyJsonObjectRequest jsonObjectRequest = new VolleyJsonObjectRequest(url,
             new VolleyResponse.Listener<JSONObject>() {....

```
* **JSONArray Request**
```
VolleyJsonArrayRequest jsonArrayRequest = new VolleyJsonArrayRequest(Request.Method.POST, url,
               @Nullable body, new VolleyResponse.Listener<JSONArray>() {
            @Override
            public void onResponse(JSONArray response) {
            }
        }, new VolleyResponse.ErrorListener() {
            @Override
            public void onErrorResponse(int statusCode, String errorMessage) {
                MySnackBar.showSnackBarForMessage(activity, statusCode, errorMessage);
            }
        });
        VolleyNeeds.getInstance().setVolleyExtraCalls(jsonArrayRequest);    

// for Get Request
VolleyJsonArrayRequest jsonArrayRequest = new VolleyJsonArrayRequest(url,
             new VolleyResponse.Listener<JSONArray>() {....

```

* **String Request**

```
VolleyStringRequest volleyStringRequest = new VolleyStringRequest(Request.Method.POST, url,
               @Nullable body, new VolleyResponse.Listener<JSONArray>() {
            @Override
            public void onResponse(JSONArray response) {
            }
        }, new VolleyResponse.ErrorListener() {
            @Override
            public void onErrorResponse(int statusCode, String errorMessage) {
                MySnackBar.showSnackBarForMessage(activity, statusCode, errorMessage);
            }
        });
        VolleyNeeds.getInstance().setVolleyExtraCalls(volleyStringRequest);    
```

* **Network Response Request**
```
 VolleyNetworkRequest volleyNetworkRequest = new VolleyNetworkRequest(Request.Method.POST, URL,
                @Nullable body, new VolleyResponse.Listener<Integer>() {
            @Override
            public void onResponse(Integer response) {
                if (VolleyNeeds.getInstance().checkResponseCode(response)) {
                    // for response between 200 to 300
                } else {
                    MySnackBar.showSnackBarForMessage(ActivityProfileChange.this, R.string.connection_something_went_wrong);
                }
            }
        }, new VolleyResponse.ErrorListener() {
            @Override
            public void onErrorResponse(int statusCode, String errorMessage) {
            }
        });
        VolleyNeeds.getInstance().setVolleyExtraCalls(volleyNetworkRequest);
```

* **Response Request**
```
VolleyResponseRequests volleyStringRequest = new VolleyResponseRequests(Request.Method.POST, url,
               @Nullable body, new VolleyResponse.Listener<String>() {
            @Override
            public void onResponse(String response) {
            }
        },new VolleyResponse.Listener<Integer>() {
            @Override
            public void onResponse(Integer response) {
                if (VolleyNeeds.getInstance().checkResponseCode(response)) {
                    // for response between 200 to 300
                } else {
                    MySnackBar.showSnackBarForMessage(ActivityProfileChange.this, R.string.connection_something_went_wrong);
                }
            }
        }, new VolleyResponse.ErrorListener() {
            @Override
            public void onErrorResponse(int statusCode, String errorMessage) {
                MySnackBar.showSnackBarForMessage(activity, statusCode, errorMessage);
            }
        });
        VolleyNeeds.getInstance().setVolleyExtraCalls(volleyStringRequest);    
```

* **Multipart File Uploading Request**
```
// Setup calls for setting file for Uploadind
Map<String, ModelByPart> params = new HashMap<>();

// params.put(TAG,new ModelByPart(FileName,fileDataFromBitmap,"image/"+ext.));
params.put(API_TAG, new ModelByPart(file.getName(),    VolleyHelper.getFileDataFromBitmap(BitmapFactory.decodeFile(mCurrentPhotoPath.getAbsolutePath())),
                        "image/" + file.getName().substring(file.getName().lastIndexOf(".") + 1).toLowerCase()));
                        
VolleyMultipartRequest multipartRequest = new VolleyMultipartRequest(URL, params,
     new VolleyResponse.Listener<String>() {
         @Override
         public void onResponse(String response) {
                    
    }, new VolleyResponse.ErrorListener() {
            @Override
            public void onErrorResponse(int statusCode, String errorMessage) {
                utilityClass.closeProgressDialog();
                MySnackBar.showSnackBarForMessage(ActivityProfileChange.this, statusCode, errorMessage);
            }
        });
VolleyNeeds.getInstance().setVolleyExtraCalls(multipartRequest);
   
```
* **Last Call to setup Request for Execution is By**

```
        VolleyNeeds.getInstance().setVolleyExtraCalls(jsonObjectRequestSetAvatar);    
```

* **Volley in Background Service**

Jamun Volley Background Services provide you a better and efficent approach to Upload or Download data payloads in background tasks.
It will help developers to maintain session during payload uploading and downloading. This will return result after complete execution, so no need to maintain another threads for waiting response.

There are different types to use **Jamun-Volley** in Background Tasks :-

1. **Get Request**

```
String response = VolleyBackgroundServices.getInstance().volleyToGetData(URL, new VolleyResponse.ErrorListener() {
            @Override
            public void onErrorResponse(int statusCode, String errorMessage) {
                //Error Response
            }
        });
```
2. **Post Request**

```
String response = VolleyBackgroundServices.getInstance().volleyToSendData(URL, payload,new VolleyResponse.ErrorListener() {
            @Override
            public void onErrorResponse(int statusCode, String errorMessage) {
                //Error Response
            }
        });
```
3. **Get Post Request**

```
//integer Methods are Request.Method.POST,Request.Method.GET,Request.Method.DELETE,Request.Method.UPDATE
String response = VolleyBackgroundServices.getInstance().volleyToGetPostData(Method,URL, payload,new VolleyResponse.ErrorListener() {
            @Override
            public void onErrorResponse(int statusCode, String errorMessage) {
                //Error Response
            }
        });
```
4. **Upload File**

```
//Methods are Request.Method.POST,Request.Method.GET,Request.Method.DELETE,Request.Method.UPDATE
// Tag name used for uploading file with API tag
String response = VolleyBackgroundServices.getInstance().volleyToSendFile(File, Method, URL, tagName,new VolleyResponse.ErrorListener(){
            @Override
            public void onErrorResponse(int statusCode, String errorMessage) {
                //Error Response
            }
        });
```
5. **Close In-Between**

Using this method, help you stoping APIs call in between;

```
VolleyBackgroundServices.getInstance().stopServices();
```
* **HTTPConnection Request for Payload with Notifcaion**

1. **Uploading File**
```
    /**
     * Method helps you uploading heavy files with HttpURLConnection request. Method required AsyncTasks or Service to handle uploading;
     * Otherwise thrown NetworkOnMainThreadException
     * @param url Request URL for Upload payload
     * @param sourceFile Source file need to be Upload
     * @param helperNotification HelperNotification class for Notified user by Progress Notification
     * @param notificationId Unique id for Progress Notification
     * @return APIs response
     */
String response = VolleyDownUpFiles.getInstance().uploadFile(URL, SourceFile, HelperNotification, notificationId);
```
2. **Downloading File**
```
    /**
     * Method helps you downloading heavy files with HttpURLConnection request. Method required AsyncTasks or Service to handle uploading;
     * Otherwise thrown NetworkOnMainThreadException
     * @param requestUrl Request URL for Upload payload
     * @param filePath Download file need to be Saved
     * @param helperNotification HelperNotification class for Notified user by Progress Notification
     * @param notificationId Unique id for Progress Notification
     * @return APIs response
     */
String response = VolleyDownUpFiles.getInstance().downloadFile(URL, filePath, HelperNotification, notificationId);
```
3. **Stop Service**
```
VolleyDownUpFiles.getInstance().stop();
```
4. **Customize Buffer Size**

Different file have differnt size in Uploading, this required volley to create a buffer to maintain file in Uploading Tasks;
Need to be set according to mean of the Files Size to stop MemoryBufferSizeException;

```
VolleyDownUpFiles.getInstance().stop();
```

# Dependency

* Android Volley ``v1.1.0``
* Java jar ``org.apache.http.legacy.jar``

## Credits

Desgin & Developed by : **[Jatin Sahgal](https://www.linkedin.com/in/jatinsahgal/)**
 (**[Linkedin](https://www.linkedin.com/in/jatinsahgal/)** & **[Website](https://blog.jamun.tk)**) 

# Live Project using this Library

The following apps are using this library without facing any kind of Bugs.

* **[SimplyBlood](https://play.google.com/store/apps/details?id=com.simplyblood)**
* **[ZINI](https://play.google.com/store/apps/details?id=ai.zini)**
* **[LifeMantra](https://play.google.com/store/apps/details?id=com.lifemantra)**
* **[Wall-E](https://play.google.com/store/apps/details?id=ai.hd.wallpaper)**
* **[Jumboo](https://play.google.com/store/apps/details?id=com.doubtzone)**
* **[SaveBloodIndia](https://play.google.com/store/apps/details?id=com.savebloodindia)**
* **[Rectangle India](https://play.google.com/store/apps/details?id=com.rectangleindia.blooddonation)**
* **[Jeevan Rakshak](https://play.google.com/store/apps/details?id=com.jeevanrakshak)**

## More Library under Jamun 
* **[Pickers](https://github.com/Lib-Jamun/Pickers.git)**
Pickers Library provide you a set of Pickers like Country, Language, Share and Intent Chooser.

* **[Country-Pickers](https://github.com/Lib-Jamun/Pickers.git)**
allow you to access Country picking functionality with great UI/UX design, and there are numberous of function which help you to modify picker as per your requirements. Library has been provided with four custom UI initate mode you can decide how the view of picker can be initate. You can also decide weather picker inheriate Single or Multi Selection property. Library consists of updated collection of country name, code and there flags. We are using APIs base structure to avoid increase in the size of apk due to flag Images. This module Maintain the database so that you don't need to call APIs again and again rather than you can choose when to refresh the Database and fetch new real time data.

* **[Language-Pickers](https://github.com/Lib-Jamun/Pickers.git)**
provides you read-made Language picker  which is easy to use and comes with great UI/UX, and there are numberous of function which help you to modify picker as per your requirements. Library has been provided with four custom UI initate mode you can decide how the view of picker can be initate. You can also decide weather picker inheriate Single or Multi Selection property.

* **[Scanner](https://github.com/Lib-Jamun/scanner.git)**
is a collection of Beautiful Activity which help others to make there own Custom QR/Barcode Scanner. 

* **[Calendar](https://github.com/Lib-Jamun/calendar.git)**
is a collection of Beautiful Activities which help others to make there Fully Custom Calendar View with Single and Multi Date Picker Functionality 

* **[UI](https://github.com/Lib-Jamun/ui.git)**
library is a set of UI Views, Custom Component and Collection of Helper Classes which help Developer for making quality Product. Such as Camera, Gallery, Number of Pickers, Calendar, Date Pickers, Dialogs and many more Heler UI and Backend Component.

* **[Camera](https://github.com/Lib-Jamun/ui.git)**
library provide you Custom Complete Camera view with full features like Flash, Rotation, Gallery Picker, Focus, Tap to capture, Confirmation window and last but not least croping feature. It also provide you file path in return so that developer can feel a friendly handy way to Deal After. 

* **[Gallery](https://github.com/Lib-Jamun/ui.git)**
have some Beautiful UI Components and Multi files Mode for android Developers to give there app a A Rich look With single and Multi picker Functionality.

* **[Elements](https://github.com/Lib-Jamun/elements.git)**
Library provide you a custom set of Android Elements that have custom views and properties like CircularImageView or CircularNetworkImageView and many more.

* **[Browser](https://github.com/Lib-Jamun/Browser.git)**
Library provide you two type Single Pager and Multi Pager In-APP Browser Functionality with Event Handling and Functions to Customize Views. It also provide you Copy to clipboard, Open in Browser and share link feature in-Bulit.

## License
    Copyright (c) 2018 Jatin Sahgal

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
