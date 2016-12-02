---
layout: post
title:  "Amazon announce AWS X-Ray for distributed tracing"
date:   2016-12-02 11:12:08 +0800
categories: tracing
---

At the Amazon re:Invent conference, Amazon today announced [AWS X-Ray][aws-xray] as a new entrant to the distributed tracing space. X-Ray is comparable to [Google Stackdriver Trace][google-trace], the open source [Zipkin][zipkin] project and the transaction tracking capabilities in commercial Application Performance Management offerings from [New Relic][new-relic], [App Dynamics][app-dynamics] and [IBM][ibm-apm].

The compelling reason to use X-Ray, rather than your own tracing infrastructure, is the out-of-the-box visibility into other Amazon products, such as [AWS Elastic Beanstalk][aws-elastic-beanstalk] and [Amazon API Gateway][aws-api-gateway]. The benefit here is two-fold; not only do you get rapid time-to-value, but also a level of visibility that cannot be replicated in any other product. Anyone that has spent days or weeks trying to isolate a mysterious network overhead, between a requester and provider, will understand the importance of this visibility.

It's notable that X-Ray uses sampling to manage the volume of traces, which are stored and queriable. This is necessary for tackling high traffic applications, however it limits the potential for exploitation of the tracing data. A typical use case, for an application support engineer, is to investigate an issue reported by a user. E.g., the web app timed-out whilst processing order id 123456 for bob@example.com. When sampling is used, you have no confidence whether that request will have been traced. You would need to resort to other methods, such as log analysis. This limitation undermines the value proposition that many teams are trying to get out of distributed tracing. Not all requests are created equal (consider a search query vs shopping checkout) so an ability to distinguish business critical requests is desirable.

Amazon have released their own SDK for instrumenting your application code. Whilst quick to get started, coding directly against the SDK causes vendor lock-in that makes it harder to move to a different tracing infrastructure or cloud platform.  [OpenTracing][open-tracing] is a vendor-neutral open standard that is intended to tackle exactly this problem. I'm sure we will see support for apps instrumented with OpenTracing, to send to X-Ray, in the near future.

[aws-xray]: 				https://aws.amazon.com/xray/
[aws-elastic-beanstalk]: 	https://aws.amazon.com/elasticbeanstalk/
[aws-api-gateway]: 			http://aws.amazon.com/apigateway
[google-trace]: 			https://cloud.google.com/trace/
[zipkin]: 					http://zipkin.io
[new-relic]: 				https://newrelic.com/transaction-trace
[app-dynamics]: 			https://www.appdynamics.com/info/business-transaction-tracing
[ibm-apm]: 					http://www-03.ibm.com/software/products/en/ibm-application-performance-management
[open-tracing]: 			http://opentracing.io

