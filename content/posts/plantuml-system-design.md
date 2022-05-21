+++
title = "PlantUML: The Ultimate System Design Aid"
date = "2019-01-25"
author = "Lorem Ipsum"
cover = "plantumlsystemdesign/cover.png"
description = "How to code, save, version control and copy/paste your engineering diagrams with amazing speed?"
+++

As I gain more experience in writing software, I am constantly in search of tools that make my life easy and also save a lot of time. Some of the tools that i use are —

1. Vim Everywhere — Starting from my code editors, to terminal command line, to my browser — all have vim keybindings. Heck, I have even customised my keyboard to create a [HYPERKEY setup](https://gist.github.com/dragod812/fee8f5d4e3a24cf99ccf5e34d7f57d53) for vim normal mode via [Hammerspoon](https://www.hammerspoon.org/) and [Karabiner](https://karabiner-elements.pqrs.org/).
2. [Sourcegraph](https://sourcegraph.com/search) — Code search in all repositories. Using the Sourcegraph extension in VSCode is very seamless.
3. [Alfred](https://www.alfredapp.com/) — This app gives you a Mac Spotlight like search capability, but on steroids. I create custom web searches in this app to get to websites with parameterised URLs in a matter of seconds.

But [PlantUML](https://plantuml.com/) is one of the most impressive tools!

What if i told you, You can code your architecture, interaction, sequence and class diagrams ? PlantUML does exactly that!

I have created templates for different types of Engineering diagrams, which I can quickly pull up and start charting my design!

For example this is my Architecture / Interaction Diagram Template.


```
@startuml
!include <awslib/AWSCommon>
!include <awslib/AWSSimplified.puml>
!include <awslib/Compute/all.puml>
!include <awslib/mobile/all.puml>
!include <awslib/general/all.puml>
!include <awslib/GroupIcons/all.puml>
!include <awslib/NetworkingAndContentDelivery/all.puml>
skinparam ComponentStyle rectangle

rectangle "High Level Design" {
  Users(users, "People", "")
  frame Clients {
    Mobileclient(appclient, "App", "")
    Client(webclient, "Web", "")
  }
  ELBNetworkLoadBalancer(lb, "Load Balancer", "")
  GlobalAccelerator(cdn, "CDN", "")

  component "Service" as service
  queue "Message Queue" as q
  database "Database" as db {
    frame table {
      database user as userdb
    }
  }
}


users ..> Clients
cdn <-> appclient
appclient --> lb :1: message
webclient ..> lb :2: more message
lb --> service
lb --> q
service --> userdb

@enduml
```

Just paste the above code on the [online server](https://www.plantuml.com/plantuml). This should generate something like this —

![architecture template](/plantumlsystemdesign/architecture-template.png)

Now to add interaction between components in this diagram you just have to add —

`service -> q : Push Elements into queue`

![interaction example](/plantumlsystemdesign/interaction-sample.png)

There you go — You can code, save, version control, copy/paste your diagrams with amazing speed! You also have a [lot of choices](https://github.com/awslabs/aws-icons-for-plantuml/blob/master/AWSSymbols.md) for the icons that you use in these diagrams.

You want to chart a sequence diagram ? This is my template —

```
@startuml
participant Participant as Foo
actor       Actor       as Foo1
boundary    Boundary    as Foo2
control     Control     as Foo3
entity      Entity      as Foo4
database    Database    as Foo5
collections Collections as Foo6
queue       Queue       as Foo7
alt success
  Foo -> Foo1 : To actor
  activate Foo1
  note left: this is a first note
else failure
  Foo -> Foo2 : To boundary
  note over Foo2, Foo1: Both are great items
end
par Run in parallel go routines
  Foo -> Foo3 : To control
else
  Foo -> Foo4 : To entity
else
  Foo -> Foo5 : To database
end
group Grouped Actions
  loop 100 times
    Foo -> Foo6 ++ #FFBBBB: activate collections with color
    Foo <- Foo6 -- : deactivate after done
    destroy Foo6
  end
  Foo -> Foo7: To queue
end
Foo1 -> Foo : work done
deactivate Foo1
@enduml
```

![sequence diagram template](/plantumlsystemdesign/sequence-diagram-template.png)

I urge you to explore all the different diagrams in [plantuml.com](https://plantuml.com/). It will definitely make your life very easy. For example, I was able to chart the high level design of a very basic chat application in like 10 mins →

![chat diagram](/plantumlsystemdesign/chat-diagram.png)






