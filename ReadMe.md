**Smart Home**

This code in this repository gets the temperature and humidity data from Windows IOT Core Raspberry Pi at the interval set by the user and adds it to the Azure table storage via an App Service hosted in the Azure cloud.

This also has a Xamarin Forms based app that downloads data from the service and displays it as a graph using Syncfusion.

Apart from obtaining the data from the cloud, the App enables user to turn the display on the Raspberry Pi On/Off from the phone. This is done using SignalR technology. The user can be anywhere on the internet.

Keep in mind that this is WORK IN PROGRESS.

It has minimal authentication, no transient fault handling and it uses direct calls to the REST API service instead of using any IotHub or a Service bus. So this can be useful for quick learning and building fun project; but it does not have production quality robustness.

In order to build it, open SmartHome.sln using VS 2017 Restore all the packages and then perform the build. You would want to change the appropriate parameters (marked with YOUR word)

This will build the REST API service and the Raspberry Pi App. You can run the Raspberry Pi app locally on your Windows 10 machine in simulator mode. In the simulator mode, it can generate random data and update the storage table using the REST API service.

Here are the Modules in brief.

**HomeHub.Model**

This is a portable class library that hosts models that transfer between the client apps (Xamarin Forms and Windows Core IOT) and the REST API.

**HomeHubClient**

This is a portable class library that provides typed REST API client for the backend service. It takes care of translating the models and adding authentication parameters.

_***Note:***_
This project is common to both Windows 10 IoT Core and the Xamarin App. However, when compiling for IoT core, use 6.0.4 version of the Newtonsoft library and when compiling for Xamarin App, use 10.0.3 version of the library. Other versions have loading issues on the respective platforms. Please (un)comment lines in the packages.config accordingly. If you find any cure, please share it.

**SmartHomePiApp**

This is a Windows 10 IOT Core UWP app that obtains data from the SenseHat and uploads to the cloud using the Client library and the model library. This can also act in the simulation mode. So you can run it with no Raspberry Pi.

**SmartHomeRESTAPI**

This is the REST API service hosted on the cloud or as localhost. It is ago between the Azure storage and the client. It also provides authentication mechanism.

-----------------
To build Mobile + UWP App(s), open SmartHomeApp.sln from the SmartHomeApp folder.
Make sure, there is right version of Newtonsoft. Restore all the packages. And perform the build

**SmartHomeApp**

It is a Xamarin Forms based App that uses MVVM and Command pattern. It obtains the data using HomeHub.Model and HomeHubClient modules. It is displayed using Synfusion chart.





