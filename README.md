# SocialMediaAPI
## Description

Built to provide the agility, speed, and flexibility crucial to both startups and social media applications, this API uses a NoSQL approach to perform the Create, Read, Update, and Delete (CRUD) operations necessary for a social media startup. Startups tend to start with limited resources, grow rapidly, and pivot directions quickly. Startups also tend to deal with diverse data types and heterogeneous data, and they may need to modify schema as the project evolves. With the cost-effectiveness, scalability, and flexibility of NoSQL databases like MongoDB, NoSQL is an apt choice for a startup environment. Social media networks benefit from NoSQL approaches in similar ways. Social media applications require rapid read and write operations in order to provide the dynamic, real-time experiences that users expect. Given how widely users vary in behavior, social media applications often work with unstructured data. NoSQL is a great match to help social media applications provide smooth, rapid user experiences while accommodating unstructured data.

This API uses MongoDB and Mongoose to allow full CRUD operations for users and thoughts and Create and Delete operations for friends and reactions. It balances flexibility with structure, and it enforces validation rules to prevent erroneous data types, invalid emails, duplicate usernames. But, the API leans more towards the flexibility that is the main draw of MongoDB. When used with Insomnia or another API client, the application responds with the appropriate JSON data and gives informative messages and HTTP status codes as necessary. Overall, this project is a solid, yet adaptable, backend which facilitates rapid, accurate database operations.

### Built With

- [![Mongo][MongoDB]][Mongo-url]
- [![Mongoose][Mongoosejs]][Mongoose-url]
- [![Express][Express.js]][Express-url]
- [![Node][Node.js]][Node-url]
- [![Insomnia][Insomnia.rest]][Insomnia-url]
- [![Javascript][JavaScript]][Javascript-url]
- [![Nodemon][Nodemon.io]][Nodemon-url]
- [![VSCode][Visualstudio.com]][VSCode-url]


<!-- GETTING STARTED -->
## Getting Started

