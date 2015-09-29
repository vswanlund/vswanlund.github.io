---
layout: page
title: Triggers on iOS
permalink: /tag-mobile-sdks/ios/triggers/
---

Triggers allow your application to detect and react to PowaTag Tags.

Once a Tag has been detected your application must [retrieve the Workflow]({{site.baseurl}}/tag-mobile-sdks/ios/workflows/) associated with the tag from the PowaTag API to determine the action(s) that should be surfaced to the user.

A number of triggers are currently supported:

* Audio
* QR
* Touch To Buy (Mobile Web or App2App)

<br />

# Audio Tags

1. 1. Audio tag detection requires the use of the audio recording permission. Add the following entry to your manifest:

    <pre>INSERT WHAT IS REQUIRED IN MANIFEST/&gt;</pre>
	==================

2. Create a PTKAudioTagDetector in your ViewController and set a PTKAudioTagDetectorDelegate to be notified of any events:

    <pre>- (instancetype)initWithCoder:(NSCoder *)aDecoder {
	 if (self = [super initWithCoder:aDecoder]) {
     _audioTagDetector = [PTKAudioTagDetector new];
	   _audioTagDetector.delegate = self;
   }
	 return self;
   }

   - (void)onAudioTagDetected:(PTKTag *)audioTag {
	   [[[UIAlertView alloc] initWithTitle:@"PowaTag Barcode Tag Detected" message:audioTag.reference, volume] delegate:nil cancelButtonTitle:@"OK" otherButtonTitles:nil] show];
   }

   - (void)onVolumeChanged:(double)volume {
     [[[UIAlertView alloc] initWithTitle:@"Current Volume" message:[NSString stringWithFormat:@"%.2f", volume] delegate:nil cancelButtonTitle:@"OK" otherButtonTitles:nil] show];
   }

   - (void)onDetectorStopped:(NSError *)error {
	   [[[UIAlertView alloc] initWithTitle:@"Error!" message:[error localizedDescription] delegate:nil cancelButtonTitle:@"OK" otherButtonTitles:nil] show];
   }</pre>

3. Call startDetection and stopDetection when required:

    <pre>- (IBAction)startButtonClick {
	   [self.audioTagDetector startDetection];
   }

   - (IBAction)stopButtonClick {
	   [self.audioTagDetector stopDetection];
   }</pre>
   
4. To check if the audio tag detector is actively listening for tags use:

	<code>AUDIOTAGDETECTOR ISDETECTING CODE SNIPPET</code>
	=========================

<br />


# QR Tags

1. Add the PTKBarcodeTagDetectorView to your ViewController, drop new View onto your controller, open the identity inspector and set the custom class to "PTKBarcodeTagDetectorView".

    <img src="{{ '/images/powatag_mobile_sdks_ios_triggers_barcode_class.png' | prepend: site.baseurl }}" />

2. Implement the PTKBarcodeTagDetectorViewDelegate in your ViewController:

    <pre>- (void)onBarcodeTagDetected:(PTKTag *)tag image:(UIImage *)image barcodeRegion:(NSArray *)barcodeRegion {
	 PTKTag *labelTag = tag;
	   [[[UIAlertView alloc] initWithTitle:@"Supported code" message:labelTag.reference delegate:self cancelButtonTitle:@"OK" otherButtonTitles:nil] show];
   }

   - (void)onNonPowaTagBarcodeDetected:(PTKBarcode *)barcode image:(UIImage *)image barcodeRegion:(NSArray *)barcodeRegion {
	   [[[UIAlertView alloc] initWithTitle:@"Unsupported code" message:@"unsupported barcode" delegate:self cancelButtonTitle:@"OK" otherButtonTitles:nil] show];
   }

   - (void)onDetectorStarted {
   }

   - (void)onDetectorStopped:(NSError *)error {
     [[[UIAlertView alloc] initWithTitle:@"Error!" message:[error localizedDescription] delegate:nil cancelButtonTitle:@"OK" otherButtonTitles:nil] show];
   }</pre>

3. Set the delegate when your controller loads:

    <pre>- (void)viewDidLoad {
     self.barcodeTagDetectorView.delegate = self;
   }</pre>

4. Call startDetection and stopDetection from appropriate lifecycle methods in your ViewController:

    <pre>- (void)viewDidAppear {
     [self.barcdeTagDetectorView startDetection];
   }

   - (void)viewDidDisappear {
     [self.barcodeTagDetectorView stopDetection];
   }</pre>
   
5. To check if the audio tag detector is actively listening for tags use:

	<code>TAGDETECTOR ISDETECTING CODE SNIPPET</code>

<br />

# Touch to Buy Tags - STEPS AND CODE SNIPPETS NEEDED

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
	}    
	}</pre>


<br/>

# Sample - MICHAL PLEASE PROVIDE THE CLASS NAME THAT A DEVELOPER CAN REVIEW FOR DETAILED EXAMPLES OF THE ABOVE

To see detailed examples of these three triggers, [import the HelloPowaTagSample]({{site.baseurl}}/tag-mobile-sdks/ios/start/#importing-the-sample-app/) app and review the <code>CLASS/FILE NAME</code>.

<br />

# Next Get the Workflow for a Tag

See [Workflows]({{site.baseurl}}/tag-mobile-sdks/ios/workflows/) for how to retrieve workflow information for a tag from the PowaTag API.

<br />

# Troubleshooting Sample Apps

If you have a problem running a sample app, view the [FAQ]({{site.baseurl}}/tag-mobile-sdks/ios/faq/) for solutions.
