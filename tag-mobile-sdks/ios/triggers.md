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

1. Create a PTKAudioTagDetector in your ViewController and set a PTKAudioTagDetectorDelegate to be notified of any events:

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

2. Call startDetection and stopDetection when required:

    <pre>- (IBAction)startButtonClick {
	   [self.audioTagDetector startDetection];
   }

   - (IBAction)stopButtonClick {
	   [self.audioTagDetector stopDetection];
   }</pre>

<br />

**Sample**

To see an example of this code in action, import the AudioSample project from the PowaTag SDK.

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

<br />

**Sample**

To see an example of this code in action, import the BarcodeSample project from the PowaTag SDK.

<br />

# Next Get the Workflow for a Tag

See [Workflows]({{site.baseurl}}/tag-mobile-sdks/ios/workflows/) for how to retrieve workflow information for a tag from the PowaTag API.

<br />

# Troubleshooting Sample Apps

If you have a problem running a sample app, view the [FAQ]({{site.baseurl}}/tag-mobile-sdks/ios/faq/) for solutions.
