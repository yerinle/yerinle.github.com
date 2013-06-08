---
layout: post
title: "Clojure: List public methods in a java class"
date: 2013-06-08 14:51
comments: true
categories: clojure
---

*use the function below to list the public methods in a java class*

``` clojure list-methods function
(defn list-methods
  "List methods in a class"
  [c]
  (clojure.pprint/pprint
    (map #(.toString %) (.getMethods c))))
```
*or using the threading macro*

``` clojure list-methods function : using threading macro
(defn list-methods
  "List methods in a class"
  [c]
  (->> c
    (.getMethods)
    (map #(.toString %))
    clojure.pprint/pprint))
```
*examples*

``` clojure examples
;; methods in the String class
(list-methods String)

;; public methods in the Long class
(list-methods Long)
```
