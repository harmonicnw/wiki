# Create Mobile App using PhoneGap, jQuery Mobile and Yeoman

## Install PhoneGap

http://panopticdev.com/blog2014/phonegap-mac-osx-setup-configuration-android-ios/

## Install Yeoman PhoneGap Generator
see https://www.npmjs.org/package/generator-phonegap

```
npm install -g generator-phonegap
```
 
## Generate Yeoman phonegap project

```
mkdir myproject
cd myproject
yo phonegap sudo npm install
```

## Add jQuery mobile to project

...

## Modify config.xml

add:
```
<!-- preferences -->
<preference name="phonegap-version" value="3.4.0" />
<preference name="BackupWebStorage" value="none" />

<!-- platforms -->
<gap:platform name="ios" />
<gap:platform name="android" />

<!-- access -->
<access origin="*" />

<!-- icons -->

<icon src="www/icon.png" />
    
<icon gap:density="ldpi" gap:platform="android" src="www/res/icon/android/drawable-ldpi/icon.png" />
<icon gap:density="mdpi" gap:platform="android" src="www/res/icon/android/drawable-mdpi/icon.png" />
<icon gap:density="hdpi" gap:platform="android" src="www/res/icon/android/drawable-hdpi/icon.png" />
<icon gap:density="xhdpi" gap:platform="android" src="www/res/icon/android/drawable-xhdpi/icon.png" />

<icon src="www/res/icon/ios/icon-40.png" gap:platform="ios" width="40" height="40" />
<icon src="www/res/icon/ios/icon-40@2x.png" gap:platform="ios" width="80" height="80" />
<icon src="www/res/icon/ios/icon-50.png" gap:platform="ios" width="50" height="50" />
<icon src="www/res/icon/ios/icon-50@2x.png" gap:platform="ios" width="100" height="100" />
<icon src="www/res/icon/ios/icon-60.png" gap:platform="ios" width="60" height="60" />
<icon src="www/res/icon/ios/icon-60@2x.png" gap:platform="ios" width="120" height="120" />
<icon src="www/res/icon/ios/icon-72.png" gap:platform="ios" width="72" height="72" />
<icon src="www/res/icon/ios/icon-72@2x.png" gap:platform="ios" width="144" height="144" />
<icon src="www/res/icon/ios/icon-76.png" gap:platform="ios" width="76" height="76" />
<icon src="www/res/icon/ios/icon-76@2x.png" gap:platform="ios" width="152" height="152" />
<icon src="www/res/icon/ios/icon-small.png" gap:platform="ios" width="29" height="29" />
<icon src="www/res/icon/ios/icon-small@2x.png" gap:platform="ios" width="58" height="58" />
<icon src="www/res/icon/ios/icon.png" gap:platform="ios" width="57" height="57" />
<icon src="www/res/icon/ios/icon@2x.png" gap:platform="ios" width="114" height="114" />

<!-- splash screens -->
<gap:splash src="www/res/screen/android/drawable-land-hdpi/screen.png" gap:platform="android" gap:density="hdpi" />
<gap:splash src="www/res/screen/android/drawable-land-ldpi/screen.png" gap:platform="android" gap:density="ldpi" />
<gap:splash src="www/res/screen/android/drawable-land-mdpi/screen.png" gap:platform="android" gap:density="mdpi" />
<gap:splash src="www/res/screen/android/drawable-land-xhdpi/screen.png" gap:platform="android" gap:density="xhdpi" />
<gap:splash src="www/res/screen/android/drawable-port-hdpi/screen.png" gap:platform="android" gap:density="hdpi" />
<gap:splash src="www/res/screen/android/drawable-port-ldpi/screen.png" gap:platform="android" gap:density="ldpi" />
<gap:splash src="www/res/screen/android/drawable-port-mdpi/screen.png" gap:platform="android" gap:density="mdpi" />
<gap:splash src="www/res/screen/android/drawable-port-xhdpi/screen.png" gap:platform="android" gap:density="xhdpi" />

<gap:splash src="www/res/screen/ios/Default-568h@2x~iphone.png" gap:platform="ios" width="640" height="1136" />
<gap:splash src="www/res/screen/ios/Default-Landscape@2x~ipad.png" gap:platform="ios" width="2048" height="1536" />
<gap:splash src="www/res/screen/ios/Default-Landscape~ipad.png" gap:platform="ios" width="1024" height="768" />
<gap:splash src="www/res/screen/ios/Default-Portrait@2x~ipad.png" gap:platform="ios" width="1536" height="2048" />
<gap:splash src="www/res/screen/ios/Default-Portrait~ipad.png" gap:platform="ios" width="768" height="1024" />
<gap:splash src="www/res/screen/ios/Default@2x~iphone.png" gap:platform="ios" width="640" height="960" />
<gap:splash src="www/res/screen/ios/Default~iphone.png" gap:platform="ios" width="320" height="480" />   
```

## Generate Android keystore

```
cd [project_root]/AppName.keystore
keytool -genkey -v -keystore my-release-key.keystore -alias alias_name -keyalg RSA -keysize 2048 -validity 10000
```

