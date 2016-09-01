## Unity-Samples

### How to build the Samples:

- Download the Pyze Unity SDK from http://github.com/pyze/Unity-Library
- Create a new Unity Project
- Import the downloaded sdk from http://github.com/pyze/Unity-Library into the empty Unity Project
- Download or clone any Sample app listed here
- Import the downloaded sample app package into project
- Open the sample app scene
- Get your Pyze App Key from http://growth.pyze.com  (see http://unity.pyze.com for instructions)
- Initialize Pyze SDK using the Pyze Menu in Unity IDE (see http://unity.pyze.com for instructions)
- Go to File > Build Setting > (Select Platfrom) Android or iOS > Switch Platform > Build and Run you Sample

About Samples

In Hat Trick and Flappy Bird samples you can search for regions defines as "#region Pyze", to find the code changes.

1. Pyze Events App
- This sample app lets you get understanding of how the Events, Custom Events and In App Messages work in Pyze.

2. Hat Trick Sample Game
- Hat Trick Sample Game is simple game, where you need to collect bowling balls in a hat and avoid bombs from blasting. 

- This game uses Pyze SDK's curated Events to send the following events,

a. Game start - By using curated event Pyze.PyzeEvents.Gaming.PostGameStarted method

b. Game end   - By using curated event Pyze.PyzeEvents.Gaming.PostGameEnd method

- This game also makes use of InAppMessages class provided by Pyze SDK to show In App Messages if present, whenever the game ends, using the following code snippet

//Check if there are any new messages to be read.
Pyze.PyzeEvents.InAppMessages.CountNewUnFetchedMessages((sender, e) => {
	//If there are new messages present then show them to user
	if(System.Int32.Parse (e.Value) > 0){
		Pyze.PyzeEvents.InAppMessages.ShowInAppMessagesWithDefaultUI ((sender1, e1) => {
			//Handle Button Click Here eg: Increase the Game time etc.
			Pyze.PyzeEvents.PostCustomEvent("CTA Button Clicked");
		});
	}
});

- Above snippet also shows the usage of Custom events. In the above example we are posting custom "CTA Button Clicked" event, whenever the Call To Action button in the in app message is clicked.

3. Flappy Bird Style Game
- This game makes use of Pyze sdk's Timed event api's to send game start and game end events.
- It creats a timer reference using the following snippet when the game starts.
gameTimerReference = Pyze.PyzeEvents.TimerReference;

- It sends the following event when the game ends, using the reference created at the start of the game.

Dictionary<string,object> customAttributes = new Dictionary<string, object>();
customAttributes.Add ("Score", score);
Pyze.PyzeEvents.PostTimedWithEventName("Game Over",gameTimerReference,customAttributes);
