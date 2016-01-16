<a id="top"></a>
# DevFest Mobile Development Track

*A short description of your document*

Written and developed by [Matt](http://mattpic.com) and [ADI](adi).

<a href="#top" class="top" id="getting-started">Top</a>
## About This Document

### Methodology
This guide will teach you the basics of mobile programming, in particular iOS programming, by helping you to create your first mobile application. We will start with a basic app, incrementally adding features at each level until we have a fully-featured app. You can start at any of the levels if you have prior experience with iOS programming, but we recommend beginners start at the beginning to make sure they see the entire picture.

### Prerequisites
You should have a beginner's knowledge of [Swift](swift-tour), Apple's new programming language that will be used for future generations of iPhone applications. It's a great language that is somewhere between Objective-C, Python, and Javascript. Also, you should have programmed before; we'll skip over concepts like variables and functions, assuming you know what they are.

## What We're Building
Throughout this tutorial, we're going to be creating a Pokedex application. For those of you who don't know, a [Pokedex](pokedex) is a digital encyclopedia from the show "Pokemon" that holds information about all the world's pokemon. Who needs to carry around a Pokedex when we can build one for our iPhone?

We'll first start by creating a basic landing page. Then, we'll show you how to create a list to show all the different Pokemon. Next, we'll use the PokeAPI to populate our list with information about real Pokemon. After that, we'll create a detail page that will provide more information about a Pokemon that you would select. Finally, we'll make it so that each user can mark their favorite Pokemon to store for easier access.

<a href="#top" class="top" id="table-of-contents">Top</a>
## Table of Contents
-   [Level 0: Environment Setup](#level0)
-   [Level 1: Basic Landing Screen](#level1)
    -   [1.1 Sample](#sample)
        -   [1.1.1 Sample](#sample)
-   [Level 2: Simple List View](#level2)
-   [Level 3: Loading Web Data](#level3)
-   [Level 4: Adding a Detail View](#level4)
-   [Level 5: Adding Favorites with Core Data](#level5)
-   [Additional Resources](#additionalresources)


------------------------------
<a href="#top" class="top" id="level0">Top</a>
## Level 0: Environment Setup
- General DevFest environment setup (likely Git)
- Have a Mac
- Install XCode
- Install Cocoapods

<a href="#top" class="top" id="level1">Top</a>
## Level 1: Your First iPhone Application
In this section, we're going to be starting our first iOS project. We'll explore the fundamentals of how to use XCode, what a Storyboard is, and how to layout your user interface using constraints.

### 1.1 Creating your First Project
To create your first project, open XCode. Next, from the top menu bar, select `File -> New -> Project`. For your project, on the left side, select 'Application' under 'iOS', and make sure it's a 'Single View Application', as seen below. Then press next.

![Create Project](https://dl.dropboxusercontent.com/s/2648wkh80gt8zxl/create-proj.png)

Next, give a name for your project; I'm calling mine Pokedex. Also, if it doesn't come pre-filled, enter an organization name and identifier; this will be used later by the App Store, but it doesn't affect us much. Make sure your language is set to 'Swift' and your devices to 'iPhone', then press next.

![Name Project](https://dl.dropboxusercontent.com/s/lw68oyppocjeal5/nameproject.png)

Now you've created your first project!

### 1.2 Exploring XCode
XCode is the application that you develop iOS applications in. Because it's such a large piece of software with a lot of functionality, it can be confusing to understand at times. Generally though, the application is broken up into four parts: the editor, the project navigator, the utilities, and the project toolbar.

#### 1.2.1 The Editor
The editor is the large part in the center. This is where you'll write code, build your user interfaces, and essentially do most of the work. It's essentially a text editor built into the application as you might see in Sublime or some other IDE.

### 1.2.2 The Project Navigator
The project navigator is the column all the way to the left in the project. It shows all of the files that are in your project. Clicking on one opens the file in our editor. For our project, this is what it should look like:

![Navigator](https://dl.dropboxusercontent.com/s/g4rv9k3rdp7kd8q/navigator.png)

### 1.2.3 The Utilities
A lot of different things are crammed into the utilities sidebar, which appears on the right side. We'll see most of them as we continue, but it features attribute inspectors, which allow us to attributes, like fonts and colors, to UI elements, size inspectors, which allow us to configure their positions, and identity inspectors which allow us to assign specific classes to views. Also, it features our object library, which has all of the built-in views we'll use in our app, including buttons, labels, and other things.

### 1.2.4 The Project Toolbar
The project toolbar is all the way at the top, above the editor, project navigator, and utilities. On the left side, we'll see a play button and a stop button. As you may expect, these are used to run your project and to stop your project. You just pick which device you want to run your project on and press the play button.

![Play Button](https://dl.dropboxusercontent.com/s/ss71tvkwylozff0/playbutton.png)

On the right side are some buttons that change the way our views are presented Play around with them to see what they do.

## 1.3 Project File Structure
In the Project Navigator we saw above, you'll notice that there are several files that we have: `Main.storyboard`, `ViewController.swift`, and `AppDelegate.swift` are the most important. Let's discuss each one of them in detail.

### 1.3.1 Storyboards
`Main.storyboard` will be where we create our user interface. As the name suggests, the storyboard allows us to build different screens and then configure how we get from one screen to another. For example, in this level, we'll create our home screen in our `Main.storyboard` file. In the next level, we'll configure the 'Enter' button on our homescreen to bring us to the Pokedex list screen. Thus, by looking at our storyboard file, we'll be able to understand the entire flow of our application, from start to finish.

By default, we are given `Main.storyboard`, which is configured to by the entry point to our application. When our application runs, the first thing that will be presented will be the entry point of our storyboard.

You can read more about storyboards [here](storyboard).

### 1.3.2 View Controller
`ViewController.swift` represents our home screen. As the name suggests, a view controller controls the view. This means that we do things like set the text for labels, set the images for image views, load data from an API to present, and many other things. Roughly, each view controller corresponds to a different screen in our application; thus, if we want a new screen in our application, we'll create a new view controller file in our project.

Each ViewController extends the base class `UIViewController`; thus, our default `ViewController` inherits many methods from this base class, which we'll see later. To use new custom classes, we simply set the custom class inside of our `Main.storyboard` file, in the utilities sidebar. We'll see much more of this later.

You can read more about view controllers [here](view-controller).

### 1.3.3 App Delegate
`AppDelegate.swift` contains many of the global configurations for our application. We won't touch this file often, but it is the first code that is run when our application is launched. The top function in this file, `applicationDidFinishLaunchingWithOptions`, runs immediately after the application has launched, and allows us to decide which storyboard should be used, whether we have a logged-in user or not, and many other kinds of things. Global variables are also often stored in this file.

As we'll see later, a delegate is essentially an object that gets notified when certain events occur or when certain states are reached. If you click on `AppDelegate.swift`, you'll see `applicationDidEnterBackground` and `applicationWillTerminate`; without knowing how these things are detected, we can simply write code that will run whenever our application performs these things. Delegates are really helpful, and we'll explore them more later.

I found this [StackOverflow question](delegates) to be quite helpful.

### 1.3.4 Other Files
While the above three are our main files, there are some other files in our project that are less important, but still worth discussing.

`Info.plist` contains information about our application, such as our application name, what version of our application we're on, and other things like this. Some things may require configurations to be made in this file.

`LaunchScreen.storyboard`, as you may expect, is a storyboard that represents our launch screen. Here, you can configure the screen that appears just before our application launches. It defaults to just being a blank screen.

`Assets.xcassets` is a file that contains the assets for our project. If you click it, you'll see just one asset, 'AppIcon', on the left side. If you click it, you'll see the asset configuration screen open. This screen allows you to drag and drop the different sizes of the image you'll need for different screen sizes; it's fairly self-explanatory.

![Assets](https://dl.dropboxusercontent.com/s/flwod4zizqvsz2j/assets.png)

## 1.4 Creating our Home Screen
Now that we have a pretty good idea of how to use XCode and what all our different files mean, let's start making our app! To start, in our project toolbar up at the top, select 'iPhone 6s' from the dropdown and press the 'Play' button. 

After a moment, you should see the iPhone simulator appear. The simulator is essentially a simulated iPhone running inside of our computer; it allows us to test iPhone applications easily without needing a physical device. Play around in the toolbar for Simulator and you'll find that you can reach the home screen, open the 'Settings' page for the device, and do all sorts of our other things.

Initially, your application should just be a blank screen, as below. From here, let's start adding some stuff to it.

![Blank Screen](https://dl.dropboxusercontent.com/s/pxzgu8mq4s94we0/blankscreen.png)

### 1.4.1 Setting our First Property
Everyone knows that the Pokedex is red, so our plain white background definitely won't do. Let's set the background of our home screen to be red!

On the left side, click `Main.storyboard` to open our storyboard in our center editor. You should see something like this:

![Storyboard Editor](https://dl.dropboxusercontent.com/s/4lpp3vqarp9dlf1/storyboardeditor.png)

On the left side, you'll see the hierarchy of the view controllers. Right now, we have a 'View Controller Scene', which represents some action in our application. Inside of that, we have a single view controller, which corresponds to our home screen. If you click on 'View Controller' on the left side, then look over at our Utilies sidebar on the right and select the third icon from the left; in this screen, under 'Custom Class', you'll see 'ViewController' is filled in. 

![Custom Class](https://dl.dropboxusercontent.com/s/2fbimp9ge2a0tsr/configuration.png)

Thus, in order to change what type of view controller we're using, we simply need to change this class. For example, if we wanted our first view controller to be a login screen, we might create a new file, `LoginViewController`, and set the Custom Class on this view controller to be 'LoginViewController'.

Now, inside this ViewController hierarchy, we should see 'View'. For each ViewController, we have a View object, which corresponds to what we see visually. Click on 'View' on the left side. On the utilities sidebar on the right, click the attributes inspector; it's the third icon from the right. Click the 'Background' dropdown, click 'Other', and then select 'Red'; you can do this by entering 255,0,0 in the RGB selectors.

![Attribute Selector](https://dl.dropboxusercontent.com/s/sg19rtqx475s2i0/attributeselector.png)

Once you do this, the background color of the view should change to red. Press the play button to run the app, and you'll see the changed background color.

### 1.4.2 Adding our First View
You can't make an app just by changing the background color; we need things like buttons, text labels, and text fields. Let's start by adding some.

Views in iOS are recursive by definition; views are composed of a collection of views, which we call subviews, and they all descend from the class `UIView`. Some examples of subclasses of `UIView` include `UILabel`, `UIButton`, and `UITextField`. In our `Main.storyboard` file, we can add these things to our view controller's view.

To start making our app, let's add the Pokemon logo; it's a good way for people to know what exactly our app does.

Make sure our red view is up. Next, you should see a section in the bottom right with things like "View Controller" and "Storyboard Reference" in there. This is where all of the UI widgets for iOS apps, like buttons, tab bars, and text fields, reside; to add one, you just drag and drop onto your storyboard file. In the text box, type "image"; you should see one result, "Image View": Drag and drop from the Image View into the center of the red canvas. We now have an image in our app!

![Image View](https://dl.dropboxusercontent.com/s/ef0ql52ku5wiunk/image.png)

Something you may be wondering: our storyboard view is a square, not the dimensions of an iPhone. This is because the view isn't for any particular iPhone, but is meant to represent all the different iPhones, from the iPhone 4 to the iPhone 6s. We do this with a system called [Auto Layout](autolayout).

**Auto Layout** is essentially a generic way of laying out your views so that iOS can handle the views given a set of **constraints**. Constraints are a set of rules that the view must fulfill; it's the job of iOS to layout each of the views given a screen size, which we know once the app runs on the device. An example of a constraint would be to make sure that the left side of the view is 20px from the left edge, or to make sure that the top of one view is 10px from the bottom of another view, or to make sure that the view is 40px high.

If we don't use constraints, our app has no idea how to layout our views. It doesn't know how big it should be or in what position it should be. So, to make sure our image looks like we want it to, we need to add constraints.

First, let's make sure our logo is centered vertically; we want it to appear in the middle of the screen. To do this, we can add a constraint. Control-drag from our ImageView in our left bar to its parent View; we drag in this direction because we want the subview to be centered within the parent view. Once you do this, you'll see several options for different constraints, most of which do what you'd think they'd do. 

![Constraints](https://dl.dropboxusercontent.com/s/hea7osfnenno6g7/constraints.png)

To center it vertically, please select "Center Vertically in Container". Since we know that it should be centered vertically, now we should define how it will look horizontally. Control-drag the same way you did above, and first select 'Leading Space to Container Margin'. Then, select 'Trailing Space to Container Margin'. These essentially say 'How much space comes before it to the left?' and 'How much space comes before it to the right?'.

To set the actual values, select the Size inspector icon on the right side; it's the second from the right. Down toward the bottom, you'll see all the constraints that you've added. To change a value of something, just click 'Edit'. For each the trailing space and leading space, change the value to 20; this way we'll add 20px on each side within our view. Once you're done, it should look as follows:

![Constraints View](https://dl.dropboxusercontent.com/s/6ubzlgsg8r0j74e/Constraints%20View.png)

Once we've done this, on the left side you should see a red dot appear to indicate an error. Double click it, and you'll see this screen:

![Constraint Error](https://dl.dropboxusercontent.com/s/nu276g9cd7nla2m/constrainterror.png)

Our error is telling us that we don't have constraints for Y position or height. What exactly does this mean?

When we set constraints, we need to add constraints to fulfill four different things:

1. X-position
2. Y-position
3. Width
4. Height

If we don't fulfill each of these, we'll get an error, and rightfully so! If we don't give each one of these four things, iOS won't have enough information to layout our views!

Let's think about what our first three constraints did for us. Centering the image vertically means we've provided Y-position; if the view is 200px tall, iOS knows that the center of our view should be at 100px. We've also set our width; if our view is 200px wide, our view will be (200 - (2*20))px wide because of the padding we've added on each side. We've also set X-position, though this one may be less obvious. Since we've put 20px of padding on each side, we know that our view's center will be centered horizontally; we could have just as easily added another constraint, "Center Horizontally in Container."

So, as our error tells us, we're missing height. How do we decide how tall our image should be? To do this, let's think back to why we're adding this image in the first place; we want to display the Pokemon logo. To do this, we need the Pokemon logo. So, download the image [here](pokemon-logo). Since we already know the width, and we know the aspect ratio of our image, it would probably be a good idea to set the aspect ratio for our image; that way, the height can be determined from our width.

To do this, Control-drag and drop from "Image View" to itself; you'll see a new menu for constraints appear. These constraints are a little bit different, in that they aren't in terms of the views container, but in terms of attributes of the view itself. Thus, if we wanted to set the width to 200px, we wouldn't need to know anything about the containing view. 

![Self Constraints](https://dl.dropboxusercontent.com/s/sbmk0fkwxz4aple/selfconstraints.png)

Once we've added this, in the "Constraint" menu on the right side, edit the "Aspect Ratio" constraint to be equal to 125:46, the aspect ratio of our attached image.

Now that we've done this, we're almost done. However, you may notice there is a yellow warning to the right of the view hierarchy. Click it, and you should see this:

![Constraints](https://dl.dropboxusercontent.com/s/vnhzidkibiw8vfq/constraintissues.png)

What the errors (and the yellow lines we see on the views) tell us is that our views the actual dimensions don't match our expected errors. This is because iOS is trying to layout our views based on our default view size (it's 600 x 600 by default). To fix this, press the triangle in the bottom right corner and press "Update Frames". After this, you'll see the frames of our views update.

![Update Frames](https://dl.dropboxusercontent.com/s/jd8e1jguueu44nf/updateframes.png) 

Once you've done that, let's actually add our Pokemon logo. In XCode, click `File -> Add Files to "Pokedex"`, locate the Pokemon icon, and press "Add". At this point, you should see the file in the project navigator on the left, entitled "English_Pokemon_logo.svg.png". To set the image of our Image View, open `Main.storyboard`, and click the Image View in the view hierarchy on the left. Then, in your attribute selector, start typing the name of your image in the Image box, at which point it should autocomplete. Once you press enter, you'll see the Pokemon logo appear, and with that, we're done adding our first view!

![Image Name](https://dl.dropboxusercontent.com/s/18l1wak4hhqzu3o/imageselect.png)

Note: Auto Layout can be quite difficult to understand at first. Deciding what constraints will lead to the layout you want can feel like a logic puzzle at times. However, it's MUCH better than the alternative, which would be designing an interface for each of the six different iPhones. It's worth putting in the time to learn, perhaps by re-reading this section a couple times.

### 1.4.2 Adding our Second View
We're going to need a way to enter our Pokedex; let's add a button to do that. Make sure your `Main.storyboard` file is open. Just like we did last time, search "button" in the bottom-right widget section. Then, drag and drop a button onto the view just below our logo. First, let's add a constraint to center it horizontally; do this by Control-dragging from Button to View in the view hierarchy on the left and selecting "Center Horizontally in Container". 

Next, let's set the y-position relative to the Pokemon logo. Control-drag from Button to our Image View in the view hierarchy on the left (not everything has to be relative to our parent view, we can set constraints relative to two subviews). Once you've done this, select "Vertical Spacing". Once you've done this, edit the value in the right sidebar to be equal to 20; we'll want 20px between the bottom of our logo and the top of our button. Once you've done this, the constraints should look as follows:

![Button Constraints](https://dl.dropboxusercontent.com/s/ot08708z63m1exa/buttonconstraints.png)

To finish up, double click the button and change the text to "Enter Pokedex". (Note: At this time, you may have to press "Update Frames", depending on where you dragged the button.)

Now that you're done, your storyboard should look as follows:

![Finished Storyboard](https://dl.dropboxusercontent.com/s/hx66dk5diemg4sz/finstoryboard.png)

Run your app, and you'll see your first completed application!

![First App](https://dl.dropboxusercontent.com/s/mvkh63kmdyqtyvg/level1shot.png)

<a href="#top" class="top" id="level2">Top</a>
# Level 2: Creating a List of Data
Now that we have a landing page, let's start fleshing out the bulk of the app. As you may imagine, if we're going to have a Pokedex, we'll probably need to create a list of Pokemon. Let's start that in this level.

## 2.1 Adding Navigation
In the last section, we added a button to "Enter Pokedex". Thus, we'll need a new screen to appear when we press this button, which will show the information about our pokemon. Also, ideally, we'll make it so we can press a "Back" button to get back to our landing page at any point. Let's do that here.

### 2.1.1 UINavigationController
`UINavigationController` is a built-in view controller in iOS that essentially handles navigation. You've probably seen apps where you can press a button and enter a new screen, and then there's a "Back" button in the upper left corner that brings you back to your previous page. The iOS Settings page is a good example of this.

![Settings](https://dl.dropboxusercontent.com/s/8vw7gpnh2a1q3wf/SettingsPage.png)

A `UINavigationController` handles all of this navigation by essentially embedding a stack of view controllers within it and showing a navigation bar at the top to allow the user to take further actions, like going back. We can hook up actions to add view controllers to the stack, pushing the navigation one layer deeper. We can always push the back button to back out of the navigation; that is, until we reach what is called the 'root view controller', the first view controller we want to appear.

As you may guess, we want to add a UINavigationController to our project. Also, we'll want our landing page to be our root view controller. To do this is quite easy. Open your `Main.storyboard` file and click on our view controller. Then, in the menu bar, selector `Editor -> Embed In -> Navigation Controller`. Once you do this, you should see the following (you may need to zoom out a bit):

![Nav Controller](https://dl.dropboxusercontent.com/s/esidomv8oiaqhgd/navcontroller.png)

This gives us a better idea of what a full storyboard will look like. As we add screens, we'll be adding more and more view controllers onto our storyboard, just like we added a navigation controller here. Also, we'll see an arrow that connects our `UINavigationController` to our `ViewController`; if we click the arrow, we'll see it highlights a message on the left that says "Relationship 'root view controller' to 'View Controller". This is telling us that the arrow represents the fact that our `ViewController` is the root view controller, meaning it will be the first screen to appear.

If you run the app at this point, it should look exactly the same as before, yet you'll see a navigation bar at the top. We'll handle this later.

### 2.1.2 Adding a New Screen
Now that we have our navigation controller, it's easy to show our next page when we press the button. First, let's begin by dragging a new view controller from our widgets section in the bottom right. Drag it anywhere onto the storyboard. It should look as follows when you're done:

![Second View](https://dl.dropboxusercontent.com/s/mckhbiiaa76dy9d/secondviewcontroller.png)

Now, we're going to need to write some code to make our list, so let's create a new custom view controller. To do this, click on "Pokedex" in the project navigator and click "New File". 

![New File](https://dl.dropboxusercontent.com/s/ccb890frngfnnh4/newfile.png)


Select "Cocoa Touch Class" from the iOS section, and name your file `PokedexViewController`. **IMPORTANT**: Make sure the "Subclass of" box is `UIViewController`; we're making a custom subclass for our new view controller.

![Pokedex View](https://dl.dropboxusercontent.com/s/vipoay7td1pma18/pokedexview.png)

You should see a new file, `PokedexViewController.swift`, in the project navigator. Feel free to look inside the file, but we'll be getting to it in just a moment.

As we saw before, we want to set the custom class of the view controller we dragged onto the storyboard. To do this, click on the view controller in our storyboard, and set the custom class to 'PokedexViewController'; it can be found in the right sidebar when you click the icon third from the left. Note: the class name should autocomplete. If it doesn't, you may have added the file incorrectly.

![Pokedex Custom](https://dl.dropboxusercontent.com/s/d4galttyp4e8cz9/pokedexcustom.png)

### 2.1.3 Adding a Segue
Now that we have a new screen, we need a way to present it. In particular, we need it to show when we press our 'Enter Pokedex' button. To do this, we can add a segue.

A [seque](segue) is a transition between scenes. It allows us to move from one screen to the next when certain actions take place, such as pressing a button. To add a segue, simply Control-drag from our button to our new view controller. From the menu that pops up, select "Push"; you'll see a new arrow appear between the two view controllers.

![Push Segue](https://dl.dropboxusercontent.com/s/l6nuc0jtvmn8ed9/pushsegue.png)

Now, try running our app. If you click the "Enter Pokedex" button, you should see our new (albeit blank) screen appear! We have navigation! Try pressing the back button, and you'll see we end up back at our home screen.

![Second Screen](https://dl.dropboxusercontent.com/s/25fn5to7xp1lrer/SecondScreen.png)







<a href="#top" class="top" id="level3">Top</a>
## Level 3: Loading Web Data

<a href="#top" class="top" id="level4">Top</a>
## Level 4: Adding a Detail View

<a href="#top" class="top" id="level5">Top</a>
## Level 5: Adding Favorites with Core Data


___________
<a href="#top" class="top" id="additionalresources">Top</a>
## Additional Resources

Along with this tutorial, there is a wealth of information available on iOS development all across the web. Below are some good places to start:

- [ADI Resources][learn]



[github]: https://github.com/mjp2220/devfest-mobile-track
[learn]: http://adicu.com/learn
[codecademy]: http://www.codecademy.com
[adi]: http://adicu.com
[pokedex]: http://bulbapedia.bulbagarden.net/wiki/Pok%C3%A9dex
[swift-tour]: https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/GuidedTour.html
[storyboard]: https://developer.apple.com/library/ios/recipes/xcode_help-IB_storyboard/Chapters/AboutStoryboards.html
[view-controller]: https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/
[delegates]: http://stackoverflow.com/questions/652460/what-is-the-appdelegate-for-and-how-do-i-know-when-to-use-it
[autolayout]: https://developer.apple.com/library/ios/documentation/UserExperience/Conceptual/AutolayoutPG/index.html
[pokemon-logo]: https://upload.wikimedia.org/wikipedia/commons/thumb/f/f7/English_Pok%C3%A9mon_logo.svg/2000px-English_Pok%C3%A9mon_logo.svg.png
[segue]: https://developer.apple.com/library/ios/recipes/xcode_help-IB_storyboard/Chapters/StoryboardSegue.html

 
