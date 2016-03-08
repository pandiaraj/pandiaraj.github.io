---
layout: post
title: Apache Spark - Find out most repeated word in a file
summary: Find out most repeated word in a file using Apache Spark.
comments: true
tweet: true
---
We have tried word count example in Apache Spark. 

    val lines = sc.textFile("README.md")
    val wordCount = lines.flatMap(line => line.split(" ")).filter(word => word.trim().length() > 0).map(word => (word, 1)).reduceByKey((a, b) => a + b)

This will return RDD of tuples containing each word and its count.

Lets find out most repeated word in a text file.

    val mostRepeatedWord = lines.flatMap(line => line.split(" ")).filter(word => word.trim().length() > 0).map(word => (word, 1)).reduceByKey((a, b) => a + b).reduce((a, b) => if (a._2 > b._2) a else b)

The last reduce method, reduce((a, b) => if (a._2 > b._2) a else b), reduces the RDD by comparing the max count value of each word.

Below is the less verbose version of the above command,

    val mostRepeatedWord = lines.flatMap(_.split(" ")).filter(_.trim().length() > 0).map((_, 1)).reduceByKey(_+_).reduce((a, b) => if (a._2 > b._2) a else b)
