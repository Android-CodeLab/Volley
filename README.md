# Jamun-Volley (Advance Volley)

A set of Custom Classes with UI components for network programming, integration and transaction handling in a better and standard way. This will help developers for making quality use of volley library.

### What's New? (0.0.7)
* No more **BoilerCodes** Write Small and Easy Understandable Code,
* No need to **Write Header** Everywhere, just See the Implementation of writing setup on MyApplication Class,
* No need of **JSON Parsing** Using POJO, Volley is now available with **Auto Parsing JSON**
* Defined Error Controllers and Listener with Pre Defined **Messages & Network Status Code**
* **Image Uploading** Framework using Volley Customs
* **Image Compressing** Helper Classes Before Uploading Images with Custom Parameters
* **VolleyResponses** Listener Which provide Desired Result on Both Demanding **POJO CLass and String** with Different Error Listeners as well as you have Default Listeners to Use.
* Available with Uploading & Downloading Notification Handler
* No Need to Write Hasmap or JSONObject() before Put/POST, just include your POJO file and Get Desired Result
* **Lite version** for minimal code calls with maximum Auto APIs Calling features
* Easy Calling Mechanism with **Instant reply** via Listeners and Return Functions
* Customize LCache and Volley Retry Policies with single place implementations.
* Available with Androidx & Kotlin Support with Latest Google Volley 1.1.1 Update.

### Quality Measures? for (0.0.7)

The following apps are using this library without facing any kind of Bugs.

