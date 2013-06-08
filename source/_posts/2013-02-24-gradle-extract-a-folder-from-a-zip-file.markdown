---
layout: post
title: "Gradle: Extract a folder from a zip file"
date: 2013-02-24 16:14
comments: true
categories: gradle
---

*Let's say you have a zip file with the containing these two folders(lib, classes) and you
want to extract the lib folder to another zip file.*

*home.zip<br/>
 -lib<br/>
 -classes*

*first extract the zip contents into a folder*
``` groovy
task extractZip(type: Copy) {
	from zipTree('home.zip')
	destinationDir = file('temp')
}	
```

*then use another task to create the desired zip file*
``` groovy
task createZip(type: Zip, dependsOn: extractZip) {
	baseName = 'lib'
	from ('temp/home') { include 'lib/**'}
	destinationDir = file('dist')
}
```
