---
layout: page
title: Triggers on Android
permalink: /tag-mobile-sdks/0.9.6/android/triggers/
---

Triggers allow your application to detect and react to PowaTag Tags.

Once a Tag has been detected your application must [retrieve the Workflow]({{site.baseurl}}/tag-mobile-sdks/0.9.6/android/workflows/) associated with the tag from the PowaTag API to determine the action(s) that should be surfaced to the user.

A number of triggers are currently supported:

* Audio
* QR
* Touch To Buy (Mobile Web or App2App)

<br />


# Audio Tags

1. Audio tag detection requires the use of the audio recording permission. Add the following entry to your manifest:

    <pre>&lt;uses-permission android:name="android.permission.RECORD_AUDIO" /&gt;</pre>

2. Create an AudioTagDetector and set an AudioTagDetectorListener to be notified of any events:

    <pre>@Override
   protected void onCreate(final Bundle savedInstanceState) {
     super.onCreate(savedInstanceState);
     audioTagDetector = new AudioTagDetector(this);
     audioTagDetector.setAudioTagDetectorListener(new AudioTagDetectorListener() {
       @Override
       public void onAudioTagDetected(final AudioTagDetector audioTagDetector,final Tag audioTag) {
         showAlertDialog("PowaTag Audio Tag Detected", audioTag.getReference());
       }
       @Override
       public void onVolumeChanged(final AudioTagDetector audioTagDetector, final float volume) {
         // Volume from 0.0f to 1.0f
         showAlertDialog("Current Volume", Float.toString(volume));
       }
       @Override
       public void onDetectorStopped(final AudioTagDetector audioTagDetector, final PowaTagException exception) {
         if (exception != null) {
           // Detector stopped due to an error.
           showAlertDialog("Exception!", exception.getMessage());
         }
       }
     });
   }</pre>

3. Call startDetection and stopDetection when required:

    <pre>public void onStartButtonClick() {
     audioTagDetector.startDetection();
   }

   public void onStopButtonClick() {
     audioTagDetector.stopDetection();
   }</pre>

4. To check if the audio tag detector is actively listening for tags use:

	<code>audioTagDetector.isDetecting();</code>

<br/>


# QR Tags

1. Barcode tag detection requires use of the system camera and optionally the flash. Add the following entry to your manifest to grant the application the necessary permissions and features:

    <pre>&lt;uses-permission android:name="android.permission.CAMERA" /&gt;
   &lt;uses-permission android:name="android.permission.FLASHLIGHT"/&gt;

   &lt;uses-feature android:name="android.hardware.camera" /&gt;
   &lt;uses-feature android:name="android.hardware.camera.flash" /&gt;
   &lt;uses-feature android:name="android.hardware.camera.autofocus" /&gt;</pre>

2. Add the BarcodeTagDetectorView to your layout XML:

    <pre>&lt;com.powatag.android.sdk.triggers.barcode.BarcodeTagDetectorView
       android:id="@+id/barcode_detector_view"
       android:layout_width="match_parent"
       android:layout_height="match_parent"/&gt;</pre>

3. Find the BarcodeTagDetectorView and set a BarcodeTagDetectorViewListener to be notified of events:

    <pre>protected void onCreate(final Bundle savedInstanceState) {
     super.onCreate(savedInstanceState);
     setContentView(R.layout.activity_barcode_tag_detector_view);
     barcodeTagDetectorView = (BarcodeTagDetectorView) findViewById(R.id.barcode_detector_view);
     barcodeTagDetectorView.setBarcodeTagDetectorViewListener(new BarcodeTagDetectorViewListener() {
       @Override
       public void onBarcodeTagDetected(final BarcodeTagDetectorView barcodeTagDetectorView,final Tag barcodeTag, final Image image, final List&lt;PointF&gt; barcodeRegion) {
         showAlertDialog("PowaTag Barcode Tag Detected", barcodeTag.getReference());
       }
       @Override
       public void onNonPowaTagBarcodeDetected(final BarcodeTagDetectorView barcodeTagDetectorView, final Barcode barcode, final Image image, final List&lt;PointF&gt; barcodeRegion) {
         // Some other kind of barcode unsupported by PowaTag was detected.
         showAlertDialog("Unsupported Barcode Detected", barcode.getCode());
       }
       @Override
       public void onDetectorStarted(final BarcodeTagDetectorView barcodeTagDetectorView) {
         // Camera feed is live.
       }
       @Override
       public void onDetectorStopped(final BarcodeTagDetectorView barcodeTagDetectorView,final PowaTagException exception) {
         if (exception != null) {
           // Detector stopped due to an error.
           showAlertDialog("Exception!", exception.getMessage());
         }
       }
     });
     }</pre>

4. Call startDetection and stopDetection from appropriate lifecycle methods in your Activity:

    <pre>@Override
   protected void onResume() {
     super.onResume();
     barcodeTagDetectorView.startDetection();
   }

   @Override
   protected void onPause() {
     super.onPause();
     barcodeTagDetectorView.stopDetection();
   }</pre>


5. To check if the audio tag detector is actively listening for tags use:

	<code>audioTagDetector.isDetecting()</code>
<br />


# Touch to Buy Tags

1. Touch to Buy tag detection requires the following entry in your manifest:

	<pre>&lt;intent-filter&gt;
        &lt;action android:name="android.intent.action.VIEW" /&gt;
        &lt;data android:host="powat.ag" /&gt;
        &lt;data android:scheme="hellopowatag" /&gt;
    &lt;/intent-filter&gt; </pre>

2. Create an instance of the <code>AppLinkTagDetector</code>

	<pre>Set&lt;String&gt; schemes = new HashSet&lt;&gt;();
	schemes.add("hellopowatag");
	AppLinkTagDetector detector = new AppLinkTagDetector(schemes);

	AppLink appLink = detector.detectAppLink(intent);
	if (appLink != null) {
		processDetectedTag(appLink.getTag());
	}</pre>


<br/>


# Next Get the Workflow for a Tag

See [Workflows]({{site.baseurl}}/tag-mobile-sdks/0.9.6/android/workflows/) for how to retrieve workflow information for a tag from the PowaTag API.

<br />


# Sample

To explore this topic in more detail, including package imports and trigger implementation, [import the HelloPowaTagSample]({{site.baseurl}}/tag-mobile-sdks/0.9.6/android/start/#importing-the-sample-app) app and review the <code>ScanActivity</code> class.

<br />


# Troubleshooting Sample Apps

If you have a problem running a sample app, view the [FAQ]({{site.baseurl}}/tag-mobile-sdks/0.9.6/android/faq/) for solutions.

