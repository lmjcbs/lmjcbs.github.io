---
layout: post
title:      "API Architectures"
date:       2020-05-25 20:46:03 +0000
permalink:  api_architectures
---


Working with ruby and more specifcally Ruby on Rails, I built and communicated with RESTful APIs for all of my projects during my time at Flatiron. However I've recently been looking into different styles of API architectures and I hope to look at what different API architectures aim to achieve and the possible drawbacks that come with that.

### REST Architecture

REST is a web architecture that uses HTTP protocol. It is widely used for the development of web applications. REST stands for REpresentational State Transfer and it's is a protocol that does not enforce any rules about how it should be implemented at a lower level. It provides guidelines for high-level architecture implementation. 

Web services based on REST are known as RESTful web services. In these applications, every component is a resource and these resources can be accessed by a common interface using HTTP standard methods. The following four HTTP methods are commonly used in REST-based architecture:

* GET - Read-only access to a resource.
* POST - Ability to modify/create resource.
* PUT - Similar to POST, used for updating a resource.
* DELETE - Removes a resource.

### RPC Architecture

RPC stands for Remote Procedure Call. As the name suggests, the idea is that we can invoke a function/method on a remote server. RPC protocol allows one to get the result for a problem in the same format regardless of where it is executed. It can be local or in a remote server using better resources.

It's because of the ability to produce a result in the same format regardless of execution environment that makes RPC a strong contender for a microservices approach, whereby you have clusters of microservices that could be written in differing languages that are stronger at performing their isolated task, but are still able to communicate between each other seamlessly due to this feature.

RPC is very popular for IoT devices and other solutions requiring custom contracted communications for low-power devices, as much of the computation operations can be offloaded to another device. Traditionally, RPC can be implemented as RPC-XML and RPC-JSON.

### API Call Comparison

##### REST

DELETE /resource/1


##### RPC

POST /deleteResource
{
    "id": 1
}