* **[SimplyBlood](https://play.google.com/store/apps/details?id=com.simplyblood)**
* **[ZINI](https://play.google.com/store/apps/details?id=ai.zini)**,
* **[RentalBazar](https://play.google.com/store/apps/details?id=com.rentalbazaar)** 
* **[DoubtCrusher](https://play.google.com/store/apps/details?id=com.doubtcrusher)**
* **[BookAGround](https://play.google.com/store/apps/details?id=com.bookaground)**
* **[PeyFree](https://play.google.com/store/apps/details?id=com.peyfree)**
* **[ClueRace](https://play.google.com/store/apps/details?id=com.cluerace)**
* **[QR/Barcode Scanner](https://play.google.com/store/apps/details?id=com.scanner.android)** 
* **[Wall-E](https://play.google.com/store/apps/details?id=com.walle.android)**

------

## Gradle Configuration

**Add the dependency**

```java
dependencies {
        compile 'tk.jamun:volley:0.0.7'
}
```

## Maven Config

```xml
<dependency>
  <groupId>tk.jamun</groupId>
  <artifactId>volley</artifactId>
  <version>0.0.7</version>
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
* **Image Loader equest**


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
* **With Volley Error Class**

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
        VolleyNeeds.getInstance().setUpHeaders(ClassSharedPreference.getHeaderCredentials());
 }
 
 //If you want to setup LRU cache Size
 VolleySingleton.get().setLruCacheSize(int lruCacher);
 VolleyValues.get().setImageCompressionType(Bitmap.CompressFormat.JPEG)
 VolleyValues.get().setImageCompressionValue(100) -> 0 to 100(Full Quality)
 
```

Method define in Sharepreference class for accessing AUth header Details.
Example after login or registeration, setup your auth Fundamental in SharedPrefrence and push refresh to set for Global Use 

```
public ArrayList<ModelHeader> getHeaderCredentials() {
    ArrayList<ModelHeader> headerArrayList = new ArrayList<>();
    headerArrayList.add(new ModelHeader(KEY_USER_ID, sharedPreferences.getString(KEY_USER_ID, null)));
    headerArrayList.add(new ModelHeader(KEY_TOKEN, sharedPreferences.getString(KEY_TOKEN, null)));
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
Advance POJO Implementation
class Model{
   @SerializeName("first_name")
   String firstName;
   @SerializeName("last_name")
   String lastName;
   @SerializeName("gender")
   int gender;
   @SerializeName("date_of_birth")
   String dob;
   //Getter Setter
}
```

```
//Get Request Implementatino
VolleyJsonObjectRequest jsonObjectRequest = new VolleyJsonObjectRequest(url, Model.class, new VolleyResponse(){
       //Implement For Response (Model Class)
       @override void onResponse(Object response) {
                super.onResponse(response)
                if(response instanceOf Model){
                  Model model = (Model) response
                }
       }    
       //Implement For Response (Model) with String
       @override void onResponse(Object response, String responseBody) {
                super.onResponse(response, data)         
       }    
       //Implement for Error Response in all kind
       @override void onErrorResponse(VolleyError error, int statusCode, String errorMessage) {
                super.onErrorResponse(error, statusCode, errorMessage)
       }
       //Implement for Error on Status Code and Error
       @override void onErrorResponse(int statusCode, String errorMessage) {
                super.onErrorResponse(error, statusCode, errorMessage)
       }
       //Implement For Volley Error class on Errror
       @override void onErrorResponse(VolleyError error) {
                super.onErrorResponse(error, statusCode, errorMessage)
       }
}); 
VolleyNeeds.get().addCalls(jsonObjectRequest);  
```

```
//Post Implementation
Model model= new Model();
model.setFirstName("Jatin");
model.setLastName("Sahgal");
model.setGender(1);//1-Male, 2-Female
model.setDob("16/12/1995");

//Post Request
VolleyJsonObjectRequest jsonObjectRequest = new VolleyJsonObjectRequest(url, model, VolleyGson.get().getTypeToken(new TypeToken<Model>(){}),
    new VolleyResponse(){
       //Implement For Response (JSONOBject) with String
       @override void onResponse(Object response, String responseBody) {
                super.onResponse(response, data)
                if(response instanceOf JSONobject){
                }                
       }
});
VolleyNeeds.get().addCalls(jsonObjectRequest);  
```

```
//Get + Post Request Using
VolleyJsonObjectRequest jsonObjectRequest = new VolleyJsonObjectRequest(url, model, VolleyGson.get().getTypeToken(new TypeToken<Model>(){}),
    new VolleyResponse(){});

JSONObject stringBody = new JSONObject()
VolleyJsonObjectRequest jsonObjectRequest = new VolleyJsonObjectRequest(url,Model.class, stringBody.toString(),
    new VolleyResponse(){});


// For Post Request
VolleyJsonObjectRequest jsonObjectRequest = new VolleyJsonObjectRequest(url, stringBody, new VolleyResponse(){});

// For Delete Request
VolleyJsonObjectRequest jsonObjectRequest = new VolleyJsonObjectRequest(Request.Method.DELET, url, new VolleyResponse(){});

// For Other Request
VolleyJsonObjectRequest jsonObjectRequest = new VolleyJsonObjectRequest(Request.Method.PUT,url, stringBody, new VolleyResponse(){});
```

```
//Post Request
VolleyJsonObjectRequest jsonObjectRequest = new VolleyJsonObjectRequest(url, model, VolleyGson.get().getTypeToken(new TypeToken<Model>(){}),
    new VolleyResponse(){
       //Implement For Response (JSONOBject) with String
       @override void onResponse(Object response, String responseBody) {
                super.onResponse(response, data)
                if(response instanceOf JSONobject){
                }                
       }
});
VolleyNeeds.get().addCalls(jsonObjectRequest);  

//Old Implementation 
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
        VolleyNeeds.get().addCalls(jsonObjectRequest);          
        
// for Get Request
VolleyJsonObjectRequest jsonObjectRequest = new VolleyJsonObjectRequest(url,
             new VolleyResponse.Listener<JSONObject>() {....

```
* **JSONArray Request**
```

//Get Request Implementatino
VolleyJsonArrayRequest jsonArrayRequest = new VolleyJsonArrayRequest(url, Model[].class, new VolleyResponse(){
       //Implement For Response (Model Array Class)
       @override void onResponse(Object response) {
                super.onResponse(response)
                Model[] model = (Model[]) response
       }    
       //Implement For Response (Model Array Class) with String
       @override void onResponse(Object response, String responseBody) {
                super.onResponse(response, data)         
       }    
       //Implement for Error Response in all kind
       @override void onErrorResponse(VolleyError error, int statusCode, String errorMessage) {
                super.onErrorResponse(error, statusCode, errorMessage)
       }
       //Implement for Error on Status Code and Error
       @override void onErrorResponse(int statusCode, String errorMessage) {
                super.onErrorResponse(error, statusCode, errorMessage)
       }
       //Implement For Volley Error class on Errror
       @override void onErrorResponse(VolleyError error) {
                super.onErrorResponse(error, statusCode, errorMessage)
       }
}); 
VolleyNeeds.get().addCalls(jsonArrayRequest);  
```

```
//Post Request (Model[] in response or Type Token)
Model[] models= new Model[4];
VolleyJsonArrayRequest jsonArrayRequest = new VolleyJsonArrayRequest(url, models, VolleyGson.get().getTypeToken(new TypeToken<Model[]>(){}),
    new VolleyResponse(){
       //Implement For Response (Model Array Class) with String
       @override void onResponse(Object response, String responseBody) {
                super.onResponse(response, data)
                if(response instanceOf JSONobject){
                       Model[] model = (Model[]) response
         }                
       }
});
VolleyNeeds.get().addCalls(jsonArrayRequest);  

//Old Implementation 
VolleyJsonArrayRequest jsonArrayRequest = new VolleyJsonArrayRequest(Request.Method.POST, url,
               @Nullable body, new VolleyResponse.Listener<JSONArray>() {});
        VolleyNeeds.get().addCalls(jsonArrayRequest);    

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
        VolleyNeeds.get().addCalls(volleyStringRequest);    
```

* **Network Response Request**
```
 //Post Request (Model[] in response or Type Token)
Model[] models= new Model[4];
VolleyNetworkRequest volleyNetworkRequest = new VolleyNetworkRequest(Request.Method.POST, URL, models, VolleyGson.get().getTypeToken(new TypeToken<Model[]>(){}),
    new VolleyResponse(){
       //Implement For Response (Model Array Class) with String
       @override void onStatusCodeResponse(Integer statusCode) {
                super.onStatusCodeResponse(statusCode)
       }
       //Implement for Error Response in all kind
       @override void onErrorResponse(VolleyError error, int statusCode, String errorMessage) {
                super.onErrorResponse(error, statusCode, errorMessage)
       }
       //Implement for Error on Status Code and Error
       @override void onErrorResponse(int statusCode, String errorMessage) {
                super.onErrorResponse(error, statusCode, errorMessage)
       }
       //Implement For Volley Error class on Errror
       @override void onErrorResponse(VolleyError error) {
                super.onErrorResponse(error, statusCode, errorMessage)
       }        
});
VolleyNeeds.get().addCalls(jsonArrayRequest); 
```

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
        VolleyNeeds.get().addCalls(volleyNetworkRequest);
```


* **Multipart File Uploading Request**
```
// Setup calls for setting file for Uploadind
Map<String, ModelByPart> params = new HashMap<>();

// params.put(TAG,new ModelByPart(FileName,fileDataFromBitmap,"image/"+ext.));
params.put(API_TAG, new ModelByPart(file.getName(),    VolleyHelper.getFileDataFromBitmap(BitmapFactory.decodeFile(mCurrentPhotoPath.getAbsolutePath())),
                  MimeTypeMap.getFileExtensionFromUrl(file.getAbsolutePath()));
                        
VolleyMultipartRequest multipartRequest = new VolleyMultipartRequest(URL, params,
     //Implement For Response (Model Array Class) with String
       @override void onResponse(Object response, String responseBody) {
                super.onResponse(response, data)         
       }                
   //Use this only Implement for Error Response in Image Uploading
       @override void onErrorResponse(VolleyError error, int statusCode, String errorMessage) {
                super.onErrorResponse(error, statusCode, errorMessage)
       }
   });
VolleyNeeds.get().addCalls(multipartRequest);
   
```
* **Last Call to setup Request for Execution is By**

```
        VolleyNeeds.get().addCalls(volleyJsonObjects);    
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

* Android Volley ``v1.1.1``
* GSON Lib

## Credits

Desgin & Developed by : **[Jatin Sahgal](https://www.linkedin.com/in/jatinsahgal/)**
 (**[Linkedin](https://www.linkedin.com/in/jatinsahgal/)** & **[Website](https://blog.jamun.tk)**) 

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

* **[Camera](https://github.com/Lib-Jamun/camera.git)**
library provide you Custom Complete Camera view with full features like Flash, Rotation, Gallery Picker, Focus, Tap to capture, Confirmation window and last but not least croping feature. It also provide you file path in return so that developer can feel a friendly handy way to Deal After. 

* **[Gallery](https://github.com/Lib-Jamun/gallery.git)**
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
