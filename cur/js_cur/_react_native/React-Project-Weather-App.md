# React Native Projects

We encourage you to implement your own ideas or recreate any mobile app you want (talk to us to discuss it and confirm) otherwise maybe you will choose something from the list below...


> A boilerplate with navigation and several views: https://gitlab.com/barcelonacodeschool/native_template

> Example of push notifications: https://gitlab.com/gk3000/expoPushNotificationsExample

> Example of Stripe payments: https://gitlab.com/barcelonacodeschool/stripe-rn

## Some useful packages

* expo-location  ( get current position https://docs.expo.dev/versions/latest/sdk/location/ )
* react-native-google-places-autocomplete ( cities autocomplete input https://www.npmjs.com/package/react-native-google-places-autocomplete)
* react-native-elements ( react native components https://reactnativeelements.com/)
* react-native-paper ( react native components https://reactnativepaper.com/)
* @react-navigation/native ( navigation library https://reactnavigation.org/)
* @react-native-community/datetimepicker ( date and time picker input https://www.npmjs.com/package/@react-native-community/datetimepicker)
* @react-native-async-storage/async-storage ( react native version of the local storage https://www.npmjs.com/package/@react-native-async-storage/async-storage )
* react-native-maps ( display maps for react native https://github.com/react-native-maps/react-native-maps )
* react-native-chart-kit ( charts https://www.npmjs.com/package/react-native-chart-kit )


# Some ideas for the projects

## Weather App

**Create a weather forecast app according to the following requirements:**

1. it has to display the local  temperature on page load, based on the location of the device.
2. it has to have an input that can be used to search for the weather by city name.
3. you need to be able to see the weather-forecast  for at least one week.
4. it needs to have auto suggestions for the city while typing (look into google autocomplete API)
5. for this exercise you will need to use external APIs.
6. You need to have this in github from the very beginning and keep it up to date so that we can check your progress from your repo.
7. The weather could be displayed in Celsius or Fahrenheit

You will need to use OpenWeatherMap and Google Autocomplete and learn how to use them by reading the documentation of the APIs.

This should be the valid API key for OpenWeatherMap: 16909a97489bed275d13dbdea4e01f59 

You can do other google search but not look for a tutorial on how to make a weather app as this would defeat the purpose of the exercise.




<div class='screens_container'>
	<!-- ![](../pics/weather_app.png)   -->
	<img src="https://barcelonacodeschool.com/files/pics/weather_app_mobile_main.jpeg" alt="weather app screenshot" class='mobile_screen'>
	<!-- ![](../pics/weather_app_2.png) -->
	<img src="https://barcelonacodeschool.com/files/pics/weather_app_mobile_city_choice.jpeg" alt="weather app screenshot" class='mobile_screen'>
</div>

## Shopping list

A user can enter items to buy, delete them, mark as completed. 

Create/delete categories for the shopping -- like grocery, homeware, etc...

List of favorites where user can add frequently bought items and quickly re-add them to the current list 

As an extra make shared lists with other users (will require to use the server)

## Hangman game 

Classic word game 

## Currency converter

Could be done with automatic detection of user's current location and suggesting to convert to/from the local currency based on that

## Trivia game 

A set of questions/answers with score, highest score, trivia topics, etc...

## Reminder app

Add reminders and get notifications on a provided date. 

This project will require a server with scheduled jobs to run through the DB of reminders and sending user a push notifications. 

Node scheduler: https://www.npmjs.com/package/node-cron

Push notifications: https://docs.expo.io/push-notifications/overview/

Sample repo of push notifications: https://gitlab.com/gk3000/expoPushNotificationsExample

<!-- ## Citizen reports

The idea for this app is that users can report something happenning in the city with location mark and optional pictures uploaded. This events are displayed on the map so that at the same time any user can see what is hapenning around their actual location. 

This app is using maps API and needs a server to keep data about every event -- coordinates, description text and optional picture (which could be stored at Cloudinary). 

Below are some screenshots of similar app.


<div class='screens_container'>
	<img src="https://barcelonacodeschool.com/files/pics/cur_files/citizen_reports_9181.jpg" alt="weather app screenshot" class='mobile_screen'>
	<img src="https://barcelonacodeschool.com/files/pics/cur_files/citizen_reports_9182.jpg" alt="weather app screenshot" class='mobile_screen'>
	<img src="https://barcelonacodeschool.com/files/pics/cur_files/citizen_reports_9184.jpg" alt="weather app screenshot" class='mobile_screen'>
	<img src="https://barcelonacodeschool.com/files/pics/cur_files/citizen_reports_9183.jpg" alt="weather app screenshot" class='mobile_screen'>
</div> -->