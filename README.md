# Web photo sender

The first part of internship task.

+ Go to [website](https://letsdonothing.github.io/web-photo-sender/) and take a photo
+ If you have installed the application from [second part](https://github.com/letsdonothing/ios-photo-receiver), then it will open with your photo

## Requirements

+ **npm** and **node.js** installed

## Doesn't work correctly

+ Any OS except iOS (and iOS without app installed) just displays your photo without having to go to the application (obviously, yes?)
+ iOS doesn't even display camera stream via any browser other than Safari

## To do

+ Checking URL and force to do nothing if something goes wrong (Safari in iOS displays an error if you don't have the application)
+ Add support for *Universal links*