First, ensure that you have the programs listed in the [Prerequisites](#prerequisites) installed on your local machine. Continue through the [Installation](#installation) steps, which will create the database, establish the connection, and start the server. Follow along with the [Usage](#usage) section or [walkthrough video](https://drive.google.com/file/d/1mStBObpAbO7XbH4da44y7pcVhYDs0q9Q/view?usp=sharing) to start making HTTP requests and see the API in action!

### Prerequisites

To use this API, you'll need to have Node.js and MongoDB installed locally. Node.js can be installed [here](https://nodejs.org/en/download) and MongoDB can be installed [here](https://www.mongodb.com/try/download/community). If you don't have an API client already installed, you can download Insomnia [here](https://insomnia.rest/download) or Postman [here](https://www.postman.com/downloads/) (any API client will work). The rest of the dependencies will be installed when running npm install in step 3 of the installation instructions below.

### Installation

1. Clone the repo:
    ```sh
    git clone https://github.com/Rthornburg-Ardi/SocialMediaAPI
    ```
2. Navigate to the project directory:
    ```
    cd social-media-startup-api
    ```
3. Install NPM packages:
    ```sh
    npm install
    ```
4. Create the database, establish the connection to the database, and start the server:
    ```sh
    npm run start
    ```
5. When the server is running, you will see a message in your terminal with the number of the port the server is listening on. If the port is the default, 3001, the base URI for HTTP requests will be `localhost:3001`. Throughout the [Usage](#usage) section, example URIs will be given assuming a port number of 3001; make sure to use your port number if the app is listening on a different port. 

<!-- USAGE EXAMPLES -->
## Usage

### Database Operations for Users and Friends

#### Create (POST) a User

Open the API client of your choosing and create a user by sending a POST request to localhost:3001/api/users, including a username and email in the JSON body (the pane on the left). The response can be seen in the pane on the right. In this case, the response was a 200 OK status and the returned data of the successfully created user.

![create user screenshot](./assets/img/image.png)

For the purpose of this demonstration, 4 additional users were created by the same method, using the 4 following JSON request bodies:

```
{
    "username": "NatureLover88",
	"email": "loverofnature88@yahoo.com"
}

{
    "username": "TechEnthusiast23",
	"email": "tech23@outlook.com"
}

{
    "username": "AdventureSeeker123",
	"email": "seeker123@protonmail.com"
}

{
    "username": "MountainExplorer56",
	"email": "mountainexplorer56@protonmail.com"
}
```

#### Read (GET) All Users

Send a GET request to `localhost:3001/api/users` to view all users. As can be seen in the below 2 screenshots, all 5 of the users were retrieved. 

![get users screenshot 1](./assets/img/image-1.png)

![get users screenshot 2](./assets/img/image-2.png)

#### Read (GET) a Single User

Send a GET request to `localhost:3001/api/users/:userId` to view a single user. In the below screenshot, the _id of the user with username of SunnyTraveler was used as the userId parameter in the URI, and the user SunnyTraveler was successfully retrieved.

![get user screenshot](./assets/img/image-3.png)

#### Update (PUT) a User

Send a PUT request to `localhost:3001/api/users/:userId` to update a user. Make sure to provide the username and email for the update in the JSON request body. In the below 2 screenshots, SunnyTraveler has been updated to have a username of OutdoorAdventurer99 and an email of adventurer99@gmail.com. When a GET request for all users is sent, the updated user appears as the first object in the response.

![update user screenshot 1](./assets/img/image-4.png)
![update user screenshot 2](./assets/img/image-5.png)

#### Delete (DELETE) a User

Send a DELETE request to `localhost:3001/api/users/:userId` to delete a user. In the below screenshot, the user with username MountainExplorer56 (the 5th user created from the POST route) is deleted by providing the user's _id as the request parameter. When a GET request for all users is sent again, MountainExplorer56 no longer appears.

![delete user screenshot 1](./assets/img/image-6.png)
![delete user screenshot 2](./assets/img/image-7.png)

#### Add (POST) a Friend

Send a POST request to `/api/users/:userId/friends/:friendId` to add a friend to a user. The user _id of the user (userId) and the user _id of the friend to be added (friendId) are both provided as request parameters. In the below example, NatureLover88 is added as a friend to OutdoorAdventurer99 (as an ObjectId reference). Upon making a subsequent GET request to view OutdoorAdventurer99, NatureLover88 appears in OutdoorAdventurer99's friends array.

![post friend screenshot 1](./assets/img/image-8.png)
![post friend screenshot 2](./assets/img/image-9.png)

#### Remove (DELETE) a Friend

Send a DELETE request to `/api/users/:userId/friends/:friendId` to remove a friend from a user, where :userId is the _id of the user with the friend, and :friendId is the user _id of the friend to be removed. In the below screenshot, NatureLover88 is removed from OutdoorAdventurer99's friends, and OutdoorAdventurer99's friends array is now empty.

![delete friend screenshot](./assets/img/image-10.png)

### Database Operations for Thoughts and Reactions

#### Create (POST) a Thought

Create a thought by sending a POST request to `localhost:3001/api/thoughts`. In the request body, include the userId of the user creating the thought, as well as the user's username and the thoughtText (the content of the thought). Two examples of creating a thought are shown below. 

![post thought screenshot 1](./assets/img/image-11.png)
![post thought screenshot 2](./assets/img/image-12.png)

#### Read (GET) All Thoughts

To see all of the thoughts, send a GET request to `localhost:3001/api/thoughts`. The 2 thoughts created in the previous section are returned as results in the below screenshot.

![get thoughts screenshot](./assets/img/image-13.png)

#### Read (GET) a Single Thought

A single thought can be retrieved by its _id by sending a GET request to `localhost:3001/api/thoughts/:thoughtId`. The below screenshot shows the successful retrieval of the first posted thought.

![get thought screenshot](./assets/img/image-14.png)

#### Update (PUT) a Thought

To update a thought, send a PUT request to `localhost:3001/api/thoughts/:thoughtId`. The request body can contain the thoughtText only, the username only, or the thoughtText and username. In the below example, the thoughtText is updated so that OutdoorAdventurer99's musings on the Lost Creek Wilderness become a Rocky Mountain National Park hike report instead.

![update thought screenshot](./assets/img/image-18.png)

#### Delete (DELETE) a Thought

To delete a thought, send a DELETE request to `localhost:3001/api/thoughts/:thoughtId`. In the below screenshot, NatureLover88's thought on the Maroon Bells-Snowmass Wilderness is deleted. When making a subsequent GET request for all thoughts, NatureLover88's thought no longer appears.

![delete thought screenshot 1](./assets/img/image-19.png)
![delete thought screenshot 2](./assets/img/image-20.png)

#### Add (POST) a Reaction

To add a reaction to a thought, send a POST request to `localhost:3001/api/thoughts/:thoughtId/reactions`. Make sure to use the _id of the thought you'd like to make a reaction to as the thoughtId request parameter. In your JSON body, include a reactionBody for the reaction and the username of the user creating the reaction. 

In the below screenshot, TechEnthusiast23 reacts to OutdoorAdventurer99's thought about Rocky Mountain National Park, and the reaction is visible in the reactions array of the OutdoorAdventurer99's thought.

![add reaction screenshot](./assets/img/image-21.png)

#### Remove (DELETE) a Reaction

To remove a reaction from a thought, send a DELETE request to `localhost:3001/api/thoughts/:thoughtId/reactions`. For the :thoughtId parameter, use the _id of the thought which currently has the reaction. In the JSON body, provide the reactionId of the reaction to be removed. 

In the below screenshot, TechEnthusiast23's reaction to OutdoorAdventurer99's thought about Rocky Mountain National Park is removed from the thought, and the response shows that the thought's reactions array is now empty.

![delete reaction screenshot](./assets/img/image-22.png)


<!-- HIGHLIGHTED FEATURES -->
## Highlighted Features

### Update Thought on User Update

When a user is updated and their username is changed, if the user has created any thoughts, the username field of the user's thoughts is updated as well. 

The below 2 images show a successful update of our earlier example's OutdoorAdventurer99, now with the username ForestWanderer which shows under the Rocky Mountain National Park thought.

![feature 1 screenshot 1](./assets/img/image-30.png)
![feature 1 screenshot 2](./assets/img/image-23.png)

### Delete Thoughts on User Delete

When a user is deleted, any thoughts the user had created are deleted as well. 

To illustrate, a GET All Thoughts request returns 3 thoughts to start: ForestWanderer's thought about Rocky Mountain National Park, a thought made by CoastalExplorer about a Dipsea Trail hike, and a thought made by CoastalExplorer about the Big Sur Coastline. See the below screenshot for this GET request.

![feature 2 screenshot 1](./assets/img/image-24.png)

After deleting CoastalExplorer, we receive the following response message: 

![feature 2 screenshot 2](./assets/img/image-25.png)

When making another GET request for all thoughts, we can see that CoastalExplorer's thoughts no longer appear.

![feature 2 screenshot 3](./assets/img/image-26.png)

### Update User on Thought Delete

When a thought is deleted, the thought should no longer appear under the user who created it. So, when a thought is deleted, the user who created the thought is updated to reflect the change. 

To verify, ForestWanderer's thought about Rocky Mountain National Park is first deleted; ForestWanderer is then retrieved through a GET request, and the thought no longer appears in the thoughts array.

![feature 3 screenshot 1](./assets/img/image-28.png)

![feature 3 screenshot 2](./assets/img/image-29.png)

<!-- CONTRIBUTING -->
## Contributing

Contributions are what make the open source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

If you have a suggestion that would make this better, please fork the repo and create a pull request. You can also simply open an issue with the tag "enhancement".

Don't forget to give the project a star! Thanks again!

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

<!-- LICENSE -->
## License

This project is covered under the MIT License. You can learn more about this license and its coverage and permissions [here](https://opensource.org/licenses/MIT).

<!-- CONTACT -->
## Contact

If you have any questions/thoughts about this project or would like to connect, you can reach me at https://github.com/Rthornburg-Ardi/ or thornburg.rebeca1@gmail.com. I look forward to hearing from you!