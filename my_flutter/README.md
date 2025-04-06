<!DOCTYPE html>
<html>
<head>
<title>my_flutter README</title>
</head>
<body>
<h1>my_flutter</h1>
<p>A new Flutter module project.</p>
<h2>Getting Started</h2>
<p>For help getting started with Flutter development, view the online <a href="https://flutter.dev/">documentation</a>.</p>
<p>For instructions integrating Flutter modules to your existing applications, see the <a href="https://flutter.dev/to/add-to-app">add-to-app documentation</a>. Follow the steps <a href="https://flutter-ko.dev/development/add-to-app/ios/project-setup">here</a>.</p>
<hr>
<p>Create Parent folder which will have iOS app and flutter module</p>
<p><strong>Step:</strong> Create flutter module App by executing following cmd</p>
<pre><code>flutter create --template module my_flutter</code></pre>
<p>Then run the project</p>
<p>Then create iOS app and open pod file</p>
<h3>Option A - Embed with CocoaPods and the Flutter SDK</h3>
<p>This method requires every developer working on your project to have a locally installed version of the Flutter SDK. The Flutter module is compiled from source each time the app is built. Simply build your application in Xcode to automatically run the script to embed your Dart and plugin code. This allows rapid iteration with the most up-to-date version of your Flutter module without running additional commands outside of Xcode.</p>
<p>The following example assumes that your existing application and the Flutter module are in sibling directories. If you have a different directory structure, you may need to adjust the relative paths.</p>
<pre><code>some/path/
├── my_flutter/
│   └── .ios/
│       └── Flutter/
│           └── podhelper.rb
└── MyApp/
    └── Podfile</code></pre>
<p>If your existing application (MyApp) doesn’t already have a Podfile, run <code>pod init</code> in the MyApp directory to create one. You can find more details on using CocoaPods in the CocoaPods getting started guide.</p>
<p>Add the following lines to your Podfile:</p>
<pre><code>flutter_application_path = '../my_flutter'
load File.join(flutter_application_path, '.ios', 'Flutter', 'podhelper.rb')</code></pre>
<p>For each Podfile target that needs to embed Flutter, call <code>install_all_flutter_pods(flutter_application_path)</code>.</p>
<pre><code>target 'MyApp' do
  install_all_flutter_pods(flutter_application_path)
end</code></pre>
<p>In the Podfile’s post_install block, call <code>flutter_post_install(installer)</code>.</p>
<pre><code>post_install do |installer|
  flutter_post_install(installer) if defined?(flutter_post_install)
end</code></pre>
<p><strong>Note:</strong> The <code>flutter_post_install</code> method (added in Flutter 3.1.0), adds build settings to support native Apple Silicon arm64 iOS simulators. Include the <code>if defined?</code> check to ensure your Podfile is valid if you are running on older versions of Flutter that don’t have this method.</p>
<p>Run <code>pod install</code>.</p>
<p><strong>Note:</strong> When you change the Flutter plugin dependencies in <code>my_flutter/pubspec.yaml</code>, run <code>flutter pub get</code> in your Flutter module directory to refresh the list of plugins read by the <code>podhelper.rb</code> script. Then, run <code>pod install</code> again from your application at <code>some/path/MyApp</code>.</p>
<p>The <code>podhelper.rb</code> script embeds your plugins, <code>Flutter.framework</code>, and <code>App.framework</code> into your project.</p>
<p>Your app’s Debug and Release build configurations embed the Debug or Release build modes of Flutter, respectively. Add a Profile build configuration to your app to test in profile mode.</p>
<p><strong>Tip:</strong> <code>Flutter.framework</code> is the bundle for the Flutter engine, and <code>App.framework</code> is the compiled Dart code for this project.</p>
<p>Open <code>MyApp.xcworkspace</code> in Xcode. You can now build the project using ⌘B.</p>
<p><strong>Note:</strong> WHEN YOU ARE ADDING THE <code>Info-Release.plist</code> add to correct path</p>
<p>Then ADD FLUTTER SCREEN <a href="https://docs.flutter.dev/add-to-app/ios/add-flutter-screen">here</a>.</p>
</body>
</html>
