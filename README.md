## Discord Server: 
### https://discord.gg/mDxtRwr3je

## For Developers
### Setting Up A Watch Page
To setup a watch page you first have to create a new class that inherits `WatchPage` bellow is an example of a page using Banana OS which has two buttons that you can click
```cs
using System.Text;
using BananaOS;
using BananaOS.Pages;
using UnityEngine;

namespace YourProjectsNamespace
{
    public class Page : WatchPage
    {
        // Constants to avoid magic strings and to make the code more maintainable
        private const string PageTitle = "Example";
        private const string NotificationMessage = "<align=center><size=5>Notification</size></align>";

        // Default colors for the notification
        private readonly Color notificationColor = Color.blue;
        private readonly Color textColor = Color.white;

        // Main Menu Display Control
        public override bool DisplayOnMainMenu => true;

        // What will be shown on the main menu if DisplayOnMainMenu is set to true
        public override string Title => PageTitle;

        // This method is called after the watch is completely setup
        public override void OnPostModSetup()
        {
            // Set max index for the selection so the indicator stays on the screen
            selectionHandler.maxIndex = 1;
        }

        // This method returns the content to be displayed on the watch screen
        public override string OnGetScreenContent()
        {
            var stringBuilder = new StringBuilder();

            // Adding colorized page title
            stringBuilder.AppendLine($"<color=yellow>==</color> {PageTitle} <color=yellow>==</color>");

            // Adding button options with selection indicators
            stringBuilder.AppendLine(selectionHandler.GetOriginalBananaOSSelectionText(0, "ButtonLabel1"));
            stringBuilder.AppendLine(selectionHandler.GetOriginalBananaOSSelectionText(1, "ButtonLabel2"));

            return stringBuilder.ToString();
        }

        // This method handles button press events
        public override void OnButtonPressed(WatchButtonType buttonType)
        {
            switch (buttonType)
            {
                case WatchButtonType.Up:
                    selectionHandler.MoveSelectionUp();
                    break;

                case WatchButtonType.Down:
                    selectionHandler.MoveSelectionDown();
                    break;

                case WatchButtonType.Enter:
                    HandleEnterButtonPress();
                    break;

                case WatchButtonType.Back:
                    ReturnToMainMenu();
                    break;
            }
        }

        // This method handles the Enter button press logic
        private void HandleEnterButtonPress()
        {
            switch (selectionHandler.currentIndex)
            {
                case 0:
                    // Add logic for the first button (Test Button)
                    HandleTestButtonAction();
                    break;

                case 1:
                    // Add logic for the second button (Test Button 2)
                    HandleTestButton2Action();
                    break;

                default:
                    // Add fallback logic or notification if needed
                    break;
            }
        }

        // Example action for Test Button 1
        private void HandleTestButtonAction()
        {
            // This can trigger a notification or some logic
            BananaNotifications.DisplayNotification($"{NotificationMessage} Button 1 clicked!", notificationColor, textColor, .8f);
        }

        // Example action for Test Button 2
        private void HandleTestButton2Action()
        {
            // This can trigger a different notification or logic
            BananaNotifications.DisplayNotification($"{NotificationMessage} Button 2 clicked!", notificationColor, textColor, .8f);
        }
    }
}
```
<br>


### Displaying Notifications
There are multiple ways you can choose to display notifications using the `DisplayNotification` method here is an example of a basic implementation of `DisplayNotification`
```cs
BananaNotifications.DisplayNotification("This is a basic example of displaying a notification");
```
this notifcation will have the default parameters which is a yellow background color, white text color, and the duration of 3 or the implementation of this
<br>
<br>
Here is an example of what the example above looks like in full form
```cs
BananaNotifications.DisplayNotification("This is a basic example of displaying a notification", Color.yellow, Color.white, 3);
```
This is an example of an implementation that changes these parameters so the background color would be red, the text color would be green, the notification duration would be 6, and the text that would be displayed would be "This is a example of displaying a notification"
```cs
BananaNotifications.DisplayNotification("This is a example of displaying a notification", Color.red, Color.green, 6);
```
There is also two other methods that are for basic warning and error messages without changing the paramters `DisplayErrorNotification()` and `DisplayWarningNotification()`

### This product is not affiliated with Gorilla Tag or Another Axiom LLC and is not endorsed or otherwise sponsored by Another Axiom LLC. Portions of the materials contained herein are property of Another Axiom LLC. ©2021 Another Axiom LLC.
