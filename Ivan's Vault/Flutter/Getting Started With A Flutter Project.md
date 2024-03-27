#flutter 

- [macOS Flutter SDK](https://docs.flutter.dev/get-started/install/macos)
- [Windows Flutter SDK](https://docs.flutter.dev/get-started/install/windows)
## ## Create the app
1. Install Flutter SDK on VSCode
3. Invoke **View > Command Palette**.
4. Type “flutter”, and select the **Flutter: New Project**.
5. Select **Application**.
6. Create or select the parent directory for the new project folder.
7. Enter a project name, such as `my_app`, and press **Enter**.
8. Wait for project creation to complete and the `main.dart` file to appear.

## From CMD
1. Do the necessary steps to install flutter
2. `flutter doctor` Run to check for any issues, for me, I have yet to install Android Studio and have some problems with XCode. 
3. `flutter channel master` Switch to the master channel
4. `flutter upgrade` Download and install the latest dependencies
5. `flutter config --enable-web` To enable to web in the config from the command line
6. `flutter devices`  To check if chrome is a device
7. `flutter create <Project Name>`
Output:
```
Creating project the_basics_youtube_tutorial...
Resolving dependencies in the_basics_youtube_tutorial...
Got dependencies in the_basics_youtube_tutorial.
Wrote 129 files.

All done!
You can find general documentation for Flutter at: https://docs.flutter.dev/
Detailed API documentation is available at: https://api.flutter.dev/
If you prefer video documentation, consider: https://www.youtube.com/c/flutterdev

In order to run your application, type:

  $ cd the_basics_youtube_tutorial
  $ flutter run

Your application code is in the_basics_youtube_tutorial/lib/main.dart.

```

8. Run the project and configure it using VSCode, making sure you have the SDK installed and press the play button on the top right.
9. From then on you can use  `flutter run` in the console to run the project