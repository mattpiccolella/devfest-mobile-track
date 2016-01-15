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



<a href="#top" class="top" id="level2">Top</a>
## Level 2: Simple List View

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

 
