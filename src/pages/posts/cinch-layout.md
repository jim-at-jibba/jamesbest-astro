---
slug: "/cinch-a-layout-library-for-react-native"
title: "CINCH — A layout library for React Native"
description: "I am super pumped to talk about the release of CINCH, a layout library for React Native."
pubDate: "2019-09-27"
hero: "../images/posts/cinch-layout/cinch-logo.png"
tags: ["reactnative", "react", "javascript"]
layout: "../../layouts/BlogPostLayout.astro"
---

I am super pumped to talk about the release of CINCH, a layout library for React Native.

> CINCH - Making React Native layouts a cinch

The aim of the library is to take away the complexities of flexbox layouts in React Native. Cinch used Styled Components as a base for build the styled layout components and as such is a peer dependency of Cinch.

The library is inspired by Hedron and follows a similar API. I had been in discussion with Garet, Hedrons creator about adding React Native support to Hedron and having taken a look, I decided to create a stand-alone library. I did not want to bloat the Hedron package adding complexity to the build config. Also, the React Native implementation would not use a lot of the current functionality of Hedron.
Example

![Alt Text](https://thepracticaldev.s3.amazonaws.com/i/x9tel61ko2y00a346p0l.png)

Let have a look at a simple example.

Create a new project

`react-native init cinchExample && cd $_`

Now let's install Cinch.

`yarn add cinch-layout`

Open your project in your favourite editor and replace the contents of App.js with the following:

```javascript
import * as React from "react"
import { SafeAreaView, Text } from "react-native"
import { CinchProvider, CinchBounds, CinchBox } from "./src"

export default class App extends React.Component {
  render() {
    return (
      <SafeAreaView style={{ flex: 1, backgroundColor: "white" }}>
        <CinchProvider>
          <CinchBounds flex={1} debug flexDirection="vertical">
            <CinchBox debug style={{ width: "50%" }}>
              <Text>Hello</Text>
            </CinchBox>

            <CinchBox flex={2} debug={true}>
              <Text>Hello</Text>
            </CinchBox>

            <CinchBox flex={1} debug={true}>
              <Text>Hello</Text>
            </CinchBox>
          </CinchBounds>
          <CinchBounds>
            <CinchBox debug valign={"center"} halign="right">
              <Text>Hello</Text>
            </CinchBox>
            <CinchBox debug style={{ marginHorizontal: 20 }}>
              <Text>Hello</Text>
            </CinchBox>
          </CinchBounds>
        </CinchProvider>
      </SafeAreaView>
    )
  }
}
```

Finally, start your React Native project.

This simple example shows you how easy it is to create complex flexbox layouts.

The debug prop will add borders to each Cinch component giving you a better visual display of the View components.

Each Cinch component will default to flex: 1 but you can easily change the flex value by adding the `flex={}` props.

Need to change the `flexDirection`? Just use the `flexDirection={}` prop. Aligning the child elements could not be easier. Just add a `valign={}` or `halign={}` prop and Cinch will work out the placement based on the `flexDirection` props.

Each Cinch component also accepts the React Native style props and will pass those styles to the correct component.

And that is about it. The package is still new and will have some issues

# Thanks for reading 🙏

Check out our software focused podcast - [Salted Bytes](https://open.spotify.com/show/7IdlgpiDfYcOdCn57mPLvH?si=X1ArfHvqQXSOAfc1h7Y_Eg)
