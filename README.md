# TapVerse
1) Commit or download the zip onto your system
2) Run ***react-native run-android***

# INFO
1) After linking react-native firebase google sign in option viro media testbed does not work, alternative is to either generate bundle using the command below and run using android studio or ***react-native run-android --variant={debug variant}***
2) debug variant for this app is ***gvrDebug***
3) Run the metro bundler, using react-native start, before running "react-native run-android --variant=gvrDebug"

# Commands
To generate the index bundle file to run the app on android studio<br>
1) react-native bundle --platform android --dev false --entry-file index.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res 


# TODO: 
***[done]*** 1) Make a scorecard and set score as a state variable for scorecard <br><br>
***[done]*** 2) Replace the multiple viro sounds that you are adding with each object with just one speaker, to reduce the number of components being mounted<br><br>
***[noted]*** 3) Remove drawable and raw folder from android/app/src/main/res<br><br>
***[done]*** 4) Change App.js code for sign in page after checking the bookmark from your chrome <br><br>
***[done]*** 5) Add a exit button in the game screen<br><br>
***[done]*** 6) Add log out button in the main menu and also add a user name in top right corner or somewhere<br><br>
***[done]*** 7) Check if you change the VR part of the game and generate the bundle will the edit be shown in the app without using ./setup-ide.sh android command (cause this command will fuck up the entire android build at this point)<br><br>
***[done]*** 8) Clean the code (remove unnecessary styles that you declared etc.) and add leaderboard<br><br>
***[done]*** 9) take part in code gladiator and also don't forget about infytq<br><br>
10) Take part in code gladiator ML challenge and practice DBMS for infytq qualifiers<<br>br> 
***[done]*** 11) remove sound attached to each viroSound<br><br>
12) Implement pagination to load the data faster<br><br>
***[done]*** 13) Add the user data in the firestore from the login page if the user database does not exist in the firestore<br><br>
***[done]*** 14) Only update if the current high score of the user is more than the previous high score<br><br>
15) Use react-native-pages to implement pages in the leaderboard<br><br>
***[done]*** 16) Retrive data from firestore and display it on leaderboard<br><br>
***[done]*** 17) Check why the setFirestoreData is being called thrice when the app starts, which means the main menu is being rendered thrice (I am not sure why).<br><br>
***[done]** 18) Check when will a component unmount, because the last time I was trying to stop a song from playing when I am not playing the game anymore, it wasn't working.<br><br>
***[done]*** 19) Leaderboard is fetching data from the firestore several times when called once because of re-rendering, try to fix that. (Because of firestore sending documents indefinetely while onSnapshot is used, we can try react.memo to stop re-rendering of leaderboard several times) <br><br>
***[done]*** 20) Create a single js file for LoadScreen component and reuse it in game container and main app.<br><br>
***[done]*** 21) Try to create a function to get the userrank from the cloud instead of sorting the data on the client end and finding the rank.<br><br>
***[done]*** 22) Decrement the previous high score by 1 and increment the new high score by 1 in scores collection array

# Future TODO
1) Don't load the sound files on every re-render (prolly make them global, 'cause they are not going to be changed at any point)<br><br>

# Solutions to TODO queries
17) I was setting the state variables loggedIn and User seperately due to which there were two extra renderings, I fixed that by having one state variable. This bought down the number of re-renderings to 2, once in the initial load before the user data has been set and once after setting the user data (because fetching user data is a asynchronous task which will not interfere with the rendering).<br><br>
18) A component will unmount if it is no longer visible on the screen and all the subscriptions registered in the component have to be unregistered or not executed when the component is unmounted because otherwise it will throw an error.<br><br>
19) Got a temporary fix to the problem by retreiving the data every 1 second and only updating if there is a change in the data, this can be problamatic if the data grows and hence pagination is required so that you only have to keep checking for updates in the current page and not in the whole data.<br><br>
20) The score on the leaderboard does not match what is displayed when the game is over, prolly submitscore() function is being called before the game is over. <br><br>

# Sidenotes for TODO
21) Instead of creating cloud function, I created a collection in firestore that will store the reverseIndexed array to determine the userrank in real-time.

# Cool Features
1) Implemented almost constant time userrank retrival algorithm so that I don't have to go through every user's score to find out the current user's rank, will be very helpful when number of players are more.
