A sample Android app using [whisper.cpp](https://github.com/ggerganov/whisper.cpp/) to do voice-to-text transcriptions.

To use:

1. Select a model from the [whisper.cpp repository](https://github.com/ggerganov/whisper.cpp/tree/master/models).[^1]
2. Copy the model to the "app/src/main/assets/models" folder.
3. Select a sample audio file (for example, [jfk.wav](https://github.com/ggerganov/whisper.cpp/raw/master/samples/jfk.wav)).
4. Copy the sample to the "app/src/main/assets/samples" folder.
5. Select the "release" build variant in Android Studio:
   - Open the Build Variants tool window (View > Tool Windows > Build Variants)
   - In the Build Variants window, select "release" from the Active Build Variant dropdown for the app module
   Then click the "Run" button (or press Shift+F10) to build and deploy the app to your connected Android device.
[^1]: I recommend the tiny or base models for running on an Android device.

(PS: Do not move this android project folder individually to other folders, because this android project folder depends on the files of the whole project.)

<img width="300" alt="image" src="https://user-images.githubusercontent.com/1670775/221613663-a17bf770-27ef-45ab-9a46-a5f99ba65d2a.jpg">
