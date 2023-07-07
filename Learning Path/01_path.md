# What is devops ? The big picture

Devops is a mindset/culture that seeks faster development cycles of software. It leverages continuous integration/continuous delivery and is usually coupled with the agile methodology. The classic *infinite* devops representation is the **plan > code > build > test > release > deploy > operate > monitor** cycle.
The goal is to make this cycle as efficient as possible and with the lowest amount of friction possible. It takes two key areas of the software development cycle, the development and the operations parts and connects them into a unique workflow.


# What does one need to learn ?

There is a lot to cover in the devops field. A few resources describe a roadmap one can follow to learn the foundations of devops engineering. Two examples are this [roadmap]() and this [blog post](https://www.kasten.io/kubernetes/resources/blog/devops-learning-curve). I will also be learning a few aspects contained in the [backend engineering roadmap](https://roadmap.sh/backend) which covers topics that are close to devops but also goes more into software engineering. These resources will serve as a guideline for my learning journey.

The goal here is to be as much hands-on as possible.
I will be working on a project all along my journey. The project will be a personal website that will host my information (CV), a blog and should allow for further extensions in case I want to host some demo apps.

## Learning a programming language/software engineering

I already have a few years of experience using python as my primary programming language. I am currently learning Java at my job which will nicely complement my python skills. Concerning python I am still learning flask as a web framework and how to properly test code which is an area I did not put enough emphasis on. Proper testing is also an element I am learning on my day job as the company I am working with is building its software using test-driven development.

I am also currently revisiting the basics of algorithms and data structures, where I follow the [algorithms illuminated](https://www.algorithmsilluminated.org/) book series and implement essential algorithms and datastructures in my [algorithms](https://github.com/Cernewein/Algorithms) github repo.

An area I need to expand my knowledge on is software engineering, which is an area where the [backend engineering roadmap](https://roadmap.sh/backend) will come in handy. The key areas I will be focusing on are software design and architecture and backend technologies.

## Learning linux basics

Knowing how to work with linux is an essential skill for a devops engineer as the linux OS is used everywhere. Luckily I already have experience managing a linux system as I managed a server at my previous job. I will still be revisiting some knowledge to fill in my gaps.


## Understanding networking

Similarly to linux, knowledge about networking is an essential part of devops engineering as it is networking that allows the apps we are building to communicate with other apps and with the users. Networking fundamentals to learn include DNS, subnetting, DHCP, the OSI model, firewalls, load balancers, proxies...

## Learning to use a cloud provider

A lot of systems are now being deployed on the cloud. The biggest players in the cloud ecosystem are AWS, Azure and GCP. Once I get to this part I will choose one provider and stick to it. I will seek out to master the skills necessary to get one of the certifications offered by the cloud providers, for example the [Azure fundamentals certification](https://learn.microsoft.com/fr-fr/certifications/azure-fundamentals/).

## Containerization/container orchestration

Containerization is the practice of shipping software in a containerized environment where all dependencies for running the software are included, and most importantly where they are controlled. This allows for a consistent deployment experience since the environment required for running an application is portable.

## Infrastructure as code and app configuration automation

In the same spirit as containerization, infrastructure as code allows for specifying the requirements for the system that we want to put into place using code. This way building infrastructure is repeatable and safe. The most common tool used here is Terraform.

Similarly, tools like Ansible allow for repeatible configuration of applications.

## CI/CD Pipelines

Instead of manually updating our apps when new code is pushed, the process can be automated using CI/CD. The two essential elements of this pipeline are :

- Continuous integration (CI): this is used in the building, testing and releasing phase of the devops cycle.
- Continuous deployment (CD) : this is used for automatically updating the running app once it has passed the CI part. CD pushes fresh code to the different environments where the app is running.

The most common tool used here is Jenkins.

## Application and system monitoring

When the apps are running, how does one make sure everything is running smoothly ? This is where application and system monitoring comes in. The goal of application monitoring is to make sure the app is running correctly. Infrastructure monitoring on the other hand makes sure the server doesn't have any problems, for example that it has enough resources to handle the load. An appreciated tool here is for example Datadog for both monitoring scenarios.