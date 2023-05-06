# Distributed-Application-and-Dashboard
This project contains the following parts:
1. A Web application deployed to the cloud through codespace. 
2. The information from a third-party API will be fetched to support user interactions at Android App.
3. Logging data from the Android App will be stored in the MongoDB and displayed in a dashboard.
<img src="/application_summary.png" alt="Diagramt" width="500"/>

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

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Here are screenshots of main menu and subviews   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="https://user-images.githubusercontent.com/124459825/236644202-739072d7-ff14-4361-acfa-6d5882369d02.png" alt="Diagramt" width="700"/>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Here are screenshots of an example for user interaction   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="https://user-images.githubusercontent.com/124459825/236644282-3306e97a-a913-4d90-8773-68eaa2ba9c0e.png" alt="Diagramt" width="530"/>

#### 2. make an HTTP request to the web service
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; My application does an HTTP GET request in EmojiModel.Java. The HTTP request is: "github-codeSpace-URL/getEmoji/" + searchTag   
Where searchTag is the user’s input:
- approach 1: choice of the four categories
- approach 2: typed search term
- approach 3: searchTag is set to “random”.   

The search method makes this request of my web application, parses the returned Json message to get the hashcode of Emoji and return, display 
the Emoji in HTML format. Here is a simple workflow to aid understanding:   

<img src="https://user-images.githubusercontent.com/124459825/236644466-5c53a742-f845-48ba-986b-e2823a843801.png" alt="Diagramt" width="600"/>

An example of the Json reply is:   
![image](https://user-images.githubusercontent.com/124459825/236644692-419dba57-5c33-4925-b6e8-31110d596b75.png)

#### 3. Connect to MongoDB Atlas
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The main MongoDB web site is https://www.mongodb.com. The site provides documentation, a downloadable version of the database manager application (mongod) that you can run on your laptop, and MongoDB drivers for many languages, including Java.  
Mongod is the MongoDB database server. It listens by default on port 27017. Requests and responses with the database are made via a MongoDB protocol.  
Mongo (without the DB) is a command line shell application for interacting with a MongoDB database. It is useful for doing simple operations on the database such as finding all the current contents or deleting them.   
This is where the logging information will be stored.

##### Setting up MongoDB Atlas
1. Create your account. Go to https://www.mongodb.com/atlas/database and create your own free account.
2. Answer the "Tell us a few things..." questions however you like, but include Java as the preferred language.
3. Choose to create a FREE shared cluster.
4. Accept the default settings and Create Cluster.
5. In the Security Quickstart:
 - *How would you like to authenticate your connection?*  
 Authenticate using Username and Password.  Create a MongoDB user name and password 
 - *Where would you like to connect from?*  
 Choose My Local Environment, add the IP address `0.0.0.0/0`, and Add Entry.
 - Then Finish and Close.
 
#### 4. Display Web-based Dashboard
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The dashboard contains analytical statistics regarding user activities:
- User IP address: to avoid potential security threats; to better identify potential target group of users.
- Search Date and Time: to track when the searches are made most frequently.
- User Input: to track what category the user is most interested in and searched a lot of times.
- Response, including name, category, and group: to assess if the users will be satisfied with such response or not.
- Latency: how long it took for a user to get the output, which is an emoji. We should optimize the mobile application if there is high latency.
- Device: track the devices the user used for the mobile application.
- Index: a series of constructive integers starting from 1. 1 indicate the first search made by the user. This helps to track the details of the latest 
search made.   

![image](https://user-images.githubusercontent.com/124459825/236645149-4e70f7f1-6a76-4702-93c9-eeb666c915bf.png)

## Emoji API:
- Name: EmojiHub
- URL: https://emojihub.yurace.pro/api/random  
 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;EmojiHub provides an opportunity to get random emojis from already sorted categories and groups.
My mobile app will prompt the user to select a category (e.g: people, sports, animals, and travel) that the user is 
interested in and then search EmojiHub using their API to display a random Emoji image related to that category.
