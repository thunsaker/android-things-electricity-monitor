# Electricity Monitor

For those who may not know, I live in South Africa, a country where we sometimes battle with electricity.  
Hey we even have a multitude of apps that give out ["load-shedding"](http://loadshedding.eskom.co.za/loadshedding/description) schedules. See [here](https://play.google.com/store/apps/details?id=com.ashwhale.sepush.eskom&hl=en) and [here](https://play.google.com/store/apps/details?id=com.news24.loadshedding&hl=en). 

While these apps serve a purpose, they are not so good when we have unplanned outages. 

Which often leaves me asking myself the following questions:

- Do I have power at home right now?
- If not, how long has the power been out for?
- Is it okay to eat the contents of my freezer? 

## Introducing "Electricity Monitor"... ##

<img src="art/power_on.png" alt="phone image" width="200px" />
<img src="art/power_off.png" alt="phone image" width="200px" />

I decided to use a Raspberry Pi 3 running Android Things and Firebase Realtime Database to monitor the electricity in my house. 

Mainly because Firebase has a *VERY* powerful tool for monitoring if a client is connected to your Realtime database or not. By leveraging the `onDisconnect()` method on the Firebase Realtime database, the server can automatically change some data (or log a time) when a client disconnects.  

To get the app working, do the following:

1. Checkout this repository.
2. Run the "app" project to a Raspberry Pi 3. Make sure the Raspberry Pi is connected to the internet.
3. Run the "companion-app" on your every day device. 
4. If you have electricity, you will see a house with lights on and the accumulated time you have had power for. 
5. If you don't have electricity, the Raspberry Pi will lose its power source and trigger the `onDisconnect()` callbacks on the Firebase server,this will then show up in our "companion-app" and the lights in the house will go off. 
It will then also display information about how long the electricity has been off for. 

## Setup Requirements
Before running the app, you need to:

1. Create a Firebase Project.
2. Download the google-service.json file from the Firebase Console to both the app folder and the companion-app folder
3. Set the Realtime database rules to be read and write for everyone (Firebase Console -> Database -> Rules)```
{
  "rules": {
    ".read": true,
    ".write": true
  }
}```
4. Deploy "app" to the Raspberry Pi or equivalent Android Things device.
5. Deploy "companion-app" to your phone. 

## Yes I know...
- There are easier ways to monitor your power at home
- This is basically monitoring my Pi's connection to the internet and not power, which in most cases will be accurate enough for me as I am hardly without internet. (I guess this could be rebranded as - "Do I have Internet at home?") 
- Yes there is *no* security on the database right now, luckily its not controlling my power. (pull requests are welcome :bowtie:) 
- This should probably be moved into a background service so it can run in the background. 
- You might not understand the need for this app, which is okay, it is useful for me and hopefully fellow South Africans :smile:

## References

- Building an Online Presence System using Firebase Realtime Database - https://firebase.googleblog.com/2013/06/how-to-build-presence-system.html
- Android Things Setup - https://developer.android.com/things/index.html
- Illustration from Vecteezy - https://www.vecteezy.com/vector-art/110154-vector-houses
