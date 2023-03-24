# Element Capture

Pre-existing mechanisms such as [getDisplayMedia()](https://www.w3.org/TR/screen-capture/#dom-mediadevices-getdisplaymedia) allow Web applications to initiate screen-capture. If the user chooses to share a tab, the capturing application receives a video MediaStreamTrack. Mechanisms such as [Region Capture](https://w3c.github.io/mediacapture-region/) allow this track to be mutated; these mechanisms allow Web applications to perform some operation on the captured frames. (In the case of [Region Capture](https://w3c.github.io/mediacapture-region/), this mutation consists of cropping.)

The Element Capture document introduces a new mutation mechanism which we name "restriction". After a Web application "restricts" a video track to a given target-element, frames produced on that video track only consist information from the target-element and (and its descendants). Phrased differently, the track becomes a capture of the DOM sub-tree rooted at the target-element.
