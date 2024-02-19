---
layout: post
title: "Beware Of Cloudwatch Ingestion Costs"
date: 2024-02-19 07:10:33 +0800
categories: aws costs
---
I kind of love CloudWatch.

It's not the most advanced. It doesn't have the best features. It's UX is..., let's call it workmanlike. And yet, it does most things well enough, and the integration with the rest of the AWS ecosystem is veeery smooth. 

For most of my projects I find that CloudWatch has everything I need. I can keep logs, create metrics, set up alarms and build dashboards without ever having to install and manage my own solutions, or involve an external vendor. For most things, the cost of learning and interoperating with something else doesn't make sense. 

All that said, I kind of hate CloudWatch pricing. And I specifically hate how dominating the ingestion cost is, and how much that seems to trip up people who are trying to control their logging costs.

As [this piece from Kevin Lin highlights](https://bit.kevinslin.com/p/a-deep-dive-into-observability-pricing) (the piece is essentially advertising for his company, but it's still pretty useful), most observability solutions charge you very little for ingest, prefering to get their money from storage , query and other service costs. After all, the more data you ingest, the more locked in you are.

CloudWatch is not like that. 

As of the writing of this post, [CloudWatch charges $0.50 per GB of data ingested](https://aws.amazon.com/cloudwatch/pricing) ($0.25 if you are using the Infrequent Access tier). Meanwhile, storage costs 0.03 per GB/month. That means that, if you are using standard logs, it takes almost 17 months for the storage costs to match the cost you pay the second you ingest the logs in the first place.

For a lot of organizations the first thing they think of doing when they see their log costs ballooning is to delete old logs and diminish the log retention period. Things that are very likely to have only minor effects on their costs.

In fact, when it comes to CloudWatch, pretty much the only meaningful cost optimization you can make is having less logs. Which can be a pain, both because you might want to have those logs around, and because it gets harder and harder to guarantee that every developer is using logging sensibly as the organization gets larger. In fact, that's the moment where that smooth integration with the AWS ecosystem can become a problem, since it's very easy to send a bunch of logs to CloudWatch without having to think about it, and sometimes even without realizing it.

Which is not to say that switching to another vendor is a panacea. Those costs can become very large too, although what they charge you for might be somewhat different. But it does mean that you have to be very aware of the dominance of ingest costs when you are thinking about using CloudWatch for your logs.