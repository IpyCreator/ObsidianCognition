  

  

“A historical detour

Before diving into the underlying system, you’ll take a brief, historical detour to the 1970s. Apple’s platforms are all based on a version of Unix, the operating system famously developed at Bell Labs in the 1970s. Surprisingly, you can trace why code signing is a pain back to Unix’s original assumptions!

In Unix, a program has the same access and privileges as the user running it. This made sense back in the 1970s because you had to code and load your own programs using punched cards. But in modern times, this is not a good assumption. Nowadays, the programs you run are typically third-party apps that you didn’t write yourself.

For security reasons, your apps should not have the same access as you do. Third-party apps shouldn’t have free rein over your files, data and hardware. A malicious or compromised app that can do everything you can could wreak havoc on your system.

Consider how you would handle this issue if you were Apple. What kind of system would you build to protect users from the consequences of this decades-old assumption? Are you thinking of a system that separates a user’s privileges from[…]”

  

  

“Broadly speaking, the resources that require permission fall into five categories:

Hardware: Camera, microphone, sensors, etc.

Network access: Inbound and outbound traffic.

Data from other apps: Contacts, calendars, email, etc.

User files: Files from the file system or the Files app.

Special functionality: Push notifications, HomeKit access, etc.

Note: This is where terminology gets confusing. In technical documentation, you’ll rarely see the word “permission”, but you’ll see “entitlements”, “capabilities” and “resources”. In a nutshell, developers request entitlements to add capabilities to their app so it can access system resources.

The diagram below represents how the App Sandbox works. It’s not based on the real architecture or implementation of the actual system, but it can help you identify and understand all the big pieces.”

  

  

![[Screenshot_2023-09-05_at_7.57.39_PM.png]]

“At a high level, there are resources outside the sandbox, components inside the sandbox and a runtime policy system in the middle that grants or blocks access based on the app’s entitlements. The following sections describe each in detail.”

  

“Runtime policy system

At runtime, a sandboxed app might attempt a restricted operation, like getting location updates while the app isn’t running. The policy system intercepts this operation and, based on a number of checks, allows or disallows the action.

For example, in the case of background location updates, you need three things:

The user’s explicit consent to start getting location data.

A description of why you’re asking for location data in the app’s Info.plist.

The Background Modes location entitlement.

”

  

  

  

“ As mentioned before, each sandbox container has its own file system, which the sandboxed app can access without restriction.

”

“There’s a “locked area” in the middle of the sandbox that contains the app binary. It’s “locked” because Xcode digitally signed it using codesign. After code-signing something, it’s impossible to change anything about it without breaking the code seal, which is easy to check.

The scroll icon next to the app icon represents the provisioning profile, a file embedded in the app’s binary. You can think of it as a public declaration that details who the app is, where it can run and what it wants to do.”

Excerpt From  
iOS App Distribution & Best Practices  
By Pietro Rea  
  
[https://itunes.apple.com/WebObjects/MZStore.woa/wa/viewBook?id=0](https://itunes.apple.com/WebObjects/MZStore.woa/wa/viewBook?id=0)  
This material may be protected by copyright.  

  

  

  

  

![[Screenshot_2023-09-05_at_8.09.07_PM.png]]