## Update package.json

Edit name

Update grunt-phonegap to latest version
```
"grunt-phonegap": "~0.15.2"
```

## Modify Gruntfile.js

Documentation: https://www.npmjs.org/package/grunt-phonegap

### Add plugins:
```
phonegap: {
 	config: {
 		...
 		plugins: [
 			'https://github.com/phonegap-build/StatusBarPlugin.git'
 		],
 		...
 	}
 }
```

### Add splash screens
```
screens: {
	android: {
		ldpi: '<%= yeoman.dist %>/res/screen/android/drawable-port-ldpi/screen.png',
		ldpiLand: '<%= yeoman.dist %>/res/screen/android/drawable-land-ldpi/screen.png',
		mdpi: '<%= yeoman.dist %>/res/screen/android/drawable-port-mdpi/screen.png',
		mdpiLand: '<%= yeoman.dist %>/res/screen/android/drawable-land-mdpi/screen.png',
		hdpi: '<%= yeoman.dist %>/res/screen/android/drawable-port-hdpi/screen.png',
		hdpiLand: '<%= yeoman.dist %>/res/screen/android/drawable-land-hdpi/screen.png',
		xhdpi: '<%= yeoman.dist %>/res/screen/android/drawable-port-xhdpi/screen.png',
		xhdpiLand: '<%= yeoman.dist %>/res/screen/android/drawable-land-xhdpi/screen.png'
	},
	ios: {
		ipadLand: '<%= yeoman.dist %>/res/screen/ios/Default-Landscape~ipad.png',
		ipadLandx2: '<%= yeoman.dist %>/res/screen/ios/Default-Landscape@2x~ipad.png',
		ipadPortrait: '<%= yeoman.dist %>/res/screen/ios/Default-Portrait~ipad.png',
		ipadPortraitx2: '<%= yeoman.dist %>/res/screen/ios/Default-Portrait@2x~ipad.png',
		iphonePortrait: '<%= yeoman.dist %>/res/screen/ios/Default~iphone.png',
		iphonePortraitx2: '<%= yeoman.dist %>/res/screen/ios/Default@2x~iphone.png',
		iphone568hx2: '<%= yeoman.dist %>/res/screen/ios/Default-568h@2x~iphone.png'
	}
}
```

### Add Name
```
phonegap: {
	...
	config: {
		...
		name: function(){
			var pkg = grunt.file.readJSON('package.json');
			return pkg.name;
		},
		...
	}
	...
}
```

### Add Android keystore
```
phonegap: {
	...
	config: {
		...
			key: {
				store: '[AppName].keystore',
				alias: '[AppName]',
				aliasPassword: function(){
					return('[AppPass]')
				},
				storePassword: function(){
					return('[AppPass]')
				}
			},		
		...
	}
	...
}
```

### Add Android version code
```
phonegap: {
	...
	config: {
		...
		versionCode: 1,		
		...
	}
	...
}
```

### Add releases
```
phonegap: {
	...
	config: {
		...
			releases: 'releases',
			releaseName: function(){
				var pkg = grunt.file.readJSON('package.json');
				return(pkg.name + '-' + pkg.version);
			},		
		...
	}
	...
}
```
Update package version in _package.json_

Add Android release task
```
grunt.registerTask('platform-build', [
	...
	'phonegap:release:android'
]);
```

## Build for Testing in Testflight and Google Play (Alpha/Beta)

Update version in _package.json_
Increment phonegap:versionCode in _Gruntfile.js_

Build
```
grunt platform-build
```

### iOS

Copy icons and splash screens
* /app/res/icon/ios/[icons] -> /platforms/phonegap/ios/[projectName]/Classes/Resources/icons/
* /app/res/screen/ios/[splash] -> /platforms/phonegap/ios/[projectName]/Classes/Resources/splash/

Render app
* open project in Xcode (/phonegap/platforms/ios/IdiEta.xcodeproj)
* test build
* create archive (Product > Archive, Distribute..., Save for Enterprise, select profile, save to disk)

Upload .IPA to Testflight and notify Testflight users
 
### Android

Ensure icon and splash images copied over
* /app/res/icon/android/[drawable*]/icon.png -> /platforms/phonegap/android/res/[drawable*]/icon.png
* /app/res/screen/android/[drawable*]/screen.png -> /platforms/phonegap/android/[drawable*]/screen.png

Upload .APK to Google Play


## Misc Info

Consider using PhoneGap developer app (http://app.phonegap.com)


## Deprecated Android release instructions

Add path to Keystore for Ant build in /platforms/android/ant.properties
```
key.store=~/Library/Developer/AppName.keystore
key.alias=AppName   
```

Copy icons and splash screens
* /app/res/icon/android/[drawable*]/[icons] -> /platforms/phonegap/android/res/[drawable*]/[icons]
* /app/res/screen/android/[drawable*]/[splash] -> /platforms/phonegap/android/[drawable*]/[splash]
 
Run Ant release
```
cd platforms/android
ant release
```
(puts file in bin/AppName-release.apk)