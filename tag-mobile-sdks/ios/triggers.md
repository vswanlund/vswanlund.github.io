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

1. Implement the PTKAudioTagDetectorDelegate methods. and set a PTKAudioTagDetectorDelegate to be notified of any events:

  	<pre>- (void)viewDidLoad
	{
    	self.audioTagDetector = [PTKAudioTagDetector new];
		self.audioTagDetector.delegate = self;
	}
    
	&#45; (void)onAudioTagDetected:(PTKTag *)audioTag
	{
		// Handle detected tag
	}
    
	&#45; (void)onVolumeChanged:(double)volume 
	{
		// Handle volue change (display)
	}
    
    &#45; (void)onDetectorStopped:(NSError *)error 
	{
		// Hanle error if pressent
	}</pre>

2. Call startDetection and stopDetection when required:

    <pre>- (IBAction)startButtonClick 
		{
	   		[self.audioTagDetector startDetection];
  	 	}

   	&#45; (IBAction)stopButtonClick 
    {
	   [self.audioTagDetector stopDetection];
   	}</pre>
   
3. To check if the audio tag detector is actively listening for tags use:

	<pre>- (void)myMethod
		{
			if ([self.audioTagDetector isDetecting]) {
 			// It’s running 
			} else {
 			// It’s not detecting 
			}
            }</pre>

<br />


# QR Tags

1. Add the PTKBarcodeTagDetectorView to your ViewController, drop new View onto your controller, open the identity inspector and set the custom class to "PTKBarcodeTagDetectorView".

    <img src="{{ '/images/powatag_mobile_sdks_ios_triggers_barcode_class.png' | prepend: site.baseurl }}" />

2. Implement the PTKBarcodeTagDetectorViewDelegate in your ViewController:

    <pre>&#45; (void)barcodeTagDetectorView:(nonnull PTKBarcodeTagDetectorView *)barcodeTagDetectorView
	didDetectBarcode:(nonnull PTKTag *)tag
	image:(nonnull UIImage *)image
	barcodeRegion:(nonnull NSArray *)barcodeRegion
	{
		// Stop detection
		[self.detectorView stopDetection];
		// Process tag
		[self processTag:tag];
	}

	&#45; (void)barcodeTagDetectorView:(nonnull PTKBarcodeTagDetectorView *)barcodeTagDetectorView
	didDetectNonPowaTagBarcode:(nonnull PTKBarcode *)barcode
		 image:(nonnull UIImage *)image
		barcodeRegion:(nonnull NSArray *)barcodeRegion
	{
		// Stop detection and show error. 
	}

	&#45; (void)barcodeTagDetectorViewDidStart:(nonnull PTKBarcodeTagDetectorView *)barcodeTagDetectorView
	{
		// Detector started.
	}

 	&#45; (void)barcodeTagDetectorView:(nonnull PTKBarcodeTagDetectorView *)barcodeTagDetectorView
	  didStopWithError:(nullable NSError *)error
	{
		// Detector stopped handle error if present.
	}   </pre>

3. Set the delegate when your controller loads:

    <pre>- (void)viewDidLoad 
    {
     self.barcodeTagDetectorView.delegate = self;
   }</pre>

4. Call startDetection and stopDetection from appropriate lifecycle methods in your ViewController:

    <pre>- (void)viewDidAppear 
    {
     [self.barcdeTagDetectorView startDetection];
   	}

   &#45; (void)viewDidDisappear 
   {
     [self.barcodeTagDetectorView stopDetection];
   }</pre>
   
5. To check if the audio tag detector is actively listening for tags use:

	<pre>- (void)myMethod
	{
		if ([self.detectorView isDetecting]) {
		// detecting
		} else {
		// not detecting
		}
        }</pre>

<br />

# Touch to Buy Tags

1. Add the following to the <code>plist</code> file
<pre>&lt;key&gt;CFBundleURLTypes&lt;/key&gt;
	&lt;array&gt;
		&lt;dict&gt;
			&lt;key&gt;CFBundleURLName&lt;/key&gt;
			&lt;string&gt;com.powatag&lt;/string&gt;
			&lt;key&gt;CFBundleURLSchemes&lt;/key&gt;
			&lt;array&gt;
				&lt;string&gt;hellopowatag&lt;/string&gt;
			&lt;/array&gt;
		&lt;/dict&gt;
	&lt;/array&gt;</pre>


2. Create an instance of the <code>AppLinkTagDetector</code>

	<pre>- (BOOL)application:(UIApplication )application handleOpenURL:(NSURL )url
    {	
    	NSError *error; 
		PTKAppLink *tagDetector = [PTKAppLinkTagDetector detectAppLinkWithURL:url  error:&error];
		if (tagDetector) {
 			[self processTag:tagDetector.labelTag];
		} else {
 			// No/invalid tag  error.
		}
    }</pre>
    
      
<br/>

# Sample

To see detailed examples of these three triggers, [import the HelloPowaTagSample]({{site.baseurl}}/tag-mobile-sdks/ios/start/#importing-the-sample-app/) app and review the <code>ScanController.swift</code> and <code>AppDelegate.swift</code> files.

<br />

# Next Get the Workflow for a Tag

See [Workflows]({{site.baseurl}}/tag-mobile-sdks/ios/workflows/) for how to retrieve workflow information for a tag from the PowaTag API.

<br />

# Troubleshooting Sample Apps

If you have a problem running a sample app, view the [FAQ]({{site.baseurl}}/tag-mobile-sdks/ios/faq/) for solutions.
