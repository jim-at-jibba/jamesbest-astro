---
slug: "/set-up-programatic-ios-project"
title: "Setting up an Xcode Project for Programmatic UIs"
description: "Setting up an Xcode Project for Programmatic UIs"
pubDate: "2023-06-23"
hero: "../images/posts/ios-project-set-up/xcode-swift.png"
tags: ["mobile", "ios"]
layout: "../../layouts/BlogPostLayout.astro"
---

When it comes to developing iOS applications, Xcode is the go-to integrated development environment (IDE) for many developers. Xcode provides a comprehensive set of tools and features that simplify the process of building robust and user-friendly apps. One of the key decisions developers often face is whether to use storyboards or go completely programmatic for their user interfaces. In this article, we will explore the process of setting up an Xcode project for programmatic projects, allowing developers to create user interfaces entirely in code.

The first step in setting up a programmatic project is to remove the default main.storyboard file that Xcode creates when you start a new project. To do this, simply locate the file in the project navigator and delete it. Don't worry, removing the storyboard file doesn't mean you won't be able to create a user interface—it just means you'll be doing it programmatically.

Once the main.storyboard file has been deleted, navigate to the Info tab of your project settings. Look for the Main storyboard file base name entry and delete it. This step ensures that Xcode won't try to load a storyboard file at runtime.

Next, let's make sure we remove any references to storyboards in the project configuration. Use the search functionality in Xcode to search for the term 'storyboard.' This search will help us locate any remaining references to storyboards that need to be removed. One important entry to find and delete is the UISceneStoryboardFile entry. Removing this entry prevents Xcode from trying to load a storyboard file to instantiate the app's initial scene.

Now that we have removed the necessary storyboard-related configurations, we need to make some changes to the SceneDelegate.swift file. Open the file and locate the scene(\_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions) function. This function is called when a new scene is being created for the app.

Inside the scene function, we need to add a few lines of code to set up the initial scene programmatically. This code will create a new window, set the window's scene to the provided windowScene, assign a root view controller, and make the window visible. Here's the code snippet you should add to the scene function:

```swift
func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions) {
    guard let windowScene = (scene as? UIWindowScene) else { return }

    // Add these bits
    window = UIWindow(frame: windowScene.coordinateSpace.bounds)
    window?.windowScene = windowScene
    window?.rootViewController = ViewController()
    window?.makeKeyAndVisible()
}
```

The added code creates a new instance of UIWindow using the provided windowScene as its frame. It then assigns the window scene to the created window and sets the root view controller to an instance of ViewController(). Finally, the makeKeyAndVisible() function ensures that the window becomes visible.

With these changes in place, you are now ready to start building your programmatic user interface. The ViewController() class used in the example code is a placeholder for your custom view controller class. You should replace it with your own implementation or create a new view controller class that suits your project's needs.

Setting up an Xcode project for programmatic projects provides developers with greater control and flexibility over their user interfaces. By removing the default storyboard and making the necessary adjustments to the project configuration and scene delegate, developers can fully embrace a programmatic approach to UI development. Whether you prefer a purely code-based workflow or want to mix storyboards with programmatic views, Xcode offers the versatility to cater to your preferences and project requirements. Happy coding!
