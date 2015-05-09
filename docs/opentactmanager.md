

2.OpentactManager
=======
---
The OpentactManager class is a singleton class, and application MUST create one and at most one of this class instance before it can do anything else, and similarly, once this class is destroyed, application must NOT call any library API. 
This class is the core class of Opentact, and it provides the following functions:

  * Starting up and shutting down
  * User agency of SIP and IM

##Preparation
Before instantiate the OpentactManager, you must do some preparation:

  * Get the [SID,SSID,AUTHTOKEN](http://opentact-api-documentation.readthedocs.org/en/latest/accounts.html)
  * Customization of configurations, such as Opentact configuration,SIP configuration,IM configuration.
  * Instantiating the OnSipCallback, you should implements the OnSipCallback to create your own callback class.
  
  e.g

```java
    public class MyOnSipCallback implements OnSipCallback
```
  
```java
    public static final String SID = "YOUR SID";
    public static final String SSID = "YOUR SSID"
	public static final String AUTHTOKEN = "YOUR AUTHTOKEN";
    public MyOnSipCallback myOnSipCallback = new MyOnSipCallback();
    public OpentactConfig cfg = new OpentactConfig();
    
    ...
    
    cfg.getSipConfig().setIceEnable(true);
    cfg.getSipConfig().setStunEnable(true);
	cfg.getSipConfig().setTurnEnable(true);
    
    ...
```
##Instantiating the OpentactManager

Call OpentactManager.startWork static method to start the opentact api:

```java
    opentactManager = OpentactManager.startWork(getApplicationContext(), SID, AUTHTOKEN, SSID, cfg, onSipCallback);
```

##Shutting Down the OpentactManager
Call opentactManager.stopOpentact() to shut down the library:

```java
    opentactManager.stopOpentact();
```

#Class Reference
---

##The OpentactManager

class OpentactManager

    OpentactManager represents an instance of opentact library.There can only be one instance of opentact library in an application, hence this class is a singleton.
    
####Public Functions

 `static OpentactManager`**`startWork`**`(Context ctx,String sid,String authToken,String ssid,OpentactConfig opentactConfig,OnSipCallback sipCallback)`
 
  &#160; &#160;Start the opentact library. Note that you must call it before calling any other method of opentact.
  
  &#160; &#160;**@Parameters**
  
  * `ctx`-<br>
  &#160; &#160;application context.

  * `sid`-<br>
    &#160; &#160;User master account's identifies of opentact. More detail seek from [**Opentact API**](http://opentact-api-documentation.readthedocs.org/en/latest/intro.html).

  * `authToken`-<br>
    &#160; &#160;Password of user master account.
 
  * `ssid`-<br>
    &#160; &#160;[**SubAccount Identifies**](http://opentact-api-documentation.readthedocs.org/en/latest/subaccounts.html) under user master account's identifies..

  * `opentactConfig`-<br>
    &#160; &#160;[**OpentactConfig**]().

  * `sipCallback`-<br>
    &#160; &#160;[**OnSipCallback**]().

`static OpentactManager `**`getInstance()`**
 
 &#160; &#160;Get OpentactManager instance.
 
 &#160; &#160;**@Return**<br>
 &#160; &#160;&#160; &#160;OpentactManger instance.

 `void `**`stopOpentact()`**
 
 &#160; &#160;Stop the opentact library.
 
`void `**`stopSipService()`**
 
 &#160; &#160;Stop the SIP service.
 
`SipService `**`getSipService()`**
 
 &#160; &#160;Get the SIP instance.
 
 &#160; &#160;**@Return**<br>
 &#160; &#160;&#160; &#160;a SIP instance.
 
 `IMService `**`getImService()`**
 
 &#160; &#160;Get the IM instance.
 
 &#160; &#160;**@Return**<br>
 &#160; &#160;&#160; &#160;a IM instance.
 
`void `**`answerCall()`**`
 
 &#160; &#160;Answer the incoming phone.
 
`void `**`hangupCall()`**`
 
 &#160; &#160;Hangup the incoming phone.
 
`void `**`setSipCodecPriority`**`(String codecID,short priority,boolean isDefault)`
 
 &#160; &#160;Change [**codecs**]() priority.
 
 &#160; &#160;**@Paramters**<br>
 &#160; &#160;`codecID`-<br>
 &#160; &#160;&#160; &#160;Codec ID, which is a string that uniquely identify the codec (such as “speex/8000/1”).
 &#160; &#160;`priority`-<br>
 &#160; &#160;&#160; &#160;Codec priority, 0-255, where zero means to disable the codec.
 &#160; &#160;`isDefault`-<br>
 &#160; &#160;&#160; &#160;if true, change codecs by Default.

`String[] `**`getCodecList()`**

&#160; &#160;Get the codecs which opentact support.

&#160; &#160;**@Return**<br>
&#160; &#160;&#160; &#160;a string array of codecs.

`void `**`makeCallToSSid`**`(String friend_ssid)`

&#160; &#160;make a call to friend.

&#160; &#160;**@Paramters**<br>
&#160; &#160;`friend_ssid`-<br>
&#160; &#160;&#160; &#160;[**Friend ssid**](http://opentact-api-documentation.readthedocs.org/en/latest/friends.html).

`void `**`makeCallToTermination`**`(String number)`

&#160; &#160;make a call to a phone.

&#160; &#160;**@Paramters**<br>
&#160; &#160;`number`-<br>
&#160; &#160;&#160; &#160;the number = [Country Codes](https://countrycode.org/) + phone number, such as '86 159xxxxxxxx'.

`void `**`addSipAccount`**`(String username,String password)`

&#160; &#160;Add a [**SIP Account**](http://opentact-api-documentation.readthedocs.org/en/latest/sip.html) to application.

&#160; &#160;**@Paramters**<br>
&#160; &#160;`username`-<br>
&#160; &#160;&#160; &#160;the SIP number.
&#160; &#160;`password`-<br>
&#160; &#160;&#160; &#160;the SIP password.

`void `**`imDoConnect`**`(IMCallback callback)`

&#160; &#160;Connect to IM server, before you call other IM method, you MUST successful connect to IM server.

&#160; &#160;**@Paramters**<br>
&#160; &#160;`callback`-<br>
&#160; &#160;&#160; &#160;use the callback to listener connect status.

` void `**`imPublish`**`(String friend_ssid,String msg,IMCallback callback)`

&#160; &#160;Send a message to your friend.

&#160; &#160;**@Paramters**<br>
&#160; &#160;`friend_ssid`-<br>
&#160; &#160;&#160; &#160;[**Friend ssid**](http://opentact-api-documentation.readthedocs.org/en/latest/friends.html).
&#160; &#160;`msg`-<br>
&#160; &#160;&#160; &#160;the message you want to send.
&#160; &#160;`callback`-<br>
&#160; &#160;&#160; &#160;use the callback to listener send status.

`void `**`imSubscribe`**`(IMCallback callback)`

&#160; &#160;Subscribe yourself so that others can send message to you.

&#160; &#160;**@Paramters**<br>
&#160; &#160;`callback`-<br>
&#160; &#160;&#160; &#160;use the callback to listener subscribe status.
