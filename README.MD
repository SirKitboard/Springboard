
# Roll A Ball, Unity Tutorial

_Setting Up Your Environment_

What you need: 
* Download the version of unity compatiable with your device [here](https://unity3d.com/get-unity/download)

While your download is taking place, let me speak to you briefly about Unity 

##That's it! Now Lets Get started

**Set Up**
_This part is going to be very particular to make sure we all stay on the same page_

1. Create new Project. Name it *Roll A Ball*
2. Save scenes in a folder called _Scenes. Name it MiniGame.
3. Change Layout to 2 by 3 (_Easier to work with, not mandatory_)
4. Create  a Plane and name it ground. Scale it (2, 1, 2)
5. Add a Ball Called Player and reset it
6. Move the ball up on the Y to 0.5.
7. Create a materials folder
8. Create a material here and name it background
9. On the Albedo variable in the inspector, change color to RGB: 0, 32, 64
10. Drag this material onto the floor
11. Change angle on the Y to 60

*Great*! Now that the ball is set up, we can move on to the fun stuff

**Moving The Player**

1. Select the Player object. And Add RigidBody
2. Create a Scripts folder
3. Create a script component onto the Player object named PlayerController.cs
4. Remove sample code and write void FixedUpdate

_Now for some code..._

float moveHorizontal = Input.GetAxis("Horizontal");
        float moveVertical = Input.GetAxis("Vertical");

The Rigidbody component is accessed via scripting. We need to create a private variable to hold our rigidbody. 

private Rigidbody rb;
void Start() {
        rb = GetComponent<Rigidbody>();
    }
Vector3 movement = new Vector3(moveHorizontal, 0f, moveVertical);

        rb.AddForce(movement);

*Leave the new Vector blank first*.

Create public float speed and multiply to movement. Test different values, I would suggest just sticking to 10.

**Camera**

*Move the Camera to y = 9.5
*Rotate 45 on the X

Now let's create a script to better control our camera angles

Create a Script called CameraController and attach it to Camera
    public GameObject player;

    private Vector3 offset;

    // Use this for initialization
    void Start () {
        offset = transform.position - player.transform.position;
    }
    
    // Update is called once per frame
    void LateUpdate () {
        transform.position = player.transform.position + offset;
    }


**Setting Walls**

1. Create empty walls. Reset it to origin
2. Create cube west wall and reset. Parent Walls
3. Scale west walls by (0.5, 2, 20.5). Use translate tool to place. It should be -10
4. Dupllicate for east wall
5. Duplicate for north and south wall, rotate these walls.

_Test!_  At this point if you have any questions at all, you should be shooting them my way.

Now that as have our "game board" and barriers so we dont fall of our screen, let's set up some targets for our player.

**Collectibles**

Go to on trigger enter. Take the sample code to PlayerController
We don’t want to destroy, just deactivate. 
Remove destroy and replace with a compareTag on other.gameObject 
compareTag(“PickUp”). Create a PickUp tag.
Other game Object setActive (false);
It hides the other game object  
Now find the audio source download and put it in an Audio folder in theAssets folder. Drag that onto the player component. Add GetComponent<AudioSource>().Play()

**Displaying Text**

Private count var in C#
In trigger enter do count = count + 1;
Create UI Text. Rename to Count Text. Reset the transform and change color to white.
Select the Anchors icon. Hold shift and alt keys and select top left
Change the rect transform to x 10 and y -10
In PlayerController, using Unity UI
Public Text countText

**Write**

include the following piece of code:

countText.text = "Count: " + count.ToString();

in *both* start and on trigger.

Make reference to text

Make new UI Text named WinText. Reset transform

Change font size to 24 and color to white(_Or whatever you prefer_)
Change text to Win Text. And Pos Y to 75

Make another public text winText.

In onTrigger after countText write
if (count > [num of objects]) {
                winText.text = "You Win!";
            }
And in Start winText.text = “”

Make reference to winText

**Quit**
In Player Controller create an update that waits for the escape key and quits the game.




























