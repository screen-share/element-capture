# Security and Privacy Questionnaire for Element Capture

## Questions to Consider

### 2.1. What information might this feature expose to Web sites or other parties, and for what purposes is that exposure necessary?

This feature does not, in itself, expose additional information to Web sites or third parties. This feature allows the shaping of information already exposed to Web sites that self-capture through pre-existing means (such as getDisplayMedia).

### 2.2. Do features in your specification expose the minimum amount of information necessary to enable their intended uses?

Yes.

### 2.3. How do the features in your specification deal with personal information, personally-identifiable information (PII), or information derived from them?

Not applicable.

### 2.4. How do the features in your specification deal with sensitive information?

Not applicable.

### 2.5. Do the features in your specification introduce new state for an origin that persists across browsing sessions?

No.

### 2.6. Do the features in your specification expose information about the underlying platform to origins?

No.

### 2.7. Does this specification allow an origin to send data to the underlying platform?

No.

### 2.8. Do features in this specification enable access to device sensors?

No.

### 2.9. Do features in this specification enable new script execution/loading mechanisms?

No.

### 2.10. Do features in this specification allow an origin to access other devices?

No.

### 2.11. Do features in this specification allow an origin some measure of control over a user agent’s native UI?

No. (Other than that the user agent's native UI will inform the user that tab-capture is being used. This feature builds on top of tab-capture; the native UI will have been shown regardless.)

### 2.13. How does this specification distinguish between behavior in first-party and third-party contexts?

This feature does not distinguish first-party and third-party contexts.

### 2.14. How do the features in this specification work in the context of a browser’s Private Browsing or Incognito mode?

Not applicable.


### 2.Does this specification have both "Security Considerations" and "Privacy Considerations" sections?

Yes.

### 2.16. Do features in your specification enable origins to downgrade default security protections?

No.

### 2.17. How does your feature handle non-"fully active" documents?

This feature only works for documents which use pre-existing mechanisms to self-capture. A non-"fully active" document will have this capture-session interrupted, thereby also terminating the use of this feature.

### 2.18. What should this questionnaire have asked?

A Web application that's engaged in self-capture can bypass origin isolation and read pixels from a third-party iframe. This is pre-existing. The main concern raised by the feature introduced hereby, is that it allows a Web application to observe pixels which the user cannot see.

We contend that although this sounds scary at first, it does not actually worsen security and/or privacy, because no new attacks can be launched against the user.
* First, a malicious Web application that managed to trick the user into self-capture, would already be able to obtain access to the same set of pixels before the user had a chance to stop it - load an iframe in the background, then bring it to the forefront; by the time the user mentally registers it, the pixels will have already been recorded by the attacker.
* Second, if a malicious application wishes to read these pixels surreptitiously, this can be done using a combination of any number of techniques. The include:
   * Display the content briefly.
   * Display the content piecemeal. (As far as one pixel at a time.)
   * Display the content at a low opacity.

Further, we contend that for non-malicious applications, this feature is a great boon to user privacy, as it allows responsible applications to pare down the set of pixels to which they gain access. This allows such applications to avoid the accidental recording, or transmission to remote users, of unintended pixels, which could be of a private nature. One example is a video-conferencing into which an iframe is embedded with content to be shared with remote participants; by using our feature, applications can guarantee that private chat messages that overlap the iframe which is intended to be shared, would not be accidentally captured and transmitted to remote participants.
