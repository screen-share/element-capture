# Element Capture

## Introduction
Pre-existing mechanisms such as [getDisplayMedia()]([url](https://www.w3.org/TR/screen-capture/#dom-mediadevices-getdisplaymedia)) allow Web applications to initiate screen-capture. If the user chooses to capture a tab, mechanisms such as [Region Capture]([url](https://w3c.github.io/mediacapture-region/)) mutate the resulting video track and perform an operation on all subsequent frames produced. (In the example of [Region Capture]([url](https://w3c.github.io/mediacapture-region/)), the operation consists of cropping frames to the frame's intersection with the bounding box of a target-element.)

Element Capture introduces a new mutation mechanism which we name "restriction". When an application "restricts" a video track to a given target-element, frames produced on the restricted video track only consist of information from the target-element and its descendants. Phrased differently, the track becomes a capture of the DOM sub-tree rooted at the target-element.

## Sample use cases

Consider the following Web application.
![image](https://user-images.githubusercontent.com/22117736/227632506-7674f0dc-dcf6-4ebc-9c47-59212cc9ccbc.png)

This Web app combines a productivity suite and a video conferencing tool. It uses [Region Capture](https://w3c.github.io/mediacapture-region/) to crop away remote participants' own videos before it transmits the main content area to everyone.

But if other HTMLElements end up being drawn on top of the "main content area", they also get captured. This is not always desirable - see the following illustration.

<p align="center">
  <img src="https://user-images.githubusercontent.com/22117736/227634359-a98136df-45dd-427d-802f-452be4612862.png" width="750"></img>
</p>

Element Capture allows this app to capture only the main content area, excluding any occluding content such as drop-down lists.

A partial list of use-cases includes:
* Removing sensitive content from video-captures, such as private messages.
* Removing distracting content from video-captures, such as drop-down lists.
* Client-side rendering.

## Sample Code

Code in the capture-target:

```js
const mainContentArea = navigator.getElementById('mainContentArea');
const cropTarget = await CropTarget.fromElement(mainContentArea);
sendCropTarget(cropTarget);

function sendCropTarget(cropTarget) {
  // Either send the crop-target using postMessage(),
  // or pass it on locally within the same document.
}
```

Code in the capturing-document:

```js
async function startRestrictedCapture(cropTarget) {
  const stream = await navigator.mediaDevices.getDisplayMedia();
  const [track] = stream.getVideoTracks();
  if (!!track.restrictTo) {
    handleError(stream);
    return;
  }
  await track.restrictTo(cropTarget);
  transmitVideoRemotely(track);
}
```
