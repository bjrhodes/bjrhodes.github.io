---
title: Comprobo - High growth architecture
subtitle: Comprobo approached me with a plan to move their existing application to a more scalable, growth-focused architecture.
permalink: /portfolio/comprobo/
meta-description: Comprobo approached me with a plan to move their existing application to a more scalable, growth-focused architecture.
primary_colour: "#2c3e50"
secondary_colour: "#3498db"
hero_image: "/assets/portfolio/comprobo-hero.jpg"
hero_opacity: 0.2
layout: post
---

## Comprobo had identified some weaknesses in their existing user interface which they wanted to address.

Working as team lead for a close team of local partners, I assisted with infrastructure and architecture planning to move to a highly scalable distributed system and took responsibility for design and development of their new user interface, along with the development of new backend software.

It was also critical to integrate my new team into the larger, distributed team Comprobo already had in place.

### Scalable Architecture

Comprobo's business plan is to experience very rapid growth in a short timescale, so being able to deliver at scale is a critical consideration for investors. We helped analyse their existing monolithic solution and draw out elements that can be managed as stand-alone aspects. Working with remote teams and our own developers, API interfaces between these services were then designed, before being assigned to separate teams for development.

In a microservice-based system, each component should be quite simple to develop and test in isolation, so long as their domain of responsibility is very clear. We were lucky to be involved in this project quite early on and that it was a complete rebuild of an existing project so each service's remit was well specified and implementation was smooth.

The client now has a collection of well-tested services and orchestration which can be deployed to any configuration of one or more servers. By leveraging existing configuration management and deployment solutions the system can be effectively scaled as need dictates, adding servers at busier times, whilst cost saving during quieter periods.

### Interface implementation

In the existing application, the user interface was heavily tied to the backend architecture and was not designed for performance or agility. As part of the rebuild the client had already determined that the entire interface would need to be rebuilt and so took the opportunity to bring this in line with their brand.

We consulted on design for this interface, advising on technical issues and providing an easily extensible framework for the design work based on atomic design principles. We started with a general feel for the interface in line with the brand and then designed the common elements of the interface. From here we built a coherent plan for the various components the interface would require and built these out in patternlab whilst the design team worked on composing layouts for user journeys.

As the project progressed, we could then work in an agile fashion regardless of the design team's availability. Should a new feature be requested, or an existing feature change, we could rework the feature according to the styleguide. Once built we could then bring design in to polish or approve the new feature. This approach allows a rapid fluidity to the build process with a design-first approach only being strictly necessary for entirely new components.

Some technical considerations regarding the product's function required the use of JavaScript, so we did not need to consider the rare use cases where users have no JavaScript engine or have JavaScript disabled. Thanks to this, and in order to make the product as scalable as possible, we settled on a fully JavaScript-powered build. This enables the client to rapidly serve a large number of clients without needing to tailor pages to each user, as this is handled on the client side. At the same time, adherence to best practice allows the server to optionally isometrically render the JS in the future should client-side performance be identified as a bottleneck.

The application is powered by [AngularJS](https://angular.io) and uses an authentication system based on [JWT](https://jwt.io/). This allows for a secure app either across microservices or through a shared gateway as desired and allows the client flexibility as they grow. The usage of [AngularJS](https://angular.io) allows the development team to grow easily around a fixed set of development practices and saves costs due to the range of off-the-shelf plugins, modules, and build tools available.

This approach does not suit every application, but in this case we feel it was a great choice for the client's business needs.

We look forward to a bright future for Comprobo and hope to continue developing new features and refining the application for years to come.

&nbsp;

>We have seen the time we take to integrate new features to our application rapidly improve. With our plans for rapid growth the process they have introduced gives complete piece of mind that the system will more than happily cope and will keep out expanding customer base happy.
>
>Steve Wood, Operations Director
