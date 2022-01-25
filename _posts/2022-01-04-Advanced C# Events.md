---
layout:     post
title:      2022-01-04-Advanced C# Event
subtitle:   Events
date:       2022-01-03
author:     BY HY
header-img: img/post-bg-csharp-dotnet.png
catalog: true
tags:
    - c#
    - Event
---

# BackGround

Events in .Net are based on the delegate model. The delegate model follows observer design pattern, which enables a subscriber to register with and receive notifications from a provider. An event handler pushes a notification that an event has happened, and an event receiver receives that notification and defines a response to it. This article describes the major components of the delegate model, how to implement and consume events in applications.

*Event* is a message sent by an object to signal the occurrence of an action. In the context of events, a delegate is an intermediary (or pointer-like mechanism) between the event source and the code that handles the event.

.NET supports below two delegates with events:  *EventHandler*, *EventHandler<TEventArgs>*. Both two eventhandler do not have return type value and take two parameters (an object for the source of the event, and an object for event data)

Delegates are multi-cast, which means that they can hold references to more than one event-handling method.

*Event Data* is usually represented by an event data class. The .NET event data naming convention is ended with *EventArgs*. E.g. SerialDataReceivedEventHandler is associated with SerialDataReceivedEventArgs. The *EventArgs* class is the very base class for all event data classes. 

* EventArgs is also the class you use when an event does not have any data associated with it. 
* You can pass the [EventArgs.Empty](https://docs.microsoft.com/en-us/dotnet/api/system.eventargs.empty) value when no data is provided.

An Event Handler method in the event receiver is used to respond to an event. Your event handlers should subscribe to the event.



