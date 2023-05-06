# Distributed-Application-and-Dashboard
This project contains the following parts:
1. A Web application deployed to the cloud through codespace. 
2. The information from a third-party API will be fetched to support user interactions at Android App.
3. Logging data from the Android App will be stored in the MongoDB and displayed in a dashboard.

## Description:
My application offers the user three different approaches to fetch an Emoji:
- Approach 1: prompt user to choose the category related to the Emoji. Eg: activities.
- Approach 2: prompt user to type a search word related to the Emoji. Eg: flags
- Approach 3: randomly generate an Emoji for the user. This approach does not take any user Input.
When the application launches, the user will be prompted with a main menu where they can choose one of approaches as described above. 
Based on the user choices (will be passed to the web service as an Http request), eventually the output (an Emoji Hash code) is fetched and displayed from a 
third Party API called EmojiHub.

## Application Design:
#### 1. Implement a native Android application
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; My application uses TextView, EditText, Button, RadioButton, RadioGroup, and ProgressBar. Please refer to the following for details of how they are incorporated into the RelativeLayout.
- activity_emoji_main.xml
- activity_emoji_one.xml
- activity_emoji_two.xml
- activity_emoji_three.xml

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Here a screenshot of the layout for main menu (activity_emoji_main.xml)

