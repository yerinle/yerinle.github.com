---
layout: post
title: "Gradle: filter a file using ant filters"
date: 2013-02-27 05:46
comments: true
categories: gradle
---

*If you want to replace tokens in a file with values from a properties file*

*For example your file (profile.txt) contains the entry*
```
name=@name@
``` 
*and your properties file (values.properties) contains an entry*
```
name=Ted Jurey
```

``` groovy
import org.apache.tools.ant.filter.ReplaceTokens

task filter(type: Copy) {
	from 'profile.txt'
	into 'filtered'
	def propreties = new Properties()
	file('values.properties').withInputStream { 
		properties.load(it)
	}

	filter(ReplaceTokens, tokens: properties)
}
```