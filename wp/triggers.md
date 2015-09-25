---
layout: page
title: Triggers on Windows Phone
permalink: /tag-mobile-sdks/wp/triggers/
---

Triggers allow your application to detect and react to PowaTag Tags.

Once a Tag has been detected your application must [retrieve the Workflow]({{site.baseurl}}/tag-mobile-sdks/wp/workflows/) associated with the tag from the PowaTag API to determine the action(s) that should be surfaced to the user.

A number of triggers are currently supported:

* Audio
* QR
* Touch To Buy (Mobile Web or App2App)

<br />

# Audio Tags

1. Audio tag detection requires the use of the audio recording permission. Add ID_CAP_MICROPHONE Capability in WMAppManifest.xml file.
2. Create handlers for OnBarcodeTagDetected and OnDetectorStarted events:

    <pre>private void audioTag_OnVolumeChanged(object sender, VolumeChangedEventArgs e) {
       Debug.WriteLine(e.Volume);
   }

   private void audioTag_OnAudioTagDetected(object sender, AudioTagDetectedEventArgs e) {
       MessageBox.Show(e.AudioTag.Reference, "Tag Discovered");
   }

   private void audioTag_OnDetectorStopped(object sender, DetectorStoppedEventArgs e) {
       MessageBox.Show("Detection");
   }</pre>

3. Create AudioTagDetector instance and assign EventHandlers:

    <pre>AudioTagDetector audioTagDetector = new AudioTagDetector();
   audioTagDetector.OnAudioTagDetected += audioTag_OnAudioTagDetected;
   audioTagDetector.OnVolumeChanged    += audioTag_OnVolumeChanged;
   audioTagDetector.OnDetectorStopped  += audioTag_OnDetectorStopped;</pre>

4. Start audio tag detection:

    <pre>audioTagDetector.StartDetection();</pre>

<br />

**Sample**

To see an example of this code in action, import the AudioSample project from the PowaTag SDK.

<br />

# QR Tags

1. Barcode tag detection requires use of the system camera. Add ID_CAP_ISV_CAMERA Capability in WMAppManifest.xml file.

2. Create handlers for OnBarcodeTagDetected and OnDetectorStarted events:

    <pre>private void OnTagDetected(object sender, BarcodeTagDetectedEventArgs e) {
       MessageBox.Show(e.BarcodeTag.Reference);
   }

   private void OnDetectionStarted(object sender, DetectorStartedEventArgs e) {
       // assign retrieved VideoBrush to a supported UI control
       Dispatcher.BeginInvoke(() => Canvas.Background = e.VideoBrush);
   }</pre>

3. Create BarcodeTagDetector instance and assign EventHandlers:

    <pre>BarcodeTagDetector barcodeTagDetector = new BarcodeTagDetector();
   barcodeTagDetector.OnBarcodeTagDetected += OnTagDetected;
   barcodeTagDetector.OnDetectorStarted    += OnDetectionStarted;</pre>

4. Call StartDetection and StopDetection according to your App lifecycle, for example when navigation happens:

    <pre>protected override async void OnNavigatedTo(NavigationEventArgs e) {
       await audioTagDetector.StartDetection();
   }

   protected override void OnNavigatedFrom(NavigationEventArgs e) {
       audioTagDetector.StopDetection();
   }</pre>

<br />

**Sample**

To see an example of this code in action, import the BarcodeSample project from the PowaTag SDK.

<br />

# Next Get the Workflow for a Tag

See [Workflows]({{site.baseurl}}/tag-mobile-sdks/wp/workflows/) for how to retrieve workflow information for a tag from the PowaTag API.

<br />

# Troubleshooting Sample Apps

If you have a problem running a sample app, view the [FAQ]({{site.baseurl}}/tag-mobile-sdks/wp/faq/) for solutions.
