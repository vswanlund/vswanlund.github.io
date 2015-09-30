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

1. Audio tag detection requires the use of the audio recording permission. Add <code>ID_CAP_MICROPHONE</code> Capability in WMAppManifest.xml file.


2. Create handlers for OnAudioTagDetected, OnVolumeChanged and OnDetectorStopped events:

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

5. To check if the audio tag detector is actively listening for tags use:

	<code>audioTagDetector.IsDetecting();</code>

<br />


# QR Tags

1. Barcode tag detection requires use of the system camera. Add <code>ID_CAP_ISV_CAMERA</code> capability in WMAppManifest.xml file.

2. Create handlers for all <code>BarcodeTagDetector</code> events:

    <pre>private void OnTagDetected(object sender, BarcodeTagDetectedEventArgs e) {
       MessageBox.Show(e.BarcodeTag.Reference);
   }
   
   private void OnNonPowaTagDetected(object sender, NonPowaTagBarcodeDetectedEventArgs e) {
       //Barcode detected that is not a PowaTag barcode.
       MessageBox.Show(e.BarcodeTag.Reference);
   }
   
   private void OnDetectionStarted(object sender, DetectorStartedEventArgs e) {
       // assign retrieved VideoBrush to a supported UI control
       Dispatcher.BeginInvoke(() => Canvas.Background = e.VideoBrush);
   }
   
   private void OnDetectionStopped(object sender, DetectorStoppedEventArgs e) {
       // assign retrieved VideoBrush to a supported UI control
       Dispatcher.BeginInvoke(() => Canvas.Background = e.VideoBrush);
   }</pre>

3. Create BarcodeTagDetector instance and assign EventHandlers:

    <pre>BarcodeTagDetector barcodeTagDetector = new BarcodeTagDetector();
   barcodeTagDetector.OnBarcodeTagDetected += OnTagDetected;
   barcodeTagDetector.OnNonPowaTagBarcodeDetected += OnNonPowaTagDetected;
   barcodeTagDetector.OnDetectorStarted    += OnDetectionStarted;
   barcodeTagDetector.OnDetectorStopped    += OnDetectionStopped;</pre>

4. Call StartDetection and StopDetection according to your App lifecycle, for example when navigation happens:

    <pre>protected override async void OnNavigatedTo(NavigationEventArgs e) {
       await audioTagDetector.StartDetection();
   }

   protected override void OnNavigatedFrom(NavigationEventArgs e) {
       audioTagDetector.StopDetection();
   }</pre>
   
5. To check if the audio tag detector is actively listening for tags use:

	<code>tagDetector.IsDetecting();</code>

<br />

# Touch to Buy Tags

1. Following entry needs to be added to manifest WMAppManifest.xml:
    
	<pre>&lt;Extensions&gt;
		&lt;Protocol Name="hellopowatag" NavUriFragment="encodedLaunchUri=%s" TaskID="_default" /&gt;
	&lt;/Extensions&gt; </pre>
	
2. Create a custom URI mapper class:

	<pre>public class AppLinkUriMapper : UriMapperBase
	{
		public const string EncodedLaunchUri = "encodedLaunchUri";
		public override Uri MapUri(Uri uri)
		{
			string uriString = uri.ToString();
 
			// URI association launch for my app detected
			if (uriString.Contains(EncodedLaunchUri + "=" + "hellopowatag"))
			{
				int embeddedUriIndex = uriString.IndexOf(EncodedLaunchUri) + EncodedLaunchUri.Length + 1;
				string embeddedUriString = uriString.Substring(embeddedUriIndex);
				return new Uri("/WorkflowPage.xaml?encodedLaunchUri=" + embeddedUriString, UriKind.Relative);
			}
 
			// Otherwise perform normal launch.
			return uri;
		}
	}

3. During App initialization set RootFrame.UriMapper to the instance of your UriMapper class (E.g. in App class constructor):
	
	<pre>RootFrame.UriMapper = new AppLinkUriMapper();</pre>


4. In WorkflowPage.OnNavigatedTo method process the app link if present:

	<pre>protected override void OnNavigatedTo(NavigationEventArgs e)
	{
		if (NavigationContext.QueryString.ContainsKey(AppLinkUriMapper.EncodedLaunchUri))
		{
			AppLink appLink =
				new AppLinkTagDetector(new HashSet<string> { "hellopowatag" }).DetectAppLink(
					NavigationContext.QueryString[AppLinkUriMapper.EncodedLaunchUri]);
		}
	}</pre>

<br/>

# Sample

To see examples of these three triggers, [import the HelloPowaTagSample]({{site.baseurl}}/tag-mobile-sdks/wp/start/#importing-the-sample-app/) app and review the <code>MainPageViewModel</code>.

<br />

# Next Get the Workflow for a Tag

See [Workflows]({{site.baseurl}}/tag-mobile-sdks/wp/workflows/) for how to retrieve workflow information for a tag from the PowaTag API.

<br />

# Troubleshooting Sample Apps

If you have a problem running a sample app, view the [FAQ]({{site.baseurl}}/tag-mobile-sdks/wp/faq/) for solutions.
