---
tags: [React & NodeJS]
title: How to made an application with ReactNative with expo
created: '2024-11-01T08:53:43.492Z'
modified: '2024-11-08T17:29:33.211Z'
---

# How to made an application with ReactNative with expo

### Create a react application
- Create the directory application
    + ` mkdir my-first-app`
- Create the react app
    + ` npx create-expo-app my-first-app`
    + ` npx create-expo-app --template blank test_blank`
    + ` npx create-expo-app --template tabs test_tabs`
    + ` npx create-expo-app --template bare-minimum test_bare`
- Enter in the react directory
    + ` cd my-first-app`
- Install and Configure *EAS CLI*
    + `npm install --global eas-cli`
    + `eas login` Enter the Expo username and password 
    + `eas whoami` To check if you are logged
    + `eas build:configure` To create eas.json configuration file and Eas build
    + `eas build -p android --profile preview` build application on Expo
    + `eas expo install expo-dev-client`
    + `eas build --profile development --platform android`
- Start project
    + ` npm run start` or `npx expo start` or `npx expo start --tunnel`

- Publish project
    + `eas build -p android --profile preview`

#### NOTES
- If the application does not start on the android device:
    + Are you logged on Expo Go?
