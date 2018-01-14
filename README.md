# dot-app-creator
C script that creates a tiny .app bundle to pull the icon from for custom NSUserNotification images.

**Why?**
This project may seem odd and unnecesary (and it kind of is) so this is the first point I'd like to address. For those who don't have their ear to the NSStreets, there is a lot of talk about using and customising NSUserNotifications all over NSBlogs and Stack Overflow.  Hanging out on SO one Friday evening (like all the coolest of dads do) I happened upon a question asking how to create a custom icon per NSUserNotification*. The accepted answer just said this was not possible and other answers mentioned using private api calls and the contentImage property.

**Dissatisfaction**
Nothing inspires me more than someone saying something isn't possible so I set out to find a solution to the 5 year old question.  NSUserNotificationCenter chooses the icon for the notification based on the bundle identifier attached supplied to it so that was my starting point.  I figured why not create the smallest valid app bundle possible with a custom icon and bundle identifier and drop it in the /tmp/ folder. 

**Result**
It's not pretty and I would never use this in production but I learned a lot about app bundles. Turns out, macOS actually checks for a valid mach-o executable inside of the bundle so I had to write a program that just returns 1 in assembly, compile it, then create a byte array to dump into the app bundle. In the end, this is mostly the programmer version of saying "ha! in your face!" to people saying that it wasn't possible to have custom NSUserNotification icons.

**Use?**
If you do choose to use this you can call the executable from your app, pass it an icon, bundle id, and app name then swizzle the bundle id from your app to return the bundle id from the fake app. 


*https://stackoverflow.com/questions/12698332/custom-icon-for-each-nsusernotification
