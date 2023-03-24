# Element Capture

## Introduction
Pre-existing mechanisms such as [getDisplayMedia()](https://www.w3.org/TR/screen-capture/#dom-mediadevices-getdisplaymedia) allow Web applications to initiate screen-capture. If the user chooses to share a tab, the capturing application receives a video MediaStreamTrack. Mechanisms such as [Region Capture](https://w3c.github.io/mediacapture-region/) allow this track to be mutated; these mechanisms allow Web applications to perform some operation on the captured frames. (In the case of [Region Capture](https://w3c.github.io/mediacapture-region/), this mutation consists of cropping.)

The Element Capture document introduces a new mutation mechanism which we name "restriction". After a Web application "restricts" a video track to a given target-element, frames produced on that video track only consist information from the target-element and (and its descendants). Phrased differently, the track becomes a capture of the DOM sub-tree rooted at the target-element.

## Sample use cases

Consider the following Web application.
![image](https://user-images.githubusercontent.com/22117736/227632506-7674f0dc-dcf6-4ebc-9c47-59212cc9ccbc.png)

This Web app combines a productivity suite and a video conferencing tool. It uses [Region Capture](https://w3c.github.io/mediacapture-region/) to crop away remote participants' own videos before it transmits the main content area to everyone.

But if other HTMLElements end up being drawn on top of the "main content area", they also get captured. This is not always desirable - see the following illustration.

<p align="center">
  <img src="https://user-images.githubusercontent.com/22117736/227634359-a98136df-45dd-427d-802f-452be4612862.png" width="750"></img>
</p>

Element Capture allows this app to capture only the main content area, excluding any occluding content such as drop-down lists.
