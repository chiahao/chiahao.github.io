---
layout: post
title: "HealthKit"
date: 2023-08-06 14:04:00
category: swift
tags: [swift]
---


Thread 1: "NSHealthUpdateUsageDescription must be set in the app's Info.plist in order to request write authorization for the following types: HKWorkoutTypeIdentifier, HKQuantityTypeIdentifierDistanceWalkingRunning"


```swift
let summariesWithinRange = HKSampleQuery.predicateForSamples(withStart: startDate, end: endDate)

let query2 = HKSampleQuery(sampleType: sampleType, predicate: summariesWithinRange, limit: Int(HKObjectQueryNoLimit), sortDescriptors: nil, resultsHandler: {
```

可是得到的筆數還是太多, 而且還有分是手機的還是手錶的, 所以試看看會不會是要 ActivitySummary  



* **Sample query.** This is a general-purpose query. Use sample queries to access any type of sample data. Sample queries are particularly useful when you want to sort the results or limit the total number of samples returned. For more information, see HKSampleQuery.
* **Anchored object query.** Use this query to search for items that have been added to or deleted from the store. The first time an anchor query is run, it returns all the matching samples currently in the store. On subsequent runs, it returns only those items that have been added or deleted since the last run. For more information, see HKAnchoredObjectQuery.
* **Statistics query.** Use this query to perform statistical calculations over the set of matching samples. You can use statistics queries to calculate the sum, minimum, maximum, or average value in the set. For more information, see HKStatisticsQuery.
* **Statistics collection query.** Use this query to perform multiple statistics queries over a series of fixed-length time intervals. You will often use these queries when creating graphs. They provide a simple method for calculating things such as the total number of calories consumed each day or the number of steps taken during each five-minute interval. For more information, see HKStatisticsCollectionQuery.
* **Correlation query.** Use this query to perform complex searches of the data contained in a correlation. These queries can contain individual predicates for each of the sample types stored in the correlation. If you just want to match the correlation type, use a sample query instead. For more information, see HKCorrelationQuery.
Source query. Use this query to search for sources (apps and devices) that have saved matching samples to the HealthKit store. A source query lists all the sources that are saving a particular sample type. For more information, see HKSourceQuery.
* **Activity summary query.** Use this query to search for activity summary information for the user. Each activity summary object contains a summary of the user’s activity for a given day. You can query for either a single day or a range of days. For more information, see HKActivitySummaryQuery.
[HKActivitySummary](https://developer.apple.com/documentation/healthkit/hkactivitysummary)
資訊真的很少, 應該就是健身的 3 個圈圈。

* **Document query.** Use this query to search for health documents. For more information, see HKDocumentQuery.


> Thread 1: "HKStatisticsCollectionQuery initialResultsHandler cannot be nil"



[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


