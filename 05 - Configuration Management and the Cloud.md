- [Course Introduction](#course-introduction)
- [Introduction to Automation at Scale](#introduction-to-automation-at-scale)
  - [Intro to Module 1: Automating with Configuration Management](#intro-to-module-1-automating-with-configuration-management)
  - [What is scale?](#what-is-scale)
  - [What is configuration management?](#what-is-configuration-management)
  - [What is infrastructure as code?](#what-is-infrastructure-as-code)
- [Introduction to Puppet](#introduction-to-puppet)
  - [What is Puppet?](#what-is-puppet)
  - [Puppet Resources](#puppet-resources)
  - [Puppet Classes](#puppet-classes)
- [Puppet Resources](#puppet-resources-1)
  - [Resource declarations](#resource-declarations)
  - [Resource uniqueness](#resource-uniqueness)
  - [Relationships and ordering](#relationships-and-ordering)
  - [Resource types](#resource-types)
  - [Title](#title)
  - [Attributes](#attributes)
  - [Namevars and `name`](#namevars-and-name)
  - [Metaparameters](#metaparameters)
  - [Resource syntax](#resource-syntax)
    - [Basic syntax](#basic-syntax)
    - [Complete syntax](#complete-syntax)
    - [Resource declaration default attributes](#resource-declaration-default-attributes)
    - [Setting attributes from a hash](#setting-attributes-from-a-hash)
    - [Abstract resource types](#abstract-resource-types)
    - [Arrays of titles](#arrays-of-titles)
    - [Adding or modifying attributes](#adding-or-modifying-attributes)
    - [Local resource defaults](#local-resource-defaults)
- [The Building Blocks of Configuration Management](#the-building-blocks-of-configuration-management)
  - [What are domain-specific languages?](#what-are-domain-specific-languages)
  - [The Driving Principles of Configuration Management](#the-driving-principles-of-configuration-management)
- [Module Review](#module-review)
  - [Module 1 Wrap Up: Automating with Configuration Management](#module-1-wrap-up-automating-with-configuration-management)
- [Deploying Puppet Locally](#deploying-puppet-locally)
  - [Deploying Puppet](#deploying-puppet)
  - [Applying Rules Locally](#applying-rules-locally)
  - [Managing Resource Relationships](#managing-resource-relationships)
  - [Organizing Your Puppet Modules](#organizing-your-puppet-modules)
  - [The Puppet language style guide](#the-puppet-language-style-guide)
  - [Module design practices](#module-design-practices)
    - [Spacing, indentation, and whitespace](#spacing-indentation-and-whitespace)
    - [Arrays and hashes](#arrays-and-hashes)
    - [Quoting](#quoting)
    - [Escape characters](#escape-characters)
    - [Comments](#comments)
    - [Functions](#functions)
    - [Improving readability when chaining functions](#improving-readability-when-chaining-functions)
  - [Resources](#resources)
    - [Resource names](#resource-names)
    - [Arrow alignment](#arrow-alignment)
    - [Attribute ordering](#attribute-ordering)
    - [Resource arrangement](#resource-arrangement)
    - [Symbolic links](#symbolic-links)
    - [File modes](#file-modes)
    - [Multiple resources](#multiple-resources)
    - [Legacy style defaults](#legacy-style-defaults)
    - [Attribute alignment](#attribute-alignment)
    - [Defined resource types](#defined-resource-types)
  - [Classes and defined types](#classes-and-defined-types)
    - [Separate files](#separate-files)
    - [Internal organization of classes and defined types](#internal-organization-of-classes-and-defined-types)
    - [Public and private](#public-and-private)
    - [Chaining arrow syntax](#chaining-arrow-syntax)
    - [Nested classes or defined types](#nested-classes-or-defined-types)
    - [Display order of parameters](#display-order-of-parameters)
    - [Parameter defaults](#parameter-defaults)
    - [Exported resources](#exported-resources)
    - [Parameter indentation and alignment](#parameter-indentation-and-alignment)
    - [Class inheritance](#class-inheritance)
    - [Public modules](#public-modules)
    - [**Type signatures**](#type-signatures)
  - [Variables](#variables)
    - [Referencing facts](#referencing-facts)
    - [Namespacing variables](#namespacing-variables)
    - [Variable format](#variable-format)
  - [Conditionals](#conditionals)
    - [Simple resource declarations](#simple-resource-declarations)
    - [Defaults for case statements and selectors](#defaults-for-case-statements-and-selectors)
    - [Conditional statement alignment](#conditional-statement-alignment)
  - [Modules](#modules)
    - [Versioning](#versioning)
    - [Module metadata](#module-metadata)
    - [Dependencies](#dependencies)
    - [README](#readme)
    - [Documenting Puppet code](#documenting-puppet-code)
    - [CHANGELOG](#changelog)
    - [Examples](#examples)
    - [Testing](#testing)
  - [Installing Puppet Server](#installing-puppet-server)
  - [Before you begin](#before-you-begin)
    - [Supported operating systems](#supported-operating-systems)
    - [Java support](#java-support)
  - [Install Puppet Server](#install-puppet-server)
    - [What to do next](#what-to-do-next)
  - [Running Puppet Server on a VM](#running-puppet-server-on-a-vm)
- [Deploying Puppet to Clients](#deploying-puppet-to-clients)
  - [Puppet Nodes](#puppet-nodes)
  - [Puppet’s Certificate Infrastructure](#puppets-certificate-infrastructure)
  - [Setting up Puppet Clients and Servers](#setting-up-puppet-clients-and-servers)
- [Puppet SSL explained](#puppet-ssl-explained)
  - [Purpose of Puppet SSL PKI](#purpose-of-puppet-ssl-pki)
  - [A notion of PKI](#a-notion-of-pki)
  - [X509 PKI](#x509-pki)
  - [RSA system](#rsa-system)
    - [Key Generation](#key-generation)
    - [Encryption](#encryption)
    - [Decryption](#decryption)
    - [Signing message](#signing-message)
    - [Security](#security)
    - [Want to know more?](#want-to-know-more)
  - [How does this fit in SSL?](#how-does-this-fit-in-ssl)
  - [Application to Puppet](#application-to-puppet)
  - [Tips and Tricks](#tips-and-tricks)
    - [Troubleshooting SSL](#troubleshooting-ssl)
      - [Certificate content](#certificate-content)
      - [Simulate a SSL connection](#simulate-a-ssl-connection)
      - [ssldump](#ssldump)
      - [Some known issues](#some-known-issues)
      - [Looking to the CRL content:](#looking-to-the-crl-content)
    - [Fingerprinting](#fingerprinting)
    - [Dirty Trick](#dirty-trick)
    - [Multiple CA or reusing an existing CA](#multiple-ca-or-reusing-an-existing-ca)
  - [Conclusion](#conclusion)
- [Updating Deployments](#updating-deployments)
  - [Modifying and Testing Manifests](#modifying-and-testing-manifests)
  - [Safety Rolling out Changes and Validating Them](#safety-rolling-out-changes-and-validating-them)
  - [Why should you test your Puppet modules?](#why-should-you-test-your-puppet-modules)
  - [What should you be testing?](#what-should-you-be-testing)
  - [Basic structure of a test file](#basic-structure-of-a-test-file)
  - [Writing your first test cases](#writing-your-first-test-cases)
- [Module Review](#module-review-1)
  - [Module 2 Wrap Up: Deploying Puppet](#module-2-wrap-up-deploying-puppet)
- [Cloud Computing](#cloud-computing)
  - [Intro to Module 3: Automation in the Cloud](#intro-to-module-3-automation-in-the-cloud)
  - [Cloud Services Overview](#cloud-services-overview)
  - [Scaling in the Cloud](#scaling-in-the-cloud)
  - [Evaluating the Cloud](#evaluating-the-cloud)
  - [Migrating to the Cloud](#migrating-to-the-cloud)
- [Managing Instances in the Cloud](#managing-instances-in-the-cloud)
  - [Spinning up VMs in the Cloud](#spinning-up-vms-in-the-cloud)
  - [Creating a New VM Using the GCP Web UI](#creating-a-new-vm-using-the-gcp-web-ui)
  - [Customizing VMs in GCP](#customizing-vms-in-gcp)
  - [Templating a Customized VM](#templating-a-customized-vm)
- [Automating Cloud Deployments](#automating-cloud-deployments)
  - [Cloud Scale Deployments](#cloud-scale-deployments)
  - [What is Orchestration?](#what-is-orchestration)
  - [Cloud Infrastructure as Code](#cloud-infrastructure-as-code)
- [Getting started with Terraform on Google Cloud](#getting-started-with-terraform-on-google-cloud)
  - [Before you begin](#before-you-begin-1)
  - [Create a Google Cloud project](#create-a-google-cloud-project)
    - [Getting project credentials](#getting-project-credentials)
    - [Setting up Terraform](#setting-up-terraform)
    - [Configure the Compute Engine resource](#configure-the-compute-engine-resource)
    - [Validate the new Compute Engine instance](#validate-the-new-compute-engine-instance)
  - [Running a server on Google Cloud](#running-a-server-on-google-cloud)
    - [Add SSH access to the Compute Engine instance](#add-ssh-access-to-the-compute-engine-instance)
    - [Use output variables for the IP address](#use-output-variables-for-the-ip-address)
  - [Building the Flask app](#building-the-flask-app)
    - [Open port 5000 on the instance](#open-port-5000-on-the-instance)
  - [Cleaning up](#cleaning-up)
- [Terraform Enterprise GCP Reference Architecture](#terraform-enterprise-gcp-reference-architecture)
  - [»Introduction](#introduction)
  - [»Implementation Modes](#implementation-modes)
  - [»Required Reading](#required-reading)
  - [»Infrastructure Requirements](#infrastructure-requirements)
    - [»Terraform Enterprise Server (Compute Engine VM via Regional Managed Instance Group)](#terraform-enterprise-server-compute-engine-vm-via-regional-managed-instance-group)
      - [»Hardware Sizing Considerations](#hardware-sizing-considerations)
    - [»PostgreSQL Database (Cloud SQL PostgreSQL Production)](#postgresql-database-cloud-sql-postgresql-production)
      - [»Hardware Sizing Considerations](#hardware-sizing-considerations-1)
    - [»Object Storage (Cloud Storage)](#object-storage-cloud-storage)
    - [»Other Considerations](#other-considerations)
      - [»Additional GCP Resources](#additional-gcp-resources)
      - [»Network](#network)
      - [»DNS](#dns)
      - [»SSL/TLS Certificates and Load Balancers](#ssltls-certificates-and-load-balancers)
    - [»Infrastructure Diagram - Standalone](#infrastructure-diagram---standalone)
    - [»Application Layer](#application-layer)
    - [»Storage Layer](#storage-layer)
      - [»Additional Information](#additional-information)
  - [»Infrastructure Provisioning](#infrastructure-provisioning)
  - [»Normal Operation](#normal-operation)
    - [»Component Interaction](#component-interaction)
    - [»Monitoring](#monitoring)
    - [»Upgrades](#upgrades)
  - [»High Availability - Failure Scenarios](#high-availability---failure-scenarios)
    - [»Terraform Enterprise Server](#terraform-enterprise-server)
    - [»Zone Failure](#zone-failure)
    - [»PostgreSQL Database](#postgresql-database)
    - [»Object Storage](#object-storage)
  - [»Disaster Recovery - Failure Scenarios](#disaster-recovery---failure-scenarios)
    - [»Data Corruption](#data-corruption)
    - [»PostgreSQL Database](#postgresql-database-1)
    - [»Object Storage](#object-storage-1)
  - [»Multi-Region Deployment to Address Region Failure](#multi-region-deployment-to-address-region-failure)
  - [»Active/Active Implementation Mode](#activeactive-implementation-mode)
    - [»Overview](#overview)
    - [»Migration to Active/Active](#migration-to-activeactive)
    - [»Infrastructure Diagram - Active/Active](#infrastructure-diagram---activeactive)
    - [»Infrastructure Requirements](#infrastructure-requirements-1)
      - [»Active Nodes](#active-nodes)
      - [»Memory Cache](#memory-cache)
    - [»Normal Operation](#normal-operation-1)
      - [»Component Interaction](#component-interaction-1)
      - [»Replicated Console](#replicated-console)
      - [»Upgrades](#upgrades-1)
    - [»Failure Scenarios](#failure-scenarios)
      - [»Memory Cache](#memory-cache-1)
    - [»Multi-Region Implementation to Address Region Failure](#multi-region-implementation-to-address-region-failure)
- [Module Review](#module-review-2)
  - [Module 3 Wrap Up: Automation in the Cloud](#module-3-wrap-up-automation-in-the-cloud)
- [Building Software for the Cloud](#building-software-for-the-cloud)
  - [Intro to Module 4: Managing Cloud Instances at Scale](#intro-to-module-4-managing-cloud-instances-at-scale)
  - [Storing Data in the Cloud](#storing-data-in-the-cloud)
  - [Load Balancing](#load-balancing)
  - [Change Management](#change-management)
  - [Understanding Limitations](#understanding-limitations)
- [Resource quotas in GCP](#resource-quotas-in-gcp)
  - [Permissions for checking and editing quota](#permissions-for-checking-and-editing-quota)
  - [Checking your quota](#checking-your-quota)
  - [Requesting an increase in quota](#requesting-an-increase-in-quota)
  - [Quotas and resource availability](#quotas-and-resource-availability)
  - [Understanding quotas](#understanding-quotas)
    - [Regional and global quotas](#regional-and-global-quotas)
    - [CPU quota](#cpu-quota)
    - [GPU quota](#gpu-quota)
    - [VM instances](#vm-instances)
    - [Quotas for preemptible resources](#quotas-for-preemptible-resources)
    - [Disk quotas](#disk-quotas)
    - [External IP addresses](#external-ip-addresses)
    - [Instance groups](#instance-groups)
- [AWS service quotas](#aws-service-quotas)
- [Monitoring and Alerting](#monitoring-and-alerting)
  - [Getting Started with Monitoring](#getting-started-with-monitoring)
  - [Getting Alerts When Things Go Wrong](#getting-alerts-when-things-go-wrong)
  - [Service-Level Objectives](#service-level-objectives)
  - [Basic Monitoring in GCP](#basic-monitoring-in-gcp)
- [Metrics, Monitoring and Alerting](#metrics-monitoring-and-alerting)
  - [Metrics](#metrics)
    - [Work metrics](#work-metrics)
    - [Resource metrics](#resource-metrics)
    - [Other metrics](#other-metrics)
  - [Events](#events)
  - [What good data looks like](#what-good-data-looks-like)
  - [Data for alerts and diagnostics](#data-for-alerts-and-diagnostics)
  - [Conclusion: Collect ’em all](#conclusion-collect-em-all)
  - [When to alert someone (or no one)](#when-to-alert-someone-or-no-one)
    - [Levels of alerting urgency](#levels-of-alerting-urgency)
      - [Alerts as records (low severity)](#alerts-as-records-low-severity)
      - [Alerts as notifications (moderate severity)](#alerts-as-notifications-moderate-severity)
      - [Alerts as pages (high severity)](#alerts-as-pages-high-severity)
    - [When to let a sleeping engineer lie](#when-to-let-a-sleeping-engineer-lie)
    - [Page on symptoms](#page-on-symptoms)
      - [Durable alert definitions](#durable-alert-definitions)
      - [Exception to the rule: Early warning signs](#exception-to-the-rule-early-warning-signs)
  - [Conclusion: Get serious about symptoms](#conclusion-get-serious-about-symptoms)
  - [A word about data](#a-word-about-data)
  - [It’s resources all the way down](#its-resources-all-the-way-down)
    - [1. Start at the top with work metrics](#1-start-at-the-top-with-work-metrics)
    - [2. Dig into resources](#2-dig-into-resources)
    - [3. Did something change?](#3-did-something-change)
    - [4. Fix it (and don’t forget it)](#4-fix-it-and-dont-forget-it)
  - [Build dashboards before you need them](#build-dashboards-before-you-need-them)
  - [Conclusion: Follow the metrics](#conclusion-follow-the-metrics)
- [An Introduction to Metrics, Monitoring, and Alerting](#an-introduction-to-metrics-monitoring-and-alerting)
  - [Introduction](#introduction-1)
  - [What Are Metrics, Monitoring and Alerting?](#what-are-metrics-monitoring-and-alerting)
    - [What Are Metrics and Why Do We Collect Them?](#what-are-metrics-and-why-do-we-collect-them)
    - [What is Monitoring?](#what-is-monitoring)
    - [What is Alerting?](#what-is-alerting)
  - [What Type of Information Is Important to Track?](#what-type-of-information-is-important-to-track)
    - [Host-Based Metrics](#host-based-metrics)
    - [Application Metrics](#application-metrics)
    - [Network and Connectivity Metrics](#network-and-connectivity-metrics)
    - [Server Pool Metrics](#server-pool-metrics)
    - [External Dependency Metrics](#external-dependency-metrics)
  - [Factors That Affect What You Choose to Monitor](#factors-that-affect-what-you-choose-to-monitor)
  - [Important Qualities of a Metrics, Monitoring, and Alerting System](#important-qualities-of-a-metrics-monitoring-and-alerting-system)
    - [Independent from Most Other Infrastructure](#independent-from-most-other-infrastructure)
    - [Reliable and Trustworthy](#reliable-and-trustworthy)
    - [Easy to Use Summary and Detail Views](#easy-to-use-summary-and-detail-views)
    - [Effective Strategy for Maintaining Historical Data](#effective-strategy-for-maintaining-historical-data)
    - [Able to Correlate Factors from Different Sources](#able-to-correlate-factors-from-different-sources)
    - [Easy to Start Tracking New Metrics or Infrastructure](#easy-to-start-tracking-new-metrics-or-infrastructure)
    - [Flexible and Powerful Alerting](#flexible-and-powerful-alerting)
  - [Additional Terminology](#additional-terminology)
  - [Conclusion](#conclusion-1)
- [Troubleshooting and Debugging](#troubleshooting-and-debugging)
  - [What to Do When You Can't Be Physically There](#what-to-do-when-you-cant-be-physically-there)
  - [Identifying Where the Failure Is Coming From](#identifying-where-the-failure-is-coming-from)
  - [Recovering from Failure](#recovering-from-failure)
- [Module Review](#module-review-3)
  - [Module 4 Wrap Up: Managing Cloud Instances at Scale](#module-4-wrap-up-managing-cloud-instances-at-scale)

# Course Introduction

Say you're in charge of a fleet of servers. Everything is full steam ahead, until one day you discover that there's a security vulnerability in one of the applications used. Now, you need to upgrade all the servers to the latest version. If you have 10 servers in the fleet, it's probably not too much trouble to log into each one of them one after the other and install the new version. But what if you have 100 servers?  

This would get super boring and you'd likely end up making mistakes, leaving some servers with the wrong version installed. Now, imagine having to do this on 1000 servers. There's no way you're going to log into each of them to upgrade the software. So what can you do instead? In this course, we'll look into how we can apply automation to manage fleets of computers. 

We'll learn how to automate deploying new computers, keep those machines updated, manage large-scale changes, and a lot more. We'll discuss managing both physical machines running in our offices and virtual machines running in the Cloud. If this sounds overwhelming, don't worry, I'll go step-by-step with you along the way. 

I'm a Site Reliability Engineer at Google working on the team that supports G-mail. If you've never heard about Site Reliability Engineering before, let me tell you a bit about what we do. SRE is focused on the reliability and maintainability of large systems. We apply tons of automation techniques to manage them. This let's teams with only a handful of engineers have a big impact, scaling our support as our service grows. We're small, but mighty. 

My job includes a lot of different tasks. Sometimes I spend my time collaborating with partner teams on the reliability aspects of a cool new feature, like scheduling emails to send at a later time on G-mail. Other days, I write software, creating tools that help automate how we manage the service. When I'm not doing that, I might do research or architectural design for a new project. I'm also part of the on-call rotation for the service. If problems come up when I'm on call, I'm in charge of fixing them or finding the right person to fix them if I can't. 

So what will we cover in this course? We'll start by looking into an automation technique called configuration management, which lets us manage the configuration of our computers at scale. Specifically, we'll learn how to use Puppet, the current industry standard for configuration management. We'll look at some simple examples, and then see how we can apply the same concept to more complex cases. You'll be a Puppet master in no time. Later on, we'll expand our automation skills by looking into how we can make use of the Cloud to help us scale our infrastructure. We'll learn about the benefits and challenges of moving services to the Cloud. 

We'll check out some of the best practices for handling hundreds of virtual machines running in the Cloud, how to adapt our services to that, and how to troubleshoot them when things don't go according to plan. Heads up, they rarely do. 

Before we move on, I should probably tell you a little bit about myself. I discovered I was interested in IT and technology as a teenager. So when I decided to enlist in the Navy right after high school, I signed up to be an Information Systems Technician there. I served in the Navy for four years supporting IT and networks resources around the world. After leaving the Navy, I went to college and then joined Google in the IT support department. The transition from working in a very structured environment like the military to a place like Google was initially a bit hard to wrap my head around. I had to become much more comfortable in dealing with ambiguity in the problem spaces that I was working in, which meant learning to trust my own sense of judgment and prioritization. 

All along the way, I kept learning new skills and growing as a person and an engineer. So I'm excited to be here to help you take the next step in your IT career, to help you keep growing your automation skills by learning how to manage fleets of computers using configuration management, and how to work with the Cloud. Modern IT is moving more and more towards Cloud-based solutions and having a solid background in how to manage them will be even more critical for IT professionals in the future. In this course, we'll use Qwiklabs which is an environment that allows you to test your code on a virtual machine running in the Cloud. 

This lets you experience real-world scenarios, where you'll need to interact with one or more remote systems to achieve your goal. We'll build on top of the many tools that you've learned about throughout the program, like using Python for automation scripts, using Git to store versions of code, or figure out what's going on when a program doesn't behave as expected. You'll see some complex topics and videos that may not 100 percent sink in the first time around. That's totally natural. Take your time and re-watch the videos a few times if you need to, you'll get the hang of it. Also, remember that you can use the discussion forums to connect with your fellow learners and ask questions anytime you need. We're about to begin our journey, learning how we can apply automation at large scale. So let's get started.

# Introduction to Automation at Scale

## Intro to Module 1: Automating with Configuration Management

No matter the size of your team or the number of computers in your fleet, knowing how to apply automation techniques will enable you to do your work much more effectively. As I shared earlier, I'm part of the Site Reliability Engineering team that supports Gmail. My team is relatively small but the service is pretty big. Without scaling our efforts through automation and tooling, it would be impossible to help Gmail meet its reliability goals. 

While you're probably not supporting such a large-scale service right now, you'll definitely benefit from using the right automation for your needs. Being able to automate the installation of new software, the provisioning of new workstations or the configuration of a new server can make a big difference even when you're the only person in your IT department. In the coming videos, we'll kick things off by looking at some important automation concepts, like what we mean when we talk about **scale** and how we can use **configuration management** to maintain the computers in our fleet, and how we can all benefit from treating our infrastructure as code. 

These concepts are the building blocks for letting us manage a growing number of devices without having to grow the team in charge of them. We'll then get to our first taste of **Puppet**, the configuration management tool that we'll be teaching you throughout this course. We'll check out a bunch of different examples to see what Puppet rules look like. We'll also learn about the underlying concepts and how you can get it to do the heavy lifting for you. 

The concepts that we'll check out throughout this module will help you take your first steps and automating at a larger scale. Knowing how to automatically manage the configuration of the devices in your fleet will let your team handle a lot more work with the same amount of people. It also frees up time to do more interesting stuff since all the boring tasks can get automated. By the end of the module, you'll have the skills to fix a bug in existing automation, which is great news since that's exactly what you're going to do with code you provide. Funny how that works, isn't it? Almost like we planned it. Let's dive in.

## What is scale?

In this course we'll focus on making our work **scale**. <u>So what do we mean when we talk about scale?</u> Being able to scale what we do means that we **can keep achieving larger impacts with the same amount of effort** when a system scales. Well an increase in the amount of work it needs to do can be accommodated by an increase in capacity. 

For example, if the web application your company provides is scalable, that it can handle an increase in the number of people using it by adding more servers to serve requests. In short, **a scalable system is a flexible one**. Adding more computers to the pool of servers that are serving the website can be a very simple or very hard operation depending on how your infrastructure is set up. 

- To figure out how scalable your current setup is, you can ask yourself questions like 
- will adding more servers increase the capacity of the service? 
- How are new servers prepared, installed, and configured? 
- How quickly can you set up new computers to get them ready to be used? 
- Could you deploy a hundred servers with the same IT team that you have today? Or would you need to hire more people to get it done faster? 
- Would all the deployed servers be configured exactly the same way? 

Scaling isn't just about website serving content of course. If your company is rapidly hiring a lot of new employees, you'll need to have an onboarding process that can scale as needed. And as you keep adding new computers to the network, you'll need to make sure that your system administration process **can scale to the growing needs of the company**. This can include tasks like a applying the latest security policies and patches while making sure users' needs still get addressed all while more and more users join the network without new support staff to back you up. 

If making this happen sounds a bit like magic right now, remember that we're here to share the secret ingredient with you, **automation**. Automation is an essential tool for keeping up with the infrastructure needs of a growing business. By using the right automation tools, we can get a lot more done in the same amount of time. 

For example, we could deploy a whole new server by running a single command and letting the automation take care of the rest. We could also create a batch of user accounts with all the necessary permissions based on data already stored in the database, eliminating all human interaction. **Automation is what lets us scale**. It allows a small IT team to be in charge of hundreds or even thousands of computers. Okay, so what does that look like in practice? There's a bunch of different tools that we can use to achieve this. Up next, we'll talk about a type of tool called **configuration management** that can help us automate how we manage the computers in our fleets.

## What is configuration management?

Imagine your team is in charge of setting up a new server. This could be a physical computer running close to you or a virtual machine running somewhere in the cloud. To get things moving, the team installs the operating system, configures some applications and services, sets up the networking stack, and when everything is ready, puts the server into use. By manually deploying the installation and configuring the computer, we see that we're using **unmanaged configuration**. 

When we say configuration here, we're talking about everything from the current operating system and the applications installed to any necessary configuration files or policies, including anything else that's relevant for the server to do its job. When you work in IT, you're generally in charge of the configuration of a lot of different devices, not just servers. Network routers printers and even smart home devices can have configuration that we can control. For example, a network switch might use a config file to set up each of its ports. All right, so now we know what we mean when we talk about configuration. We said that manually deploying a server means that the configuration is unmanaged. So what would it mean for the configuration **to be managed**? It means using a configuration management system to handle all of the configuration of the devices in your fleet, also known as **nodes**. 

There's a bunch of different tools available depending on the devices and services involved. Typically you'll define a **set of rules** that have to be applied to the nodes you want to manage and then have a **process** that ensures that those settings are true on each of the nodes. At a small scale, unmanaged configurations seem inexpensive. If you only manage a handful of servers, you might be able to get away with doing that without the help of automation. You could log into each device and make changes by hand when necessary. And when your company needs a new database server, you might just go ahead and manually install the OS and the database software into a spare computer. But this approach doesn't always scale well. The more servers that you need to deploy, the more time it will take you to do it manually. And when things go wrong, and they often do, it can take a lot of time to recover and have the servers back online. 

**Configuration management** systems aim to **solve this scaling problem**. By managing the configuration of a fleet with a system like this, large deployments become easier to work with because the system will deploy the configuration automatically no matter how many devices you're managing. When you use configuration management and you need to make a change in one or more computers, you don't manually connect to each computer to perform operations on it. Instead, you edit the configuration management rules and then let the automation apply those rules in the affected machines. This way the changes you make to a system or group of systems are done in a systematic, repeatable way. 

Being repeatable is important because it means that the results will be the same on all the devices. A configuration management tool can take the rules you define and apply them to the systems that it manages, making changes efficient and consistent. Configuration management systems often also have some form of automatic error correction built in so that they can recover from certain types of errors all by themselves. 

For example, say you found that some application that was being used widely in your company was configured to be very insecure. You can add rules to your configuration management system to improve the settings on all computers. And this won't just apply the more secure settings once. It will continue to monitor the configuration going forward. If a user changes the settings on their machine, the configuration management tooling will detect this change and reapply the settings you defined in code. How cool is that? 

There are lots of configuration management systems available in the IT industry today. Some popular systems include **Puppet, Chef, Ansible, and CFEngine**. These tools can be used to manage locally hosted infrastructure. Think bare metal or virtual machines, like the laptops or work stations that employees use at a company. Many also have some kind of Cloud integration allowing them to manage resources in Cloud environments like Amazon EC2, Microsoft Azure, or the Google Cloud platform, and the list doesn't stop there. 

There are some platform specific tools, like SCCM and Group Policy for Windows. These tools can be very useful in some specific environments, even when they aren't as flexible as the others. For this course, we've chosen to focus on Puppet because it's the current industry standard for configuration management. Keep in mind though that selecting a configuration management system is a lot like deciding on a programming language or version control system. You should pick the one that best fits your needs and adapt accordingly, if necessary. Each has its own strengths and weaknesses. So a little research beforehand can help you decide which system is best suited for your particular infrastructure needs. There are a lot of tools out there. So be sure to check them out. Up next, we'll discuss how we can make the most out of our configuration management system using the infrastructure as code paradigm.

## What is infrastructure as code?

We've called out that when we use a configuration management system, we write **rules** that describe how the computers in our fleet should be configured. These rules are then executed by the automation, to make the computers match our desired state. This means that we can model the behavior of our IT infrastructure in **files** that can be processed by automatic tools. These files can then be tracked in a **version control system**. Remember, version control systems help us keep track of all changes done to the files, helping answer questions like **who, when, and why**. 

More importantly, they're super-useful when we need to revert changes. This can be especially helpful if a change turns out to be problematic. The paradigm of storing all the configuration for the managed devices in version controlled files is known as **Infrastructure as Code or IaC**. In other words, we see that we're using Infrastructure as Code when all of the configuration necessary to deploy and manage a node in the infrastructure is stored in version control. This is then combined with **automatic tooling** to actually get the nodes provisioned and managed. If you have all the details of your Infrastructure properly stored in the system, you can very quickly deploy a new device if something breaks down. 

Simply get a new machine, either virtual or physical, use the automation to deploy the necessary configuration, and you're done. The principals of Infrastructure as Code are commonly applied in cloud computing environments, where machines are treated like interchangeable resources, instead of individual computers. This principle is also known as treating your computers as **cattle instead of pets** because you care for them as a group rather than individually. Apologies to anyone with a pet cow. This concept isn't just for managing computers in huge data centers or globe spanning infrastructures, it can work for anything; from servers to laptops, or even workstations in a small IT department. Even if your company only has a single computer working as the mail server, you can still benefit from storing all the configuration needed to set it up in a configuration management system. 

That way if the server ever stops working, you can deploy a replacement very quickly by simply applying the rules that configure the mail server to the new computer. One valuable benefit of this process is that the configuration applied to the device **doesn't depend on a human** remembering to follow all the necessary steps. Rest assured, silly human, the result will always be the same, making the deployment **consistent**. As mentioned, having Infrastructure as Code means that we can also apply the benefits of the version control system or VCS to your infrastructure. Since the configuration of our computers is stored in files, those files can be added to a VCS. This has all the **benefits** that version control systems bring. 

- It gives us an audit trail of changes, 
- it lets us quickly rollback if a change was wrong, 
- it lets others reviewed our code to catch errors and distribute knowledge, 
- it improves collaboration with the rest of the team, 
- and it lets us easily check out the state of our infrastructure by looking at the rules that are committed. 

Not too shabby. I personally think this is one of the coolest things about IaC. The ability to easily see what configuration changes were made and roll back to a known good state is super important. It can make a big difference in **quickly recovering from an outage**, especially since changing the contents of the configuration file can be as dangerous as updating the version of an application. I've had my fair share of outages caused by an innocent-looking change with unintended side effects.

But storing all the infrastructure in a version control system lets me quickly roll back to a previously known good version so that the outage length can be minimized. On top of that, having the rules stored in files means that we can also run **automated tests** on them. It's much better to find out in a test that a configuration file has a typo in it than to find out from our users. 

In a complex or large environment, treating your IT Infrastructure as Code can help you deploy a flexible scalable system. A configuration management system can help you manage that code by providing a platform to maintain and provision that infrastructure in an automated way. Having your infrastructure stored as code means that you can **automatically deploy your infrastructure with very little overhead.** 

If you need to move it to a different location, it can be deployed, de-provisioned, and redeployed at scale in a different locale with minimal code level changes. To sum all of this up, managing your Infrastructure as Code it means that your fleet of nodes are 

- **consistent, **
- **versioned, **
- **reliable, **
- **and repeatable**. 

Instead of being seen as precious or unique, machines are treated as replaceable resources that can be deployed on-demand through the automation. Any infrastructure that claims to be scalable must be able to handle the capacity requirements of growth. Performing an action like adding more servers to handle an increase in requests is just a possible first step. 

There are other things that we might need to take into account, such as the **amount of traffic** that network can handle or the **load on the back end servers** like databases. Viewing your infrastructure in this way helps your IT team adapt and stay flexible. The technology industry is constantly changing and evolving. Automation and configuration management can help you embrace that change instead of avoiding it. Before diving into concrete examples of what this looks like, the first practice quiz of the course is coming up. These quizzes act as check-in points to help you make sure all the concepts covered in the videos are making sense. See you on the other side.

# Introduction to Puppet

## What is Puppet?

As we called out a couple of times already, in this course, we'll be learning how to apply basic configuration management concepts by using Puppet. **Puppet** is the current industry standard for managing the configuration of computers in a fleet of machines. Part of the reason why Puppet is so popular is that it's a **cross-platform tool** that's been around for a while. It's an open source project that was created in 2005, and it's gone through several different versions. As it's evolved, the tool has incorporated feedback from its users to make it more and more useful. The latest available version at the time this Google course went live is **Puppet 6**, which came out in late 2018. 

We typically deploy puppet using a client-server architecture. The **client is known as the Puppet agent**, and the **server is known as the Puppet master**. 

1. When using this model, the agent connects to the master and sends a bunch of facts that describe the computer to the master. 
2. The master then processes this information, generates the list of rules that need to be applied on the device, and sends this list back to the agent. 
3. The agent is then in charge of making any necessary changes on the computer. 

Puppet is a cross-platform application available for all Linux distributions, Windows, and Mac OS. This means that you can use the same puppet rules for managing a range of different computers. What are these rules that we keep talking about? 

Let's check out a very simple example. 

```json
class sudo {
    package { 'sudo':
            ensure => present,
            }
}
```

This block is saying that the package 'sudo' should be present on every computer where the rule gets applied. If this rule is applied on 100 computers, it would automatically install the package in all of them. This is a small and simple block but can already give us a basic impression of how rules are written in puppet. Don't worry too much about the syntax now, we'll look into what each piece means in future videos. 

There are various installation tools available depending on the type of operating system. Puppet will determine the type of operating system being used and select the right tool to perform the package installation. On Linux distributions, there are several package management systems like **APT**, **Yum**, and **DNF**. Puppet will also determine which package manager should be used to install the package. On Mac OS, there's a few different available providers depending on where the package is coming from. The Apple Provider is used for packages that are part of the OS, while the **MacPorts** provider is used for packages that come from the MacPorts Project. For Windows, we'll need to add an extra attribute to our rule, stating where the installer file is located on the local desk or a network mounted resource. Puppet will then execute the installer and make sure that it finishes successfully. If you use **Chocolatey** to manage your windows packages, you can add an extra Chocolatey provider to Puppet to support that. We'll add a link to more information about this in our next reading. 

Using rules like this one, we can get puppet to do a lot more than just install packages for us. 

- We can **add, remove, or modify configuration files stored in the system**, or **change registry entries on Windows**. 
- We can also enable, disable, start, or stop the services that run on our computer. 
- We can configure crone jobs, the scheduled tasks, add, remove, or modify Users and Groups or even execute external commands, if that's what we need. 

There's a lot to say about puppet. We won't go into absolutely every detail, but we'll cover the most important concepts in this course. The goal is to get you started with what you need to know about configuration management in general and puppet in particular. We'll also give you pointers to find out more information on your own. Up next, we'll check out the different resources we can use to define our rules.

## Puppet Resources

In our last video, we saw an example that installed the sudo package in a computer. To do that, our example used the **package keyword** declaring a package **resource**. In puppet, **resources are the basic unit for modeling the configuration** that we want to manage. In other words, each resource specifies one configuration that we're trying to manage, like a **service, a package, or a file.** 

Let's look at another example. 

```json
class sysctl {
    file { '/etc/sysctl.d':
         ensure => directory,
         }
}
```

In this case, we're defining a file resource. This resource type is used for managing files and directories. In this case, it's a very simple rule that ensures that `/etc/sysctl.d` exists and is a directory. Let's talk a little bit about syntax. In both our last example and this one we could see that when declaring a resource in puppet, we write them in a block that starts with the **resource type**, in this case `File`. 

The configuration of the resource is then written inside a block of curly braces. Right after the opening curly brace, we have the **title of the resource**, followed by a colon. After the colon come the attributes that we want to set for the resource. In this example, we're once again setting the `ensure` attribute with directory as the value, but we could set other attributes too >> 

Let's check out a different file resource. 

```json
class timezone {
    file { '/etc/timezone':
         ensure => file,
         content => "UTC\n",
         replace => true,
         }
}
```

In this example, we're using a file resource to configure the contents of `/etc/timezone`, a file, that's used in some Linux distributions to determine the time zone of the computer. This resource has three attributes. First, we explicitly say that this will be a file instead of a directory or a symlink, then we set the contents of the file to the `UTC` time zone. Finally, we set the **replace** attribute to `true`, which means that the contents of the file will be replaced even if the file already exists. We've now seen a couple examples of what we can do with the file resource. There are a lot more attributes that we could set, like file permissions the file owner, or the file modification time.

We've included a link to the official documentation in the next reading where you can find all the possible attributes that can be set for each resource. How do these rules turn into changes in our computers? When we declare a resource in our puppet rules. We're defining the desired state of that resource in the system. The puppet agent then turns the desired state into reality using providers.

The provider used will depend on the resource defined and the environment where the agent is running. Puppet will normally detect this automatically without us having to do anything special. When the puppet agent processes a resource, it first **decides** which provider it needs to use, then **passes along the attributes** that we configured in the resource to that provider. The code of each provider is in charge of making our computer **reflect the state requested** in the resource. In these examples, We've looked at one resource at a time. Up next, we'll see how we can combine a bunch of resources into more complex puppet classes.

I'll supply the felt and scissors.

## Puppet Classes

In the examples of Puppet code that we've seen so far, we've declared classes that contain one resource. You might have wondered what those classes were for. We **use these classes to collect the resources** that are needed to achieve a goal in a single place. For example, you could have a class that installs a package, sets the contents of a configuration file, and starts the service provided by that package. 

Let's check out an example like that. 

```json
class ntp {
    package { 'ntp':
            ensure => latest,
            }
	file { '/etc/ntp.conf':
         source => 'puppet:///modules/ntp/ntp.conf'
         replace => true,
         }
	service { 'ntp':
            enable => true,
            ensure => running
            }
}
```

In this case, we have a class with three resources, a **package**, a **file**, and a **service**. All of them are related to the Network Time Protocol, or NTP, the mechanism our computers use to synchronize the clocks. Our rules are making sure that the NTP package is always upgraded to the latest version. We're setting the contents of the configuration file using the source attribute, which means that the agent will read the required contents from the specified location. And we're saying that we want the NTP service to be **enabled** and **running**. By grouping all of the resources related to NTP in the same class, we only need a quick glance to understand how the service is configured and how it's supposed to work. This would make it easier to make changes in the future since we have all the related resources together. It makes sense to use this technique whenever we want to group related resources. For example, you could have a class grouping all resources related to managing log files, or configuring the time zone, or handling temporary files and directories. You could also have classes that group all the settings related to your web serving software, your email infrastructure, or even your company's firewall. We're just getting started with Puppet's basic resources and seeing how they can be applied. In further videos, we'll be learning a lot more about common practices when using configuration management tools. But before jumping into that, we've put together a reading with more information about Puppet syntax, resources and links to the official reference. Then we've got a quick quiz to check that everything is making sense.

By **grouping all of the resources** related to NTP in the same class, we only need a quick glance to understand how the service is configured and how it's supposed to work. This would make it easier to make changes in the future since we have all the related resources together. It makes sense to use this technique whenever we want to group related resources. 

For example, you could have a class grouping all resources related to managing **log files**, or configuring the **time zone**, or handling **temporary files and directories**. You could also have classes that group all the settings related to your **web serving software**, your **email infrastructure**, or even your **company's firewall**. We're just getting started with Puppet's basic resources and seeing how they can be applied. In further videos, we'll be learning a lot more about common practices when using configuration management tools. But before jumping into that, we've put together a reading with more information about Puppet syntax, resources and links to the official reference. Then we've got a quick quiz to check that everything is making sense.

# Puppet Resources

Resources are the fundamental unit for modeling system configurations. Each resource describes the desired state for some aspect of a system, like a specific service or package. When Puppet applies a catalog to the target system, it manages every resource in the catalog, ensuring the actual state matches the desired state.

Resources contained in classes and defined types share the relationships of those classes and defined types. Resources are not subject to scope: a resource in any area of code can be referenced from any other area of code.

A resource declaration adds a resource to the catalog and tells Puppet to manage that resource's state.

When Puppet applies the compiled catalog, it:

1. Reads the actual state of the resource on the target system.
2. Compares the actual state to the desired state.
3. If necessary, changes the system to enforce the desired state.
4. Logs any changes made to the resource. These changes appear in Puppet agent's log and in the run report, which is sent to the primary server and forwarded to any specified report processors.

If the catalog doesn't contain a particular resource, Puppet does nothing with whatever that resource described. If you remove a package resource from your manifests, Puppet doesn't uninstall the package; instead, it just ignores it. To remove a package, manage it as a resource and set `ensure => absent`.

You can delay adding resources to the catalog. For example, classes and defined types can contain groups of resources. These resources are managed only if you add that class or defined resource to the catalog. Virtual resources are added to the catalog only after they are realized.

## Resource declarations

At minimum, every resource declaration has a resource type, a title, and a set of attributes:

```json
<TYPE> { '<TITLE>': <ATTRIBUTE> => <VALUE>, }
```

The resource title and attributes are called the resource body. A resource declaration can have one resource body or multiple resource bodies of the same resource type.

Resource declarations are expressions in the Puppet language — they always have a side effect of adding a resource to the catalog, but they also resolve to a value. The value of a resource declaration is an array of resource references, with one reference for each resource the expression describes.

A resource declaration has extremely low precedence; in fact, it's even lower than the variable assignment operator (`=`). This means that if you use a resource declaration for its value, you must surround it with parentheses to associate it with the expression that uses the value.

If a resource declaration includes more than one resource body, it declares multiple resources of that resource type. The resource body is a title and a set of attributes; each body must be separated from the next one with a semicolon. Each resource in a declaration is almost completely independent of the others, and they can have completely different values for their attributes. The only connections between resources that share an expression are:

- They all have the same resource type.
- They can all draw from the same pool of default values, if a resource body with the title `default` is present.

## Resource uniqueness

Each resource must be unique; Puppet does not allow you to declare the same resource twice. This is to prevent multiple conflicting values from being declared for the same attribute. Puppet uses the resource `title` and the `name` attribute or namevar to identify duplicate resources — if either the title or the name is duplicated within a given resource type, catalog compilation fails. See the page about [resource syntax](https://puppet.com/docs/puppet/7.3/lang_resources.html#lang_resource_syntax) for details about resource titles and namevars. To provide the same resource for multiple classes, use a class or a virtual resource to add it to the catalog in multiple places without duplicating it. See [classes](https://puppet.com/docs/puppet/7.3/lang_classes.html#lang_classes) and [virtual resources](https://puppet.com/docs/puppet/7.3/lang_virtual.html) for more information.

## Relationships and ordering

By default, Puppet applies unrelated resources in the order in which they're written in the manifest. If a resource must be applied before or after some other resource, declare a relationship between them to show that their order isn't coincidental. You can also make changes in one resource cause a refresh of some other resource. See the [Relationships and ordering](https://puppet.com/docs/puppet/7.3/lang_relationships.html#lang_relationships) page for more information.

Otherwise, you can customize the default order in which Puppet applies resources with the ordering setting. See the [configuration page](https://puppet.com/docs/puppet/7.3/configuration.html) for details about this setting.

## Resource types

Every resource is associated with a resource type, which determines the kind of configuration it manages. Puppet has built-in resource types such as `file`, `service`, and `package`. See the [resource type reference](https://puppet.com/docs/puppet/7.3/type.html) for a complete list and information about the built-in resource types.

You can also add new resource types to Puppet:

- Defined types are lightweight resource types written in the Puppet language.
- Custom resource types are written in Ruby and have the same capabilities as Puppet's built-in types.

## Title

A resource's title is a string that uniquely identifies the resource to Puppet. In a resource declaration, the title is the identifier after the first curly brace and before the colon. For example, in this file resource declaration, the title is `/etc/passwd`:

```json
file  { '/etc/passwd':
  owner => 'root',
  group => 'root',
}
```

Titles must be unique per resource type. You can have both a package and a service titled "ntp," but you can only have one service titled "ntp." Duplicate titles cause compilation to fail.

The title of a resource differs from the namevar of the resource. Whereas the title identifies the resource to Puppet itself, the namevar identifies the resource to the target system and is usually specified by the resource's `name` attribute. The resource title doesn't have to match the namevar, but you'll often want it to: the value of the namevar attribute defaults to the title, so using the name in the title can save you some typing.

If a resource type has multiple namevars, the type specifies whether and how the title maps to those namevars. For example, the `package` type uses the `provider` attribute to help determine uniqueness, but that attribute has no special relationship with the title. See each type's documentation for details about how it maps title to namevars.

## Attributes

Attributes describe the desired state of the resource; each attribute handles some aspect of the resource. For example, the `file` type has a `mode` attribute that specifies the permissions for the file.

Each resource type has its own set of available attributes; see the [resource type reference](https://puppet.com/docs/puppet/7.3/types.html) for a complete list. Most resource types have a handful of crucial attributes and a larger number of optional ones. Attributes accept certain data types, such as strings, numbers, hashes, or arrays. Each attribute that you declare must have a value. Most attributes are optional, which means they have a default value, so you do not have to assign a value. If an attribute has no default, it is considered required, and you must assign it a value.

Most resource types contain an `ensure` attribute. This attribute generally manages the most basic state of the resource on the target system, such as whether a file exists, whether a service is running or stopped, or whether a package is installed or uninstalled. The values accepted for the `ensure` attribute vary by resource type. Most accept `present` and `absent`, but there are variations. Check the reference for each resource type you are working with.

**Tip:** Resource and type attributes are sometimes referred to as parameters. Puppet also has properties, which are slightly different from parameters: properties correspond to something measurable on the target system, whereas parameters change how Puppet manages a resource. A property always represents a concrete state on the target system. When talking about resource declarations in Puppet, parameter is a synonym for attribute.

## Namevars and `name` 

Every resource on a target system must have a unique identity; you cannot have two services, for example, with the same name. This identifying attribute in Puppet is known as the namevar.

Each resource type has an attribute that is designated to serve as the namevar. For most resource types, this is the `name` attribute, but some types use other attributes, such as the `file` type, which uses `path`, the file's location on disk, for its namevar. If a type's namevar is an attribute other than `name`, this is listed in the type reference documentation.

Most types have only one namevar. With a single namevar, the value must be unique per resource type. There are a few rare exceptions to this rule, such as the `exec` type, where the namevar is a command. However, some resource types, such as `package`, have multiple namevar attributes that create a composite namevar. For example, both the `yum` provider and the `gem` provider have `mysql` packages, so both the `name` and the `provider` attributes are namevars, and Puppet uses both to identify the resource.

The namevar differs from the resource's title, which identifies a resource to Puppet's compiler rather than to the target system. In practice, however, a resource's namevar and the title are often the same, because the namevar usually defaults to the title. If you don't specify a value for a resource's namevar when you declare the resource, Puppet uses the resource's title.

You might want to specify different a namevar that is different from the title when you want a consistently titled resource to manage something that has different names on different platforms. For example, the NTP service might be `ntpd` on Red Hat systems, but `ntp` on Debian and Ubuntu. You might title the service "ntp," but set its namevar --- the `name` attribute --- according to the operating system. Other resources can then form relationships to the resource without the title changing.

## Metaparameters

Some attributes in Puppet can be used with every resource type. These are called metaparameters. These don't map directly to system state. Instead, metaparameters affect Puppet's behavior, usually specifying the way in which resources relate to each other.

The most commonly used metaparameters are for specifying order relationships between resources. See the documentation on [relationships and ordering](https://puppet.com/docs/puppet/7.3/lang_relationships.html#lang_relationships) for details about those metaparameters. See the full list of available metaparameters in the [metaparameter reference](https://puppet.com/docs/puppet/7.3/metaparameter.html).

## Resource syntax

You can accomplish a lot with just a few resource declaration features, or you can create more complex declarations that do more.

### Basic syntax

The simplified form of a resource declaration includes:

- The resource type, which is a word with no quotes.
- An opening curly brace `{`.
- The title, which is a string.
- A colon (`:`).
- Optionally, any number of attribute and value pairs, each of which consists of:
  - An attribute name, which is a lowercase word with no quotes.
  - A `=>` (called an arrow, "fat comma," or "hash rocket").
  - A value, which can have any [data type][datatype].
  - A trailing comma.
- A closing curly brace (`}`).

You can use any amount of whitespace in the Puppet language.

This example declares a file resource with the title `/etc/passwd`. This declaration's `ensure` attribute ensures that the specified file is created, if it does not already exist on the node. The rest of the declaration sets values for the file's `owner`, `group`, and `mode` attributes.

```json
file { '/etc/passwd':
  ensure => file,
  owner  => 'root',
  group  => 'root',
  mode   => '0600',
}
```

### Complete syntax

By creating more complex resource declarations, you can:

- Describe many resources at once.
- Set a group of attributes from a hash with the `*` attribute.
- Set default attributes.
- Specify an abstract resource type.
- Amend or override attributes after a resource is already declared.

The complete generalized form of a resource declaration expression is:

- The resource type, which can be one of:
  - A lowercase word with no quotes, such as `file`.
  - A resource type data type, such as `File`, `Resource[File]`, or `Resource['file']`. It must have a type but not a title.
- An opening curly brace (`{`).
- One or more resource bodies, separated with semicolons (`;`). Each resource body consists of:
  - A title, which can be one of:
    - A string.
    - An array of strings, which declares multiple resources.
    - The special value `default`, which sets default attribute values for other resource bodies in the same expression.
  - A colon (`:`).
  - Optionally, any number of attribute and value pairs, separated with commas (`,`). Each attribute/value pair consists of:
    - An attribute name, which can be one of:
      - A lowercase word with no quotes.
      - The special attribute `*`, called a "splat," which takes a hash and sets other attributes.
      - A `=>`, called an arrow, a "fat comma," or a "hash rocket".
      - A value, which can have any data type.
    - Optionally, a trailing comma after the last attribute/value pair.
- Optionally, a trailing semicolon after the last resource body.
- A closing curly brace (`}`)

```json
<TYPE> { default: * => <HASH OF ATTRIBUTE/VALUE PAIRS>, <ATTRIBUTE> => <VALUE>, ; '<TITLE>': * => <HASH OF ATTRIBUTE/VALUE PAIRS>, <ATTRIBUTE> => <VALUE>, ; '<NEXT TITLE>': ... ; ['<TITLE'>, '<TITLE>', '<TITLE>']: ... ; 
```

### Resource declaration default attributes

If a resource declaration includes a resource body with a title of `default`, Puppet doesn't create a new resource named "default." Instead, every other resource in that declaration uses attribute values from the `default` body if it doesn't have an explicit value for one of those attributes. This is also known as "per-expression defaults."

Resource declaration defaults are useful because it lets you set many attributes at once, but you can still override some of them.

This example declares several different files, all using the default values set in the `default` resource body. However, the `mode` value for the the files in the last array (`['ssh_config', 'ssh_host_dsa_key.pub'....`) is set explicitly instead of using the default.

```json
file {
  default:
    ensure => file,
    owner  => "root",
    group  => "wheel",
    mode   => "0600",
  ;
  ['ssh_host_dsa_key', 'ssh_host_key', 'ssh_host_rsa_key']:
    # use all defaults
  ;
  ['ssh_config', 'ssh_host_dsa_key.pub', 'ssh_host_key.pub', 'ssh_host_rsa_key.pub', 'sshd_config']:
    # override mode
    mode => "0644",
  ;
}
```

The position of the `default` body in a resource declaration doesn't matter; resources above and below it all use the default attributes if applicable.You can only have one `default` resource body per resource declaration.

### Setting attributes from a hash

You can set attributes for a resource by using the splat attribute, which uses the splat or asterisk character `*`, in the resource body.

The value of the splat (`*`) attribute must be a hash where:

- Each key is the name of a valid attribute for that resource type, as a string.
- Each value is a valid value for the attribute it's assigned to.

This sets values for that resource's attributes, using every attribute and value listed in the hash.

For example, the splat attribute in this declaration sets the `owner`, `group`, and `mode` settings for the file resource.

```json
$file_ownership = {
  "owner" => "root",
  "group" => "wheel",
  "mode"  => "0644",
}

file { "/etc/passwd":
  ensure => file,
  *      => $file_ownership,
}
```

You cannot set any attribute more than once for a given resource; if you try, Puppet raises a compilation error. This means that:

- If you use a hash to set attributes for a resource, you cannot set a different, explicit value for any of those attributes. For example, if `mode` is present in the hash, you can't also set `mode => "0644"` in that resource body.
- You can't use the `*` attribute multiple times in one resource body, since the splat itself is an attribute.

To use some attributes from a hash and override others, either use a hash to set per-expression defaults, as described in the section on resource declaration defaults, or use the merging operator, `+` to combine attributes from two hashes, with the right-hand hash overriding the left-hand one.

### Abstract resource types

Because a resource declaration can accept a resource type data type as its resource type , you can use a `Resource[<TYPE>]` value to specify a non-literal resource type, where the `<TYPE>` portion can be read from a variable.That is, the following three examples are equivalent to each other:

```json
file { "/tmp/foo": ensure => file, } File { "/tmp/foo": ensure => file, } Resource[File] { "/tmp/foo": ensure => file, }
$mytype = File
Resource[$mytype] { "/tmp/foo": ensure => file, }
$mytypename = "file"
Resource[$mytypename] { "/tmp/foo": ensure => file, }
```

This lets you declare resources without knowing in advance what type of resources they'll be, which can enable transformations of data into resources.

### Arrays of titles

If you specify an array of strings as the title of a resource body, Puppet creates multiple resources with the same set of attributes. This is useful when you have many resources that are nearly identical.

For example:

```json
$rc_dirs = [
  '/etc/rc.d',       '/etc/rc.d/init.d','/etc/rc.d/rc0.d',
  '/etc/rc.d/rc1.d', '/etc/rc.d/rc2.d', '/etc/rc.d/rc3.d',
  '/etc/rc.d/rc4.d', '/etc/rc.d/rc5.d', '/etc/rc.d/rc6.d',
]

file { $rc_dirs:
  ensure => directory,
  owner  => 'root',
  group  => 'root',
  mode   => '0755',
}
```

If you do this, you must let the namevar attributes of these resources default to their titles. You can't specify an explicit value for the namevar, because it applies to all of the resources.

### Adding or modifying attributes

Although you cannot declare the same resource twice, you can add attributes to an resource that has already been declared. In certain circumstances, you can also override attributes. You can amend attributes with either a resource reference, a collector, or from a hash using the splat (`*`) attribute.

To amend attributes with the splat attribute, see the section about setting attributes from a hash.

To amend attributes with a resource reference, add a resource reference attribute block to the resource that's already declared. Normally, you can only use resource reference blocks to add previously unmanaged attributes to a resource; it cannot override already-specified attributes. The general form of a resource reference attribute block is:

- A resource reference to the resource in question
- An opening curly brace
- Any number of attribute `=>` value pairs
- A closing curly brace

For example, this resource reference attribute block amends values for the `owner`, `group`, and `mode` attributes:

```json
file {'/etc/passwd':
  ensure => file,
}

File['/etc/passwd'] {
  owner => 'root',
  group => 'root',
  mode  => '0640',
}
```

You can also amend attributes with a collector.

The general form of a collector attribute block is:

- A [resource collector](https://puppet.com/docs/puppet/7.3/lang_collectors.html) that matches any number of resources
- An opening curly brace
- Any number of attribute => value (or attribute +> value) pairs
- A closing curly brace

For resource attributes that accept multiple values in an array, such as the relationship metaparameters, you can add to the existing values instead of replacing them by using the "plusignment" (`+>`) keyword instead of the usual hash rocket (`=>`). For details, see appending to attributes in the [classes](https://puppet.com/docs/puppet/7.3/lang_classes.html) documentation.

This example amends the `owner`, `group`, and `mode` attributes of any resources that match the collector:

```js
class base::linux { 
  file {'/etc/passwd':
    ensure => file,
  } 
  ...}

include base::linux

File <| tag == 'base::linux' |> {
 owner => 'root',
 group => 'root',
 mode => '0640',
}
```

**CAUTION:** Be very careful when amending attributes with a collector. Test with `--noop` to see what changes your code would make.

- It can override other attributes you've already specified, regardless of class inheritance.
- It can affect large numbers of resources at one time.
- It implicitly realizes any virtual resources the collector matches.
- Because it ignores class inheritance, it can override the same attribute more than one time, which results in an evaluation order race where the last override wins.

### Local resource defaults

Because resource default statements are subject to dynamic scope, you can't always tell what areas of code will be affected. Generally, do not include classic resource default statements anywhere other than in your site manifest (`site.pp`). See the [resource defaults documentation](https://puppet.com/docs/puppet/7.3/lang_defaults.html) for details. Whenever possible, use resource declaration defaults, also known as per-expression defaults.

However, resource default statements can be powerful, allowing you to set important defaults, such as file permissions, across resources. Setting local resource defaults is a way to protect your classes and defined types from accidentally inheriting defaults from classic resource default statements.

To set local resource defaults, define your defaults in a variable and re-use them in multiple places, by combining resource declaration defaults and setting attributes from a hash.

This example defines defaults in a `$file_defaults` variable, and then includes the variable in a resource declaration default with a hash.

```json
class mymodule::params {
  $file_defaults = {
    mode  => "0644",
    owner => "root",
    group => "root",
  }
  # ...
}

class mymodule inherits mymodule::params {
  file { default: *=> $mymodule::params::file_defaults;
    "/etc/myconfig":
      ensure => file,
    ;
  }
}
```

# The Building Blocks of Configuration Management

## What are domain-specific languages?

Up until now, we've seen examples of very simple Puppet rules they just define one or more resources. These resources are the building blocks of Puppet rules, but we can do much more complex operations using **Puppet's domain specific language or DSL**. Typical programming languages like Python, Ruby, Java or Go are **general purpose languages** that can be used to write lots of different applications with different goals and use cases. On the flip side, a domain specific language is a programming language that's more limited in scope. 

Learning a domain-specific language is usually much faster and easier than learning a general purpose programming language because there's a lot less to cover. You don't need to learn as much syntax or understand as many keywords or taking to account a lot of overhead in general. In the case of Puppet, the DSL is limited to operations related to when and how to apply configuration management rules to our devices. For example, we can use the mechanisms provided by the DSL to set different values on laptops or desktop computers, or to install some specific packages only on the company's web servers. On top of the basic resource types that we already checked out, Puppet's DSL includes **variables**, **conditional statements**, and **functions**. Using them, we can apply different resources or set attributes to different values depending on some conditions. 

Before we jump into an example of what that looks like, let's talk a bit about Puppet **facts**. 

**Facts** are variables that **represent the characteristics of the system**. When the Puppet agent runs, it calls a program called `factor` which analyzes the current system, storing the information it gathers in these facts. Once it's done, it sends the values for these facts to the server, which uses them to calculate the **rules** that should be applied. 

Puppet comes with a bunch of baked-in **core facts** that store useful information about the system like what the current OS is, how much memory the computer has whether it's a virtual machine or not or what the current IP address is. If the information we need to make a decision isn't available through one of these facts, we can also write a script that checks for the information and turns it into our own custom fact. 

Let's check out an example of a piece of Puppet code that makes use of one of the built-in facts. 

```json
if $facts['is_virtual'] {
    package { 'smartmontools':
		ensure => purged,
	}
} else {
    package { 'smartmontools':
		ensure => installed,
	}
}
```

This piece of code is using the `is_virtual` fact together with a conditional statement to decide whether the `smartmontools` package should be `installed` or `purged`. This package is used for monitoring the state of hard drives using SMART. So it's useful to have it installed in physical machines, but it doesn't make much sense to install it in our virtual machines. 

We can see several of the characteristics of Puppets domain specific language in this block. So let's spend a little time looking at all of the elements of syntax here. First, **facts is a variable**. All variable names are preceded by a dollar sign in Puppet's DSL. In particular, the facts variable is what's known as a **hash** in the Puppet DSL, which is **equivalent to a dictionary in Python**. This means that we can access the different elements in the hash using their keys. In this case, we're accessing the value associated to the `is_virtual` key. 

Second, we see how we can write a conditional statement using if-else, enclosing each block of the conditional with curly braces. Finally, each conditional block contains a **package** resource. We've seen resources before, but we haven't looked at the syntax in detail. So let's do that now. 

Every resource starts with the type of resource being defined. In this case, **package** and the contents of the resource are then enclosed in curly braces. Inside the resource definition, the first line contains the **title** followed by a **colon**. Any lines after that are attributes that are being set. We use **equals greater than** to assign values to the attributes and then each attribute ends with a comma. We've now covered a large chunk of puppet's DSL syntax. If you look back to what it was like to learn your first programming language, you'll probably notice how much less syntax there is to learn here. That's typical of the domain specific languages used by configuration management tools. While each tool uses their own DSL, they're usually very simple and can be learned very quickly. Up next, we'll talk about a few other principles behind most configuration management tools. Whenever you're ready, let's dive in.

## The Driving Principles of Configuration Management

Up to now, we've seen a few examples of what Puppet rules look like, including a bunch of different resources and even a conditional expression. You might have noticed that in all the examples we've checked out, we were never telling the computer the steps it should follow in order to do what we wanted. 

Instead, we were just **declaring the end goal** that we wanted to achieve, like going to a drive-through and ordering a burger, we didn't make it, but there it is. The providers that we mentioned earlier lake **apt** and **yum** are the ones in charge of turning our goals into whatever actions are necessary. We say that Puppet uses a declarative language because we declare the state that we want to achieve rather than the steps to get there. 

Traditional languages like Python or C are called **procedural** because we write out the procedure that the computer needs to follow to reach our desired goal. Coming from a procedural language like Python, it might take some time to get used to writing declarative code like the ones used for Puppet, and that's okay. Just remember that when it comes to configuration management, it makes sense to simply **state what the configuration should be**, **not what the computer should do to get there**. 

Say you're using a resource to declare that you want a package installed, you don't care what commands a computer has to run you install it, you only care that after the configuration management tool has run, the package is installed. Another important aspect of configuration management is that operations should be **idempotent**. 

In this context, an **idempotent action can be performed over and over again without changing the system after the first time the action was performed**, and with no unintended side effects. 

Let's check this out with an example of a file resource. 

```json
file { '/etc/issue': 
     mode => '0644',
     content => "Internal system \l \n", 
     }
```

This resource ensures that the `/etc/issue` file has a **set of permissions** and a **specific line** in it. Fulfilling this requirement is an idempotent operation. If the file already exists and has the desired content, then Puppet will understand that no action has to be taken. 

If the file doesn't exist, then puppet will create it. 

If the contents or permissions don't match, Puppet will fix them. 

No matter how many times the agent applies the rule, the end result is that this file will have the requested contents and permissions. **Idempotency is a valuable property of any piece of automation**. If a script is idempotent, it means that it can fail halfway through its task and be run again without problematic consequences. Say you're running your configuration management system to setup a new server. Unfortunately, the setup fails because you forgot to add a second disk to the computer and the configuration required two disks. If your automation is idempotent, you can add the missing disk and then have the system pick up from where it left off. 

Most Puppet resources provide idempotent actions, and we can rest assured that two runs of the same set of rules will lead to the same end result. **An exception to this is the exec resource**, which runs commands for us. The actions taken by the exec resource might not be idempotent since a command might modify the system each time it's executed. To understand this, let's check out what happens when we execute a command that moves a file on our computer. First, we'll check that the `example.txt` file is here, and then we'll move it to the desktop directory.

This works fine now, but what happens if we run the exact same command again after it's been executed once? We receive an error because the file is no longer in the same place. In other words, this was not an idempotent action, as executing the same action twice produced a different result and the unintended side effect of an error. If we were running this inside Puppet, this would cause our Puppet run to finish with an error. 

So if we need to use the exec resource to run a command for us, we need to be careful to ensure that the action is idempotent. We could do that for example by using the **onlyif** attribute like this. 

```json
exec { 'move example file': 
     command => 'mv /home/user/example.txt /home/user/Desktop',
     onlyif => 'test -e /home/user/example.txt',
     }
```

Using the **onlyif attribute**, we specified that this command should be executed **only if the file that we want to move exists**. This means that the file will be moved if it exists and **nothing will happen if it doesn't**. By adding this conditional, we've taken an action that's not idempotent and turned it into an idempotent one. 

Another important aspect of how configuration management works is the **test and repair paradigm.** This means that **actions are taken only when they are necessary** to achieve a goal. Puppet will first test to see if the resource being managed like a file or a package, actually needs to be modified. If the file exists in the place we want it to, no action needs to be taken. If a package is already installed, there's no need to install it again. This avoids wasting time doing actions that aren't needed. 

Finally, another important characteristic is that Puppet is **stateless**, this means that there's n**o state being kept between runs of the agent.** Each Puppet run is independent of the previous one, and the next one. Each time the puppet agent runs, it collects the current facts. The Puppet master generates the rules based just on those facts, and then the agent applies them as necessary. We're just getting started with what configuration management is and what it looks like in Puppet. But hopefully, you're starting to see how understanding these basic concepts and how turning them into practical rules can help you manage a small army of computers. Up next, there's a reading with links to more information about the concepts we've covered followed by a quick quiz. You've got this.

## The Puppet design philosophy

Puppet can be somewhat alien to technologists who have a background in automation scripting. Where most of our scripts are procedural, Puppet is *declarative*. While a declarative language has many major advantages for configuration management, it does impose some interesting restrictions on the approaches we use to solve common problems.

Although Puppet’s design philosophy may not be the most exciting topic to begin this book, it drives many of the practices in the coming chapters. Understanding that philosophy will help contextualize many of the recommendations covered.

## Declarative code

The Puppet Domain Specific Language (DSL) is a declarative language, as opposed to the imperative or procedural languages that system administrators tend to be most comfortable and familiar with.

![tip_animal](http://s.radar.oreilly.com/wp-files/2/2015/04/tip_animal.jpg)In an imperative language, we describe how to accomplish a task. In a declarative language, we describe what we want to accomplish. Imperative languages focus on actions to reach a result, and declarative languages focus on the result we wish to achieve. We will see examples of the difference below.

Puppet’s language is (mostly) verbless. Understanding and internalizing this paradigm is critical when working with Puppet; attempting to force Puppet to use a procedural or imperative process can quickly become an exercise in frustration and will tend to produce fragile code.

In theory, a declarative language is ideal for configuration baselining tasks. With the Puppet DSL, we describe the desired state of our systems, and Puppet handles all responsibility for making sure the system conforms to this desired state. Unfortunately, most of us are used to a procedural approach to system administration. The vast majority of the bad Puppet code I’ve seen has been the result of trying to write procedural code in Puppet, rather than adapting existing procedures to Puppet’s declarative model.

### Procedural code with Puppet

In some cases, writing procedural code in Puppet is unavoidable. However, such code is rarely elegant, often creates unexpected bugs, and can be difficult to maintain. We will see practical examples and best practices for writing procedural code when we look at the exec resource type in Chapter 5.

Of course, it’s easy to simply say “be declarative.” In the real world, we are often tasked to deploy software that isn’t designed for a declarative installation process. A large part of this book will attempt to address how to handle many uncommon tasks in a declarative way. As a general rule, if your infrastructure is based around packaged open source software, writing declarative Puppet code will be relatively straight-forward. Puppet’s built in types and providers will provide a declarative way to handle most of your operational tasks. If you’re infrastructure includes Windows clients and a lot of enterprise software, writing declarative Puppet code may be significantly more challenging.

Another major challenge system administrators face when working within the constraints of a declarative model is that we tend to operate using an imperative workflow. How often have you manipulated files using regular expression substitution? How often do we massage data using a series of temp files and piped commands? While Puppet offers many ways to accomplish the same tasks, most of our procedural approaches do not map well into Puppet’s declarative language. We will explore some examples of this common problem and discuss alternative approaches to solving it.

## What is declarative code anyway?

As mentioned earlier, declarative code tends not to have verbs. We don’t create users and we don’t remove them; we ensure that the users are present or absent. We don’t install or remove software; we ensure that software is present or absent. Where create and install are verbs, present and absent are adjectives. The difference seems trivial at first, but proves to be very important in practice.

A real world example:

Imagine that I’m giving you directions to the Palace of Fine Arts in San Francisco.

Procedural instructions:

- Head North on 19th Avenue
- Get on US-101S
- Take Marina Blvd. to Palace Dr.
- Park at the Palace of Fine Arts Theater

These instructions make a few major assumptions:

- You aren’t already at the Palace of Fine Arts
- You are driving a car
- You are currently in San Francisco
- You are currently on 19th avenue or know how to get there.
- You are heading North on 19th avenue.
- There are no road closures or other traffic disruptions that would force you to a different route.

Compare this to the declarative instructions:

- Be at 3301 Lyon Street, San Francisco, CA 94123 at 7:00PM

The declarative approach has a few major advantages in this case:

- It makes no assumptions about your mode of transportation. These instructions are still valid if your plans involve public transit or parachuting into the city.
- The directions are valid even if you’re currently at the Palace of Fine Arts
- These instructions empower you to route around road closures and traffic

The declarative approach allows you to chose the best way to reach the destination based on your current situation, and it relies on your ability to find your way to the destination given.

Declarative languages aren’t magic. Much like an address relies on your understanding how to read a map or use a GPS device, Puppet’s declarative model relies on its own procedural code to turn your declarative request into a set of instructions that can achieve the declared state. Puppet’s model uses a *Resource type* to model an object, and a *provider* implementing procedural code to produce the state the model describes.

The major limitation imposed by Puppet’s declarative model might be somewhat obvious. If a native resource type doesn’t exist for the resource you’re trying to model, you can’t manage that resource in a declarative way. Declaring that I want a red two-story house with 4 bedrooms might empower you to build the house out of straw or wood or brick, but it probably won’t actually accomplish anything if you don’t happen to be a general contractor.

There is some good news on this front, however. Puppet already includes native types and providers for most common objects, the Puppet community has supplied additional native models, and if you absolutely have to accomplish something procedurally you can almost always fall back to the `exec` resource type.

## A practical example

Let’s examine a practical example of procedural code for user management. We will discuss how to make the code can be made robust, its declarative equivalent in Puppet, and the benefits of using Puppet rather than a shell script for this task.

### Imperative / Procedural Code

Here’s an example of an imperative process using BASH. In this case, we are going to create a user with a home directory and an authorized SSH key on a CentOS 6 Host.

**Example 1-1. Imperative user creation with BASH**

```bash
groupadd examplegroupuseradd -g examplegroup alicemkdir ~alice/.ssh/chown alice.examplegroup ~alice/.sshecho "ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAIEAm3TAgMF/2RY+r7KIeUoNbQb1TP6ApOtgJPNV\0TY6teCjbxm7fjzBxDrHXBS1vr+fe6xa67G5ef4sRLl0kkTZisnIguXqXOaeQTJ4Idy4LZEVVbngkd\2R9rA0vQ7Qx/XrZ0hgGpBA99AkxEnMSuFrD/E5TunvRHIczaI9Hy0IMXc= \alice@localhost" > ~alice/.ssh/authorized_keys
```

What if we decide this user should also be a member of the wheel group?

**Example 1-2. Imperative user modification with BASH**

```bash
useradd -g examplegroup aliceusermod -G wheel alice
```

And if we want to remove that user and that user’s group?

**Example 1-3. Imperative user removal with BASH**

```bash
userdel alicegroupdel examplegroup
```

Notice a few things about this example:

- Each process is completely different
- The correct process to use depends on the current state of the user
- Each of these processes will produce errors if invoked more than one time

Imagine for a second that we have several systems. On some systems, example user is absent. On other systems, `alice` is present, but not a member of the wheel group. On some systems, `alice` is present and a member of the wheel group. Imagine that we need to write a script to ensure that `alice` exists, and is a member of the wheel group on every system, and has the correct authorized key. What would such a script look like?

**Example 1-4. Robust user management with BASH**

```bash

#!/bin/bash
if ! getent group examplegroup; then 
	groupadd examplegroup
fi
 
if ! getent passwd alice; then
	useradd -g examplegroup -G wheel alice
fi
 
if ! id -nG alice | grep -q 'examplegroup wheel'; then 
	usermod -g examplegroup -G wheel alice
fi
 
if ! test -d ~alice/.ssh; then 
	mkdir -p ~alice/.ssh
fi
 
chown alice.examplegroup ~alice/.ssh
 
if ! grep -q alice@localhost ~alice/.ssh/authorized_keys; then
	echo "ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAIEAm3TAgMF/2RY+r7KIeUoNbQb1TP6ApOtg\ JPNV0TY6teCjbxm7fjzBxDrHXBS1vr+fe6xa67G5ef4sRLl0kkTZisnIguXqXOaeQTJ4Idy4LZEVVb\
ngkd2R9rA0vQ7Qx/XrZ0hgGpBA99AkxEnMSuFrD/E5TunvRHIczaI9Hy0IMXc= \ alice@localhost" >> ~alice/.ssh/authorized_keys
fi
chmod 600 ~alice/.ssh/authorized_keys
```



Of course, this example only covers the use case of creating and managing a few basic properties about a user. If our policy changed, we would need to write a completely different script to manage this user. Even fairly simple changes, such as revoking this user’s wheel access could require somewhat significant changes to this script.

This approach has one other major disadvantage; it will only work on platforms that implement the same commands and arguments of our reference platform. This example will fail on FreeBSD (implements adduser, not useradd) Mac OSX, and Windows.

### Declarative code

Let’s look at our user management example using Puppet’s declarative DSL.

Creating a user and group:

**Example 1-5. Declarative user creation with Puppet**

```json
$ssh_key = "AAAAB3NzaC1yc2EAAAABIwAAAIEAm3TAgMF/2RY+r7KIeUoNbQb1TP6ApOtgJPNV0T\
Y6teCjbxm7fjzBxDrHXBS1vr+fe6xa67G5ef4sRLl0kkTZisnIguXqXOaeQTJ4Idy4LZEVVbngkd2R\
9rA0vQ7Qx/XrZ0hgGpBA99AkxEnMSuFrD/E5TunvRHIczaI9Hy0IMXc="
 
group { 'examplegroup': 
	ensure	=> 'present',
}
 
user { 'alice':
	ensure		=> 'present',
	gid			=> 'examplegroup', 
	managehome	=> true,
}
 
ssh_authorized_key { 'alice@localhost': 
	ensure	=> 'present',
	user	=>'alice',
	type	=>'ssh-rsa',
	key		=> $ssh_key,
}
```

Adding `alice` to the wheel group:

**Example 1-6. Declarative group membership with puppet**

```json
$ssh_key = "AAAAB3NzaC1yc2EAAAABIwAAAIEAm3TAgMF/2RY+r7KIeUoNbQb1TP6ApOtgJPNV0T\
Y6teCjbxm7fjzBxDrHXBS1vr+fe6xa67G5ef4sRLl0kkTZisnIguXqXOaeQTJ4Idy4LZEVVbngkd2R\
9rA0vQ7Qx/XrZ0hgGpBA99AkxEnMSuFrD/E5TunvRHIczaI9Hy0IMXc="
 
group { 'examplegroup': 
	ensure	=> 'present',
}
 
user { 'alice':
	ensure		=> 'present',
	gid			=> 'examplegroup', 
	groups		=> 'wheel', # (1)
	managehome	=> true,
}
 
ssh_authorized_key { 'alice@localhost': 
	ensure	=> 'present',
	user	=>'alice',
	type	=>'ssh-rsa',
	key   	=> $ssh_key,
}
```

(1) Note that the only change between this example and the previous example is the addition of the `groups` parameter for the `alice` resource.

Remove `alice`:

**Example 1-7. Ensure that a user is absent using Puppet**

```json
$ssh_key = "AAAAB3NzaC1yc2EAAAABIwAAAIEAm3TAgMF/2RY+r7KIeUoNbQb1TP6ApOtgJPNV0T\
Y6teCjbxm7fjzBxDrHXBS1vr+fe6xa67G5ef4sRLl0kkTZisnIguXqXOaeQTJ4Idy4LZEVVbngkd2R\
9rA0vQ7Qx/XrZ0hgGpBA99AkxEnMSuFrD/E5TunvRHIczaI9Hy0IMXc="
 
group { 'examplegroup':
	ensure => 'absent', # (1)
}
 
user { 'alice':
	ensure		=> 'absent', # (2)
	gid			=> 'examplegroup', 
	groups		=> 'wheel', 
	managehome	=> true,
}
 
ssh_authorized_key { 'alice@localhost': 
	ensure	=> 'absent', # (3)
	user	=>'alice',
	type	=>'ssh-rsa',
	key		=> $ssh_key,
}
 
Ssh_authorized_key['alice@localhost'] -> # (4)
User['alice'] -> # (5)
Group['examplegroup']
```

(1), (2), (3) Ensure values are changed from Present to Absent.

(4), (5) Resource ordering is added to ensure groups are removed after users. Normally, the correct order is implied due to the Autorequire feature discussed in Chapter 5.

![tip_animal](http://s.radar.oreilly.com/wp-files/2/2015/04/tip_animal.jpg)
You may notice the addition of resource ordering in this example when it wasn’t required in previous examples. This is a byproduct of Puppet’s Autorequire feature. [PUP-2451](https://tickets.puppetlabs.com/browse/PUP-2451) explains the issue in greater depth.

![tip_animal](http://s.radar.oreilly.com/wp-files/2/2015/04/tip_animal.jpg)
In practice, rather than managing `alice` as 3 individual resources, we would abstract this into a defined type that has its own ensure parameter, and conditional logic to enforce the correct resource dependency ordering.

In this example, we are able to remove the user by changing the ensure state from present to absent on the user’s resources. Although we could remove other parameters such as gid, groups, and the users key, in most cases it’s better to simply leave the values in place, just in case we ever decide to restore this user.

![tip_animal](http://s.radar.oreilly.com/wp-files/2/2015/04/tip_animal.jpg)
It’s usually best to disable accounts rather than remove them. This helps preserve file ownership information and helps avoid UID reuse.

In our procedural examples, we saw a script that would bring several divergent systems into conformity. For each step of that example script, we had to analyze the current state of the system, and perform an action based on state. With a declarative model, all of that work is abstracted away. If we wanted to have a user who was a member of 2 groups, we would simply declare that user as such, as in Example 1-6.

### Non-Declarative code with Puppet

It is possible to write non-declarative code with Puppet. Please don’t do this:

```json
$app_source  = 'http://www.example.com/application.tar.gz'
$app_target  = '/tmp/application.tar.gz'
 
exec { 'download application':
  command => "/usr/bin/wget -q ${app_source} -O ${app_target}",
  creates => '/usr/local/application/',
  notify => exec['extract application'],
}
 
exec { 'extract application':
  command     => "/bin/tar -zxf ${app_target} -C /usr/local",
  refreshonly => true,
  creates     => '/usr/local/application/',
}
```

This specific example has a few major problems:

1. Exec resources have a set timeout. This example may work well over a relatively fast corporate Internet connection, and then fail completely from a home DSL line. The solution would be to set the timeout parameter of the exec resources to a reasonably high value.
2. This example does not validate the checksum of the downloaded file, which could produce some odd results upon extraction. An additional exec resource might be used to test and correct for this case automatically.
3. In some cases, a partial or corrupted download may wedge this process. We attempt to work around this problem by overwriting the archive each time it’s downloaded.
4. This example makes several assumptions about the contents of application.tar.gz. If any of those assumptions are wrong, these commands will repeat every time Puppet is invoked.
5. This example is not particularly portable, and would require a platform specific implementation for each supported OS.
6. This example would not be particularly useful for upgrading the application.

This is a relatively clean example of non-declarative Puppet code, and tends to be seen when working with software that is not available in a native packaging format. Had this application been distributed as an RPM, dpkg, or MSI, we could have simply used a package resource for improved portability, flexibility, and reporting. While this example is not best practices, there are situations where is unavoidable, often for business or support reasons.

![tip_animal](http://s.radar.oreilly.com/wp-files/2/2015/04/tip_animal.jpg)
This example could be made declarative using the [nanliu/staging](https://forge.puppetlabs.com/nanliu/staging) module.

Another common pattern is the use of conditional logic and custom facts to test for the presence of software. Please don’t do this unless it’s absolutely unavoidable:

```json
Facter.add(:example_app_version) do 
	confine :kernel => 'Linux' 
	setcode do
		Facter::Core::Execution.exec('/usr/local/app/example_app --version') 
	end
end
 
    $app_source       = 'http://www.example.com/app-1.2.3.tar.gz'
    $app_target       = '/tmp/app-1.2.3.tar.gz'
    
if $example_app_version != '1.2.3' { 
	exec { 'download application':
		command => "/usr/bin/wget -q ${app_source} -O ${app_target}",
		before  => exec['extract application'],
	}
	exec { 'extract application':
		command => "/bin/tar -zxf ${app_target} -C /usr/local",
	} 
}
```

This particular example has many of the same problems of the previous example, and introduces one new problem: it breaks Puppet’s reporting and auditing model. The conditional logic in this example causes the download and extraction resources not to appear in the catalog sent to the client following initial installation. We won’t be able to audit our run reports to see whether or not the download and extraction commands are in a consistent state. Of course, we could check the `example_application_version` fact if it happens to be available, but this approach becomes increasingly useless as more resources are embedded in conditional logic.

This approach is also sensitive to factor and plugin sync related issues, and would definitely produce some unwanted results with cached catalogs.

Using facts to exclude parts of the catalog does have one benefit: it can be used to obfuscate parts of the catalog so that sensitive resources do not exist in future Puppet runs. This can be handy if, for example, your wget command embeds a passphrase, and you wish to limit how often it appears in your catalogs and reports. Obviously, there are better solutions to that particular problem, but in some cases there is also benefit to security in depth.

### Idempotency

In computer science, an idempotent function is a function that will return the same value each time it’s called, whether it’s only called once, or called 100 times. For example: `X = 1` is an idempotent operation. `X = X + 1` is a non-idempotent,recursive operation.

Puppet as a language is designed to be inherently idempotent. As a system, Puppet designed to be used in an idempotent way. A large part of this idempotency owed to its declarative resource management model, however Puppet also enforces a number of rules on its variable handling, iterators, and conditional logic to maintain its idempotency.

Idempotence has major benefits for a configuration management language:

- The configuration is inherently self healing
- State does not need to be maintained between invocations
- Configurations can be safely re-applied

For example, if for some reason Puppet fails part way through a configuration run, re-invoking Puppet will complete the run and repair any configurations that were left in an inconsistent state by the previous run.

### Convergence vs Idempotence

Configuration management languages are often discussed in terms of their convergence model. Some tools are designed to be eventually convergent; others immediately convergent and/or idempotent.

With an eventually convergent system, the configuration management tool is invoked over and over; each time the tool is invoked, the system approaches a converged state, where all changes defined in the configuration language have been applied, and no more changes can take place. During the process of convergence, the system is said to be in a partially converged, or inconsistent state.

For Puppet to be idempotent, it cannot by definition also be eventually convergent. It must reach a convergent state in a single run, and remain in the same state for any subsequent invocations. Puppet can still be described as an immediately convergent system, since it is designed to reach a convergent state after a single invocation.

Convergence of course also implies the existence of a diverged state. Divergence is the act of moving the system away from the desired *converged* state. This typically happens when someone attempts to manually alter a resource that is under configuration management control.

There are many practices that can break Puppet’s idempotence model. In most cases, breaking Puppet’s idempotence model would be considered a bug, and would be against best practices. There are however some cases where a level of eventual convergence is unavoidable. One such example is handling the numerous post-installation software reboots that are common when managing Windows nodes.

### Side effects

In computer science, a side effect is a change of system or program state that is outside the defined scope of the original operation. Declarative and idempotent languages usually attempt to manage, reduce, and eliminate side effects. With that said, it is entirely possible for an idempotent operation to have side effects.

Puppet attempts to limit side effects, but does not eliminate them by any means; doing so would be nearly impossible given Puppet’s role as a system management tool.

Some side effects are designed into the system. For example, every resource will generate a notification upon changing a resource state that may be consumed by other resources. The notification is used to restart services in order to ensure that the running state of the system reflects the configured state. File bucketing is another obvious intended side effect designed into Puppet.

Some side effects are unavoidable. Every access to a file on disk will cause that file’s atime to be incremented unless the entire filesystem is mounted with the noatime attribute. This is of course true whether or not Puppet is being invoked in noop mode.

### Resource level idempotence

Many common tasks are not idempotent by nature, and will either throw an error or produce undesirable results if invoked multiple times. For example, the following code is not idempotent because it will set a state the first time, and throw an error each time it’s subsequently invoked.

**Example 1-8. A non-idempotent operation that will throw an error**

```bash
useradd alice
```

The following code is not idempotent, because it will add undesirable duplicate host entries each time it’s invoked:

**Example 1-9. A non-idempotent operation that will create duplicate records**

```bash
echo '127.0.0.1 example.localdomain' >> /etc/hosts
```

The following code is idempotent, but will probably have undesirable results:

**Example 1-10. An idempotent operation that will destroy data**

```bash
echo '127.0.0.1 example.localdomain' > /etc/hosts
```

To make our example idempotent without clobbering /etc/hosts, we can add a simple check before modifying the file:

**Example 1-11. An imperative idempotent operation**

```bash
grep -q '^127.0.0.1 example.localdomain$' /etc/hosts \ 
	|| echo '127.0.0.1 example.localdomain' >> /etc/hosts
```

The same example is simple to write in a declarative and idempotent way using the native Puppet host resource type:

**Example 1-12. Declarative Idempotence with Puppet**

```json
host { 'example.localdomain':
  ip => '127.0.0.1',
}
```

Alternatively, we could implement this example using the *file_line* resource type from the optional *stdlib* Puppet module:

**Example 1-13. Idempotent host entry using the File_line resource type**

```json
file_line { 'example.localdomain host':
	path => '/etc/hosts',
	line => '127.0.0.1 example.localdomain',
}
```

In both cases, the resource is modeled in a declarative way and is idempotent by its very nature. Under the hood, Puppet handles the complexity of determining whether the line already exists, and how it should be inserted into the underlying file. Using the native host resource type, Puppet also determines what file should be modified and where that file is located.

The idempotent examples are safe to run as many times as you like. This is a huge benefit across large environments; when trying to apply a change to thousands of hosts, it’s relatively common for failures to occur on a small subset of the hosts being managed. Perhaps the host is down during deployment? Perhaps you experienced some sort of transmission loss or timeout when deploying a change? If you are using an idempotent language or process to manage your systems, it’s possible to handle these exceptional cases simply by performing a second configuration run against the affected hosts (or even against the entire infrastructure.)

When working with native resource types, you typically don’t have to worry about idempotence; most resources handle idempotence natively. A couple of notable exceptions to this statement are the *exec* and *augeas* resource types. We’ll explore those in depth in Chapter 5.

Puppet does however attempt to track whether or not a resource has changed state. This is used as part of Puppet’s reporting mechanism and used to determine whether or not a signal should be send to resources with a notify relationship. Because Puppet tracks whether or not a resource has made a change, it’s entirely possible to write code that is functionally idempotent, without meeting the criteria of idempotent from Puppet’s resource model.

For example, the following code is functionally idempotent, but will report as having changed state with every Puppet run.

**Example 1-14. Puppet code that will report as non-idempotent**

```json
exec { 'grep -q /bin/bash /etc/shells || echo /bin/bash >> /etc/shells':
	path     => '/bin',
	provider => 'shell',
}
```

Puppet’s idempotence model relies on a special aspect of its resource model. For every resource, Puppet first determines that resource’s current state. If the current state does not match the defined state of that resource, Puppet invokes the appropriate methods on the resources native provider to bring the resource into conformity with the desired state. In most cases, this is handled transparently, however there are a few exceptions that we will discuss in their respective chapters. Understanding these cases will be critical in order to avoid breaking Puppet’s simulation and reporting models.

This example will report correctly:

**Example 1-15. Improved code that will report as Idempotent**

```json
exec { 'echo /bin/bash >> /etc/shells': 
	path =>'/bin',	
	unless => 'grep -q /bin/bash /etc/shells',
}
```

In this case, unless provides a condition Puppet can use to determine whether or not a change actually needs to take place.

![tip_animal](http://s.radar.oreilly.com/wp-files/2/2015/04/tip_animal.jpg)
Using condition such as unless and only if properly will help produce safe and robust exec resources. We will explore this in depth in Chapter 5.

A final surprising example is the notify resource, which is often used to produce debugging information and log entries.

**Example 1-16. The Notify resource type**

```json
notify { 'example':
	message  => 'Danger, Will Robinson!'
}
```

The notify resource generates an alert every time its invoked, and will always report as a change in system state.

### Run level idempotence

Puppet is designed to be idempotent both at the resource level and at the run level. Much like resource idempotence means that a resource applied twice produces the same result, run level idempotence means that invoking Puppet multiple times on a host should be safe, even on live production environment.

![tip_animal](http://s.radar.oreilly.com/wp-files/2/2015/04/tip_animal.jpg)
You don’t have to run Puppet in enforcing mode in production.

Run level idempotence is a place where Puppet’s model of change becomes just as important as whether or not the resources are functionally idempotent. Remember that before performing any configuration change, Puppet will first determine whether or not the resource currently conforms to policy. Puppet will only make a change if resources are in an inconsistent state. The practical implication is that if Puppet does not report having made any changes, you can trust this is actually the case.

In practice, determining whether or not your Puppet runs are truly idempotent is fairly simple: If Puppet reports no changes upon its second invocation on a fresh system, your Puppet codebase is idempotent.

Because Puppet’s resources tend to have side effects, it’s much possible (easy) to break Puppet’s idempotence model if we don’t carefully handle resource dependencies.

**Example 1-17. Ordering is critical for run-level idempotence**

```json
package { 'httpd': 
	ensure => 'installed',
}
 
file { '/etc/httpd/conf/httpd.conf':
	ensure => 'file',
	content => template('apache/httpd.conf.erb'),
}
 
Package['httpd'] ->
File['/etc/httpd/conf/httpd.conf']
```

The *file* resource will not create paths recursively. In example 1-17, the httpd package must be installed before the httpd.conf file resource is enforced; and it depends on the existence of `/etc/httpd/conf/httpd.conf`, which is only present after the httpd package has been installed. If this dependency is not managed, the *file* resource becomes non-idempotent; upon first invocation of Puppet it may throw an error, and only enforce the state of httpd.conf upon subsequent invocations of Puppet.

Such issues will render Puppet convergent. Because Puppet typically runs on a 30 minute interval, convergent infrastructures can take a very long time to reach a converged state.

There are a few other issues that can render Puppet non-idempotent

### Non-deterministic code

As a general rule, the Puppet DSL is deterministic, meaning that a given set of inputs (manifests, facts, exported resources, etc) will always produce the same output with no variance.

For example, the language does not implement a `random()` function; instead a `fqdn_rand()` function is provided that returns random values based on a static seed (the host’s fully qualified domain name.) This function is by its very nature not cryptographically secure, and not actually random at all. It is however useful for in cases where true randomness is not needed, such as distributing the start times of load intensive tasks across the infrastructure.

Non-deterministic code can pop up in strange places with Puppet. A notorious example is Ruby 1.8.7’s handling of hash iteration. The following code is non-deterministic with Ruby 1.8.7; the output will not preserve the original order and will change between runs:

**Example 1-18. Non-deterministic hash ordering with Ruby 1.8.x**

```ruby
$example = {
	'a' => '1',
	'b' => '2',
	'c' => '3',
}
 
alert(inline_template("<%= @example.to_a.join(' ') %>\n"))
```

Another common cause of non-deterministic code pops up when our code is dependent on a transient state.

```json
file { '/tmp/example.txt': 
	ensure => 'file',
	content => "${::servername}\n",
}
```

Example 1-18 will not be idempotent if you have a load balanced cluster of Puppet Masters. The value of `$::servername` changes depending on which master compiles the catalog for a particular run.

With non-deterministic code, Puppet loses run level idempotence. For each invocation of Puppet, some resources will change shape. Puppet will converge, but it will always report your systems as having been brought into conformity with its policy, rather than being conformant. As a result, it’s virtually impossible to determine whether or not changes are actually pending for a host. It’s also more difficult to track what changes were made to the configuration, and when they were made.

Non deterministic code also has the side effect that it can cause services to restart due to Puppet’s notify behavior. This can cause unintended service disruption.

### Stateless

Puppet’s client / server API is stateless, and with a few major (but optional) exceptions, catalog compilation is a completely stateless process.

A stateless system is a system that does not preserve state between requests; each request is completely independent from previous request, and the compiler does not need to consult data from previous request in order to produce a new catalog for a node.

Puppet uses a RESTful API over HTTPS for client server communications.

With master/agent Puppet, the Puppetmaster need only have a copy of the facts supplied by the agent in order to compile a catalog. Natively, Puppet doesn’t care whether or not this is the first time it has generated a catalog for this particular node, nor whether or not the last run was successful, or if any change occurred on the client node during the last run. The nodes catalog is compiled in its entirety every time the node issues a catalog request. The responsibility for modeling the current state of the system then rests entirely on the client, as implemented by the native resource providers.

IF you don’t use a puppetmaster or have a small site with a single master, statelessness may not be a huge benefit to you. For medium to large sites however, keeping Puppet stateless is tremendously useful. In a stateless system, all Puppetmasters are equal. There is no need to synchronize data or resolve conflicts between masters. There is no locking to worry about. There is no need to design a partition tolerant system in case you lose a datacenter or data-link, and no need to worry about clustering strategies. Load can easily be distributed across a pool of masters using a load balancer or DNS SRV record, and fault tolerance is as simple as ensuring nodes avoid failed masters.

It is entirely possible to submit state to the master using custom facts or other techniques. It’s also entirely possible to compile a catalog conditionally based on that state. There are cases where security requirements or particularly idiosyncratic software will necessitate such an approach. Of course, this approach is most often used when attempting to write non-declarative code in Puppet’s DSL. Fortunately, even in these situations, the Server doesn’t have to actually store the node’s state between runs; the client simply re-submits its state as part of its catalog request.

If you keep your code declarative, it’s very easy to work with Puppet’s stateless client/server configuration model. IF a manifest declares that a resource such as a user should exist, the compiler doesn’t have to be concerned with the current state of that resource when compiling a catalog. The catalog simply has to declare a desired state, and the Puppet agent simply has to enforce that state.

Puppet’s stateless model has several major advantages over a stateful model:

- Puppet scales horizontally
- Catalogs can be compared
- Catalogs can be cached locally to reduce server load

It is worth noting that there are a few stateful features of Puppet. It’s important to weigh the value of these features against the cost of making your Puppet infrastructure stateful, and to design your infrastructure to provide an acceptable level of availability and fault tolerance. We will discuss how to approach each of these technologies in upcoming chapters, but a quick overview is provided here.

### Sources of state

In the beginning of this section, I mentioned that there are a few features and design patterns that can impose state on Puppet catalog compilation. Let’s look at some of these features in a bit more depth.

#### Filebucketing

Filebucketing is an interesting and perhaps underappreciated feature of the File resource type. If a filebucket is configured, the file provider will create a backup copy of any file before overwriting the original file on disk. The backup may be bucketed locally, or it can be submitted to the Puppetmaster.

Bucketing your files is useful for keeping backups, auditing, reporting, and disaster recovery. It’s immensely useful if you happen to blast away a configuration you needed to keep, or if you discover a bug and would like to see how the file is changed. The Puppet enterprise console can use filebucketing to display the contents of managed files.

Filebuckets can also be used for content distribution, however using a filebucket this way creates state. Files are only present in a bucket when placed there; either as a backup from a previous run, or by the static_compiler terminus. Placing a file in the bucket only happens during a Puppet run, and Puppet has no internal facility to synchronize buckets between masters. Reliance upon file buckets for content distribution can create problems if not applied cautiously. It can create problems when migrating hosts between datacenters, when rebuilding masters. Use of filebucketing in your modules can also create problems during local testing with `puppet apply`.

#### Exported resources

Exported resources provide a simple service discovery mechanism for Puppet. When a puppetmaster or agent compiles a catalog, resources can be marked as exported by the compiler. Once the resources are marked as exported, they are recorded in a SQL database. Other nodes may then collect the exported resources, and apply those resources locally. Exported resources persist until they are overwritten or purged.

As you might imagine, exported resources are, by definition stateful and will affect your catalog if used.

We will take an in depth look at PuppetDB and exported resources in Chapter 2. For the time being, just be aware that exported resources introduce a source of state into your infrastructure.

In this example, a pool of webservers export their pool membership information to a haproxy load balancer, using the [puppetlabs/haproxy](https://forge.puppetlabs.com/puppetlabs/haproxy/1.1.0/readme) module and exported resources.

**Example 1-19. Declaring state with an exported resource**

```json
include haproxy
haproxy::listen { 'web':
	ipaddress => $::ipaddress,
	ports     => '80',
}
 
Haproxy::Balancermember <<| listening_service == 'web' |>>
```

**Example 1-20. Applying state with an exported resource**

```json
@@haproxy::balancermember { $::fqdn:
  listening_service => 'web',
  server_names      => $::hostname,
  ipaddresses       => $::ipaddress,
  ports             => '80',
  options           => 'check',
}
```

![tip_animal](http://s.radar.oreilly.com/wp-files/2/2015/04/tip_animal.jpg)
This particular example is a relatively safe use of exported resources; if PuppetDB for some reason became unavailable the pool would continue to work; new nodes would not be added to the pool until PuppetDB was restored. TODO: Validate what I just said is true given the internal use of concat on this module…



Exported resources rely on PuppetDB, and are typically stored in a PostgreSQL database. While the PuppetDB service is fault tolerant and can scale horizontally, the PostgreSQL itself scales Vertically and introduces a potential single point of failure into the infrastructure.

#### Hiera

Hiera is by design a pluggable system. By default is provides JSON and YAML backends, both of which are completely stateless. However, it is possible to attach Hiera to a database or inventory service, including PuppetDB. If you use this approach, it can introduce a source of state into your Puppet Infrastructure. We will explore Hiera in depth in Chapter 6.

#### Inventory and reporting

The Puppet infrastructure maintains a considerable amount of reporting information pertaining to the state of each node. This information includes facts about each node, detailed information about the catalogs sent to the node, and the reports produced at the end of each Puppet run. While this information is stateful, this information is not typically consumed when compiling catalogs.

There are plugins to Puppet that allow inventory information to be used during catalog compilation, however these are not core to Puppet.

#### Custom facts

Facts themselves do not inherently add state to your Puppet manifests, however they can be used to communicate state to the Puppetmaster, which can then be used to compile conditional catalogs. Using facts in this way does not create the scaling and availability problems inherent in server site state, but it does create problems if you intend to use cached catalogs, and it does reduce the effectiveness of your reporting infrastructure.

# Module Review

## Module 1 Wrap Up: Automating with Configuration Management

We started our journey talking about what would happen if you needed to upgrade a package in a fleet of 1,000 different servers. If you've never heard about configuration management before, an upgrade like that probably seemed like a super long and boring task, right? But now you know that there's a bunch of tools you can use to make your life much easier when making large-scale changes like that one. We've talked about the automation that's necessary for provisioning, managing and adapting a fleet of computers in a scalable way. 

We called out that an important concept in today's IT world is to treat our infrastructure as code. This lets us manage our fleet of computers in a consistent, versionable, reliable and repeatable way. To figure out how to get there, we've covered a lot of concepts related to configuration management, like how these tools use a domain specific language to help us clearly state what we want our system to look like after the tools have run. We've mentioned that the language is declarative because we declare our goals rather than detail the steps to get there, and most importantly the actions taken must be idempotent so that several runs of the same rules always lead to the same results. 

All along, we've been using Puppet as an example of how configuration management tools work. We looked into the puppet DSL syntax and checked out the most common resources: packages, files and services. We'll learn about other resources and other advanced techniques in future videos. But by now you should have a pretty good idea of what Puppet rules look like and how you can put into action the configuration management concepts that we discussed. With the concepts we've covered, you're probably starting to see how keeping your fleet of machines, whether they're virtual or physical, off of a pedestal is good practice. If something breaks, goes down or catches fire literally or figuratively, you can easily spin up a replacement because you know exactly what it's supposed to look like from the configuration and you can deploy it easily using the automation. 

In the next module, we'll check out how you can deploy Puppet in your infrastructure and look into some more advanced configuration management and change management techniques. Before that, you'll have the opportunity to try out fixing a system where the configuration management isn't doing what it's supposed to. You'll see what running the Puppet agent looks like in practice and find out what's wrong with the deployed rules, and then get the automation to behave as expected. Cool, right? Let's go for it.

# Deploying Puppet Locally

## Deploying Puppet

Welcome back, congrats on making it through the first lab of the course. In the last module, we looked into some basic configuration management concepts, and what those look like in Puppet. In this module, we're going to dive deeper into how to use these tools. We'll kick off with how to install Puppet on your computer and how to use a simple test setup to **check your rules work as expected**. This test setup will let you try out the examples in these videos on your own computer. 

We'll also show you how to configure the typical **client-server set-up** with Puppet clients connecting and authenticating to the Puppet server to get the rules that they should apply and on top of this, we'll talk about how to use testing techniques and releasing best practices to safely deploy changes to clients of our configuration management system. You've already learned the basics of Puppet resources. 

We've seen the three most important resources, packages, files, and services. In this module, we'll check out more ways of using the basic resources and Puppet's DSL. We'll look into how you can apply different sets of rules to different nodes in your fleet, how you can organize your rules so that they're easier to maintain, and a bunch of other Puppet best-practices. We'll wrap up with another lab exercise. This time though, you'll be flexing your Puppet skills to manage the deployment and pulling the strings to make the system do what you want. Ready? Let's dive in.

## Applying Rules Locally

Up to now we've been getting to know Puppet syntax and understanding the different resources available. It's now time for the next step, trying out some **Puppet rules** on our local computer. In an earlier video, we called out that Puppet is usually deployed in a **client-server architecture**. But that's not the only way we can use Puppet. We can also use it as a **stand-alone application run from the command line**. This is common when testing new configurations. It can be the preferred configuration for complex setups where connecting to a master is no longer the best approach. 

When using a stand-alone Puppet, the same computer processes the facts, calculates the rules that need to be applied, and makes any necessary changes locally. So to get started with our Puppet deployment, let's first install Puppet and then we can start experimenting with running rules locally. In later videos, we'll check out how to create a client-server deployments. 

As we've called out, Puppet is available on a number of different platforms. We can either install it from the package management system available in the OS or download it from the official website. Both options work fine and the best one to choose will depend on our specific needs. For this exercise, we'll just go with the Puppet packages provided by the Ubuntu distribution. We'll do that by installing the Puppet master package using `sudo apt install puppet-master`.

We now have the package installed and can start trying out a few rules. We'll begin by creating the simplest possible Puppet file. We can make it more complex as we improve our deployments. For this example, we want to use Puppet to make sure that some useful tools for debugging problems are installed on each computer in our fleet. To do this, we first have to create a file where we'll store the rules that we want to apply. In Puppet lingo, these files are called **manifests** and they must end with a `.pp` extension. 

So we'll create a new file called `tools.pp` and in this file, we'll create a **package resource**. We'll start by managing the `htop` package which is a tool similar to top that can show us some extra information. We'll state that we want Puppet to **ensure** that we have this package **present** on our computer. Cool. That was simple. That's all we have to do. This resource will take care of installing the package for us. Let's save the file and try it out. But before actually applying the rules, we want to check that the command isn't present yet.

`htop` isn't installed yet. Let's fix that by running our rules using `sudo puppet apply -v tools.pp`.

The `-v` flag tells Puppet that we want to get verbose output which will tell us what's going on while Puppet is applying the rules in the file that we pass to it. So here, Puppet first told us that it was loading the facts. Then, that it compiled a catalog. After that, it told us that it was applying the current configuration. Then, that it installed the package we requested. Finally, it let us know that it finished applying this catalog. 

You're probably wondering, what's a **catalog**? We called out in an earlier video that after loading all facts for a computer, the server calculates which rules actually need to be applied. For example, if a packet should only be installed when a certain condition is met, this condition is evaluated **on the server side based on the gathered facts**. T<u>he catalog is the list of rules that are generated for one specific computer once the server has evaluated all variables, conditionals, and functions</u>. In this example, the **catalog will be exactly the same as our code** because the code didn't include any variables, functions, or conditionals. More complex sets of rules can lead to different catalogs depending on fact values. It's now time to check if our rules actually works. Let's try running the htop command again now that Puppet has installed it for us.

Yes, this time it worked. If our computer was misbehaving, we could now use this tool to get a better idea why. But fortunately, our computer's on its best behavior. So we'll exit now using `q`. Let's see what happens if we try to apply the Puppet rules again now that the package is installed.

Puppet's smart. It noticed that the package is **already installed** so it didn't try to install the package again. This means it applied the catalog much faster because nothing had to be changed. We've now seen how to write a Puppet resource in a manifest file and then use puppet apply to apply those rules to one computer. Up next, we'll check out how we can manage relationships between different Puppet resources and what that looks like when applied.

## Managing Resource Relationships

In our last video, we wrote a very simple manifest which we then applied locally. That was a great way to practice applying Puppet rules, but it was super-simple. Let's challenge ourselves with something a bit more tricky. The Puppet manifests that we use to manage computers in our fleet usually include a bunch of different resources that are related to each other. You're not going to configure a package that's not installed and you don't want to start a service until both the package and the configuration are in place. Puppets lets us control this with **resource relationships**. Let's check this out in an example. We have a file called `ntp.pp`, that has a bunch of resources related to the NUTS configuration like the one we've seen in an earlier video.

```json
class ntp {
    package { 'ntp':
            ensure => latest,
            }
	file { '/etc/ntp.conf':
          source => '/home/user/ntp.conf'
          replace => true,
          require => Package['ntp'],
		  notify => Service['ntp'],
         }
	service { 'ntp':
             enable => true,
             ensure => running,
             require => File['/etc/ntp.conf']
            }
}
```

This time, on top of declaring the resources that we need to manage, we're also declaring a few **relationships** between them. We see that the configuration file **requires** the NTP package and the service **requires** the configuration file. This way, Puppet knows that before starting the service, the **configuration file needs to be correctly set**, and before sending the configuration file, the **package needs to be installed.** 

We're also declaring that the NTP service **should be notified** if the configuration file changes. That way, <u>if we make additional changes to the contents of the configuration file in the future, the service will get reloaded with the new settings</u>. If you look closely, you might notice that the resource types are written in lowercase, but relationships like require or notify use uppercase for the first letter of the resource. This is part of Puppet syntax. 

**We write resource types in lowercase when declaring them, but capitalize them when referring to them from another resource's attributes.** This sounds confusing right now, don't worry. It might take a while to wrap your head around it, but it will eventually click. Now, one last thing. At the bottom of the file, we have a call to include NTP. That's why we told Puppet that we want to apply the rules described in a class. For this example, we put the definition of the class and the call to include the class in the same file. Typically, the class is defined in one file and include it in another. We'll checkout examples for this in later videos. All right. Let's apply these rules locally.

Great. Our rules have run and in the verbose output, we can see that it did a bunch of things. 

- First, it **installed** the package. 
- Then it **checked** that the configuration file needed to be updated and so it **changed its contents**. 
- Finally, after changing the contents of the configuration, Puppet knew to **restart** the NTP service. 

We see here how our Puppet rules have translated into a few different actions. That's cool, but it's about to get even better. Let's make a change to the configuration file by editing the ntp.com file in this directory.

This is the configuration values by the NTP service. It's currently using a bunch of servers from ntp.org. But instead of those servers, we want to try out the NTP servers provided by Google. These are called time1.google.com, and then time2, time3, and time4.

We've made the change, we'll save with `:wq` and then rerun our Puppet rules with the new configuration file.

Awesome. Puppet updated the configuration file with the new contents and then refresh the service, so it loaded the config. Success. In this video, we've seen how we can apply a Puppet manifests that includes a class with a bunch of resources. We grouped all of the information related to the NTP service in a manifest specific to it, which is common practice when dealing with Puppet rules. We want to k**eep related operations together** and separate things that are unrelated. Up next, we'll look into how we can do that using Puppet modules.

## Organizing Your Puppet Modules

In any configuration management deployment, there's usually a lot of different things to manage. We might want to install some packages, copy some configuration files, start some services, schedule some periodic tasks, make sure some users and groups are created and have access to specific devices, and maybe execute a few commands that aren't provided by existing resources. 

On top of that, there might be different configurations applied to the different computers in the fleet. For example, workstations and laptops might include resources that aren't used on servers. Each distinct type of server will need its **own specific setup**. There's a lot of different things to manage. We need to organize all these resources and information in a way that helps us maintain them long-term. This means **grouping related resources**, giving the groups **good names,** and making sure that the organization **will make sense** to new users. In puppet, we organize our manifests into modules. 

**A module is a collection of manifests and associated data.** We can put any resource we want into a module, but to keep our configuration management organized, we'll group things together under a sensible topic. For example, we could have a module for everything related to monitoring the computer's health, another one for setting up the network stack, and yet another one for configuring a web serving application. So the **module ship the manifest in the associated data**, but how is this organized? 

All manifests gets stored in a directory called `Manifests`. 

The rest of the data is **stored in different directories** depending on what it does. 

The `Files` directory includes files that are copied into the client machines without any changes, like the `ntp.conf` file that we saw in our last video. 

The `Templates` directory includes files that are preprocessed before they've been copied into the client machines. These **templates** can include **values that get replaced after calculating the manifests**, or sections that are only present if certain conditions are valid. There's a bunch more directories that can be part of a module depending on what exactly the module does. But you don't need to worry about these when creating your first puppet module. 

You can start with the simple module that just has one manifest in the `Manifest` directory. This file **should be called** `init.pp` and it should define a class with the same name as the module that you're creating. Then any files that your rules use need to be stored in the `Files` or `Templates` directories depending on whether you copy them directly or need to preprocess them. For example, this is how the NTP class that we saw in our last video looks like when turned into a module.

There's an init.pp file, which contains the NTP classes that we saw before, and the ntp.conf file that gets deployed onto the machine is now stored in the files directory. Modules like these can look pretty much **the same no matter who's using them**. That's why over time, system administrators using puppet have shared the modules they've written, letting others use the same rules. By now, there's a **large collection of prepackaged modules** that are shipped and ready to use. If one of those modules does what we want, we can just install it on our Puppet server and use it in our deployments. Let's install the Apache module provided by Puppet Labs to check out how this works.

```bash
sudo apt install puppet-module-puppetlabs-apache 
```

We've installed the module. Let's have a quick look at its contents. First, we'll change into the directory where the module files are stored and list its contents.

We see the Files, Manifests, and Templates directories that we mentioned. On top of that, there's a `lib` directory that adds functions and fact to the ones already shipped by puppet. The `metadata.json` file includes some additional data about the module we just installed, like which versions of which operating systems it's compatible with. Let's peek into the manifest directory.

That's a lot of files, like how we split the different things that we want to manage into separate modules. We can also split each separate functionality that we want to configure into separate manifests. This helps us organize our code when we make changes to it, and to see how this directory also contains its own `init.pp`. As we called out, this manifest is **special**. **It needs to always be present** because it's the first one that's read by puppet when a module gets included. So how do we include a module like this one? It's pretty easy. Let's create a manifest file that includes the module we've just installed.

```json
include ::apache
```

Here, we're telling Puppet to include the Apache module. The **double colon** before the module name, let's puppet know that this is a **global module**. Let's save this file now and apply it using Puppet apply like we did before.

Our manifest was super-simple, it just include the Apache module. But by including the module, we got puppet to apply all the rules run by default in the module. We now have an Apache server configured and ready to run on this machine. We've just seen how we can organize our code in modules and how we can even use modules provided by other teams so we don't have to reinvent the wheel. Up next, there's a reading with pointers to more information, followed by a quick quiz. After that, meet me over in the next video, where we'll check out what we need to do to deploy our rules to more machines.

# The Puppet language style guide

**Sections**

- Module design practices
  - [Spacing, indentation, and whitespace](https://puppet.com/docs/puppet/7.3/style_guide.html#spacing-indentation-and-whitespace)
  - [Arrays and hashes](https://puppet.com/docs/puppet/7.3/style_guide.html#arrays-and-hashes)
  - [Quoting](https://puppet.com/docs/puppet/7.3/style_guide.html#quoting)
  - [Escape characters](https://puppet.com/docs/puppet/7.3/style_guide.html#escape-characters)
  - [Comments](https://puppet.com/docs/puppet/7.3/style_guide.html#comments)
  - [Functions](https://puppet.com/docs/puppet/7.3/style_guide.html#functions)
  - [Improving readability when chaining functions](https://puppet.com/docs/puppet/7.3/style_guide.html#improving-readability-when-chaining-functions)
- Resources
  - [Resource names](https://puppet.com/docs/puppet/7.3/style_guide.html#resource-names)
  - [Arrow alignment](https://puppet.com/docs/puppet/7.3/style_guide.html#arrow-alignment)
  - [Attribute ordering](https://puppet.com/docs/puppet/7.3/style_guide.html#attribute-ordering)
  - [Resource arrangement](https://puppet.com/docs/puppet/7.3/style_guide.html#resource-arrangement)
  - [Symbolic links](https://puppet.com/docs/puppet/7.3/style_guide.html#symbolic-links)
  - [File modes](https://puppet.com/docs/puppet/7.3/style_guide.html#file-modes)
  - [Multiple resources](https://puppet.com/docs/puppet/7.3/style_guide.html#multiple-resources)
  - [Legacy style defaults](https://puppet.com/docs/puppet/7.3/style_guide.html#legacy-style-defaults)
  - [Attribute alignment](https://puppet.com/docs/puppet/7.3/style_guide.html#attribute-alignment)
  - [Defined resource types](https://puppet.com/docs/puppet/7.3/style_guide.html#defined-resource-types)
- Classes and defined types
  - [Separate files](https://puppet.com/docs/puppet/7.3/style_guide.html#separate-files)
  - [Internal organization of classes and defined types](https://puppet.com/docs/puppet/7.3/style_guide.html#internal-organization-of-classes-and-defined-types)
  - [Public and private](https://puppet.com/docs/puppet/7.3/style_guide.html#public-and-private)
  - [Chaining arrow syntax](https://puppet.com/docs/puppet/7.3/style_guide.html#chaining-arrow-syntax)
  - [Nested classes or defined types](https://puppet.com/docs/puppet/7.3/style_guide.html#nested-classes-or-defined-types)
  - [Display order of parameters](https://puppet.com/docs/puppet/7.3/style_guide.html#display-order-of-parameters)
  - [Parameter defaults](https://puppet.com/docs/puppet/7.3/style_guide.html#parameter-defaults)
  - [Exported resources](https://puppet.com/docs/puppet/7.3/style_guide.html#exported-resources)
  - [Parameter indentation and alignment](https://puppet.com/docs/puppet/7.3/style_guide.html#parameter-indentation-and-alignment)
  - [Class inheritance](https://puppet.com/docs/puppet/7.3/style_guide.html#class-inheritance)
  - [Public modules](https://puppet.com/docs/puppet/7.3/style_guide.html#public-modules)
  - [Type signatures](https://puppet.com/docs/puppet/7.3/style_guide.html#type-signatures)
- Variables
  - [Referencing facts](https://puppet.com/docs/puppet/7.3/style_guide.html#referencing-facts)
  - [Namespacing variables](https://puppet.com/docs/puppet/7.3/style_guide.html#namespacing-variables)
  - [Variable format](https://puppet.com/docs/puppet/7.3/style_guide.html#variable-format)
- Conditionals
  - [Simple resource declarations](https://puppet.com/docs/puppet/7.3/style_guide.html#simple-resource-declarations)
  - [Defaults for case statements and selectors](https://puppet.com/docs/puppet/7.3/style_guide.html#defaults-for-case-statements-and-selectors)
  - [Conditional statement alignment](https://puppet.com/docs/puppet/7.3/style_guide.html#conditional-statement-alignment)
- Modules
  - [Versioning](https://puppet.com/docs/puppet/7.3/style_guide.html#versioning)
  - [Module metadata](https://puppet.com/docs/puppet/7.3/style_guide.html#module-metadata)
  - [Dependencies](https://puppet.com/docs/puppet/7.3/style_guide.html#dependencies)
  - [README](https://puppet.com/docs/puppet/7.3/style_guide.html#readme)
  - [Documenting Puppet code](https://puppet.com/docs/puppet/7.3/style_guide.html#documenting-puppet-code)
  - [CHANGELOG](https://puppet.com/docs/puppet/7.3/style_guide.html#changelog)
  - [Examples](https://puppet.com/docs/puppet/7.3/style_guide.html#examples)
  - [Testing](https://puppet.com/docs/puppet/7.3/style_guide.html#testing)

This style guide promotes consistent formatting in the Puppet language, giving you a common pattern, design, and style to follow when developing modules. This consistency in code and module structure makes it easier to update and maintain the code.

This style guide applies to Puppet 4 and later. Puppet 3 is no longer supported, but we include some Puppet 3 guidelines in case you're maintaining older code.

**Tip:** Use [puppet-lint](http://puppet-lint.com/) and [metadata-json-lint](https://github.com/voxpupuli/metadata-json-lint) to check your module for compliance with the style guide.

No style guide can cover every circumstance you might run into when developing Puppet code. When you need to make a judgement call, keep in mind a few general principles.

- Readability matters

  If you have to choose between two equal alternatives, pick the more readable one. This is subjective, but if you can read your own code three months from now, it's a great start. In particular, code that generates readable diffs is highly preferred.

- Scoping and simplicity are key

  When in doubt, err on the side of simplicity. A module should contain related resources that enable it to accomplish a task. If you describe the function of your module and you find yourself using the word "and," consider splitting the module. Have one goal, with all your classes and parameters focused on achieving it.

- Your module is a piece of software

  At least, we recommend that you treat it that way. When it comes to making decisions, choose the option that is easier to maintain in the long term.

These guidelines apply to Puppet code, for example, code in Puppet modules or classes. To reduce repetitive phrasing, we don't include the word 'Puppet' in every description, but you can assume it.

For information about the specific meaning of terms like 'must,' 'must not,' 'required,' 'should,' 'should not,' 'recommend,' 'may,' and 'optional,' see [RFC 2119](http://www.faqs.org/rfcs/rfc2119.html).

## Module design practices 

Consistent module design practices makes module contributions easier.

### Spacing, indentation, and whitespace

Module manifests should follow best practices for spacing, indentation, and whitespace.

Manifests:

- Must use two-space soft tabs.

- Must not use literal tab characters.

- Must not contain trailing whitespace.

- Must include trailing commas after all resource attributes and parameter definitions.

- Must end the last line with a new line.

- Must use one space between the resource type and opening brace, one space between the opening brace and the title, and no spaces between the title and colon.

  Good:

  ```json
  file { '/tmp/sample':
  ```

  Bad: Space between title and colon:

  ```json
  file { '/tmp/sample' :
  ```

  Bad: No spaces:

  ```json
  file{'/tmp/sample':
  ```

  Bad: Too many spaces:

  ```json
  file     { '/tmp/sample':
  ```

- Should not exceed a 140-character line width, except where such a limit would be impractical.

- Should leave one empty line between resources, except when using dependency chains.

- May align hash rockets (`=>`) within blocks of attributes, one space after the longest resource key, arranging hashes for maximum readability first.

### Arrays and hashes

To increase readability of arrays and hashes, it is almost always beneficial to break up the elements on separate lines.

Use a single line only if that results in overall better readability of the construct where it appears, such as when it is very short. When breaking arrays and hashes, they should have:

- Each element on its own line.
- Each new element line indented one level.
- First and last lines used only for the syntax of that data type.

Good: Array with multiple elements on multiple lines:

```json
service { 'sshd':
  require => [
    Package['openssh-server'],
    File['/etc/ssh/sshd_config'],
  ],
}
```

Good: Hash with multiple elements on multiple lines:

```json
$myhash = {
  key       => 'some value',
  other_key => 'some other value',
}
```

Bad: Array with multiple elements on same line:

```json
service { 'sshd':
  require => [ Package['openssh-server'], File['/etc/ssh/sshd_config'], ],
}
```

Bad: Hash with multiple elements on same line:

```json
$myhash = { key => 'some value', other_key => 'some other value', }
```

Bad: Array with multiple elements on different lines, but syntax and element share a line:

```json
service { 'sshd':
  require => [ Package['openssh-server'],
    File['/etc/ssh/sshd_config'],
  ],
}
```

Bad: Hash with multiple elements on different lines, but syntax and element share a line:

```json
$myhash = { key => 'some value',
  other_key     => 'some other value',
}
```

Bad: Array with an indention of elements past two spaces: 

```json
service { 'sshd':
  require => [
              Package['openssh-server'],
              File['/etc/ssh/sshd_config'],
  ],
}
```

### Quoting

As long you are consistent, strings may be enclosed in single or double quotes, depending on your preference.

Regardless of your preferred quoting style, all variables MUST be enclosed in braces when interpolated in a string.

For example:

Good:

```json
"/etc/${file}.conf"
"${facts['operatingsystem']} is not supported by ${module_name}"
```

Bad:

```json
"/etc/$file.conf"
```



**Option 1: Prefer single quotes**

Modules that adopt this string quoting style MUST enclose all strings in single quotes, except as listed below.

For example:

Good:

```json
owner => 'root'
```

Bad:

```json
owner => "root"
```

A string MUST be enclosed in double quotes if it:

- Contains variable interpolations.

  - Good:

    ```json
    "/etc/${file}.conf"
    ```

  - Bad:

    ```json
    '/etc/${file}.conf'
    ```

- Contains escaped characters not supported by single-quoted strings.

  - Good:

    ```json
    content => "nameserver 8.8.8.8\n"
    ```

  - Bad:

    ```json
    content => 'nameserver 8.8.8.8\n'
    ```

A string SHOULD be enclosed in double quotes if it:

- Contains single quotes.

  - Good:

    ```json
    warning("Class['apache'] parameter purge_vdir is deprecated in favor of purge_configs")
    ```

  - Bad:

    ```json
    warning('Class[\'apache\'] parameter purge_vdir is deprecated in favor of purge_configs')
    ```



**Option 2: Prefer double quotes**

Modules that adopt this string quoting style MUST enclose all strings in double quotes, except as listed below.

For example:

Good:

```json
owner => "root"
```

Bad:

```json
owner => 'root'
```

A string SHOULD be enclosed in single quotes if it does not contain variable interpolations AND it:

- Contains double quotes.

  - Good:

    ```json
    warning('Class["apache"] parameter purge_vdir is deprecated in favor of purge_configs')
    ```

  - Bad:

    ```json
    warning("Class[\"apache\"] parameter purge_vdir is deprecated in favor of purge_configs") 
    ```

- Contains literal backslash characters that are not intended to be part of an escape sequence.

  - Good:

    ```json
    path => 'c:\windows\system32'
    ```

  - Bad:

    ```json
    path => "c:\\windows\\system32"
    ```

If a string is a value from an enumerable set of options, such as `present` and `absent`, it SHOULD NOT be enclosed in quotes at all.

For example:

Good:

```json
ensure => present
```

Bad:

```json
ensure => "present"
```

### Escape characters

Use backslash (`\`) as an escape character.

For both single- and double-quoted strings, escape the backslash to remove this special meaning: `\\` This means that for every backslash you want to include in the resulting string, use two backslashes. As an example, to include two literal backslashes in the string, you would use four backslashes in total.

Do not rely on unrecognized escaped characters as a method for including the backslash and the character following it.

Unicode character escapes using fewer than 4 hex digits, as in `\u040`, results in a backslash followed by the string `u040`. (This also causes a warning for the unrecognized escape.) To use a number of hex digits not equal to 4, use the longer `u{digits}` format.

### Comments

Comments must be hash comments (`# This is a comment`). Comments should explain the why, not the how, of your code.

Do not use `/* */` comments in Puppet code.

Good:  

```json
# Configures NTP
file { '/etc/ntp.conf': ... }
```

Bad:

```json
/* Creates file /etc/ntp.conf */
file { '/etc/ntp.conf': ... }
```

**Note:** Include documentation comments for Puppet Strings for each of your classes, defined types, functions, and resource types and providers. If used, documentation comments precede the name of the element. For documentation recommendations, see the Modules section of this guide.

### Functions

Avoid the `inline_template()` and `inline_epp()` functions for templates of more than one line, because these functions don’t permit template validation. Instead, use the `template()` and `epp()` functions to read a template from the module. This method allows for syntax validation.

You should avoid using calls to Hiera functions in modules meant for public consumption, because not all users have implemented Hiera. Instead, we recommend using parameters that can be overridden with Hiera.

### Improving readability when chaining functions

In most cases, especially if blocks are short, we recommend keeping functions on the same line. If you have a particularly long chain of operations or block that you find difficult to read, you can break it up on multiples lines to improve readability. As long as your formatting is consistent throughout the chain, it is up to your own judgment.

For example, this:

```json
$foodgroups.fruit.vegetables
```

Is better than this:

```json
   $foodgroups
           .fruit
           .vegetables
```

But, this:

```json
$foods = {
 "avocado"    => "fruit",
 "eggplant"   => "vegetable",
 "strawberry" => "fruit",
 "raspberry"  => "fruit",
}
 
$berries = $foods.filter |$name, $kind| {
 # Choose only fruits
 $kind == "fruit"
}.map |$name, $kind| {
 # Return array of capitalized fruits
 String($name, "%c")
}.filter |$fruit| {
 # Only keep fruits named "berry"
 $fruit =~ /berry$/
}
```

Is better than this:

```json
$foods = {
 "avocado"    => "fruit",
 "eggplant"   => "vegetable",
 "strawberry" => "fruit",
 "raspberry"  => "fruit",
}
 
$berries = $foods.filter |$name, $kind| { $kind == "fruit" }.map |$name, $kind| { String($name, "%c") }.filter |$fruit| { $fruit =~ /berry$/ }
```

**Related information**

- [Modules](https://puppet.com/docs/puppet/7.3/style_guide.html#style_guide_modules)

## Resources 

Resources are the fundamental unit for modeling system configurations. Resource declarations have a lot of possible features, so your code's readability is crucial.

### Resource names

All resource names or titles must be quoted. If you are using an array of titles you must quote each title in the array, but cannot quote the array itself.

Good:

```json
package { 'openssh': ensure => present }
```

Bad:

```json
package { openssh: ensure => present }
```

These quoting requirements do not apply to expressions that evaluate to strings.

### Arrow alignment

To align hash rockets (`=>`) in a resource's attribute/value list or in a nested block, place the hash rocket one space ahead of the longest attribute name. Indent the nested block by two spaces, and place each attribute on a separate line. Declare very short or single purpose resource declarations on a single line.

Good:

```json
exec { 'hambone':
  path => '/usr/bin',
  cwd  => '/tmp',
}

exec { 'test':
  subscribe   => File['/etc/test'],
  refreshonly => true,
}

myresource { 'test':
  ensure => present,
  myhash => {
    'myhash_key1' => 'value1',
    'key2'        => 'value2',
  },
}

notify { 'warning': message => 'This is an example warning' }
```

Bad:

```json
exec { 'hambone':
path  => '/usr/bin',
cwd => '/tmp',
}

file { "/path/to/my-filename.txt":
  ensure => file, mode => $mode, owner => $owner, group => $group,
  source => 'puppet:///modules/my-module/productions/my-filename.txt'
}
```

### Attribute ordering

If a resource declaration includes an `ensure` attribute, it should be the first attribute specified so that a user can quickly see if the resource is being created or deleted.

Good:

```json
file { '/tmp/readme.txt':
  ensure => file,
  owner  => '0',
  group  => '0',
  mode   => '0644',
}
```

When using the special attribute `*` (asterisk or splat character) in addition to other attributes, splat should be ordered last so that it is easy to see. You may not include multiple splats in the same body.

Good:

```json
$file_ownership = {
  'owner' => 'root',
  'group' => 'wheel',
  'mode'  => '0644',
}

file { '/etc/passwd':
  ensure => file,
  *      => $file_ownership,
}
```

### Resource arrangement

Within a manifest, resources should be grouped by logical relationship to each other, rather than by resource type.

Good:

```json
file { '/tmp/dir':
  ensure => directory,
}

file { '/tmp/dir/a':
  content => 'a',
}

file { '/tmp/dir2':
  ensure => directory,
}

file { '/tmp/dir2/b':
  content => 'b',
}
```

Bad:

```json
file { '/tmp/dir':
  ensure => directory,
}

file { '/tmp/dir2':
  ensure => directory,
}

file { '/tmp/dir/a':
  content => 'a',
}

file { '/tmp/dir2/b':
  content => 'b',
}
```

Use semicolon-separated multiple resource bodies only in conjunction with a local default body.

Good:

```json
$defaults = { < hash of defaults > }

file {
  default: 
    * => $defaults,;

  '/tmp/testfile':
    content => 'content of the test file',
}
```

Good: Repeated pattern with defaults:

```json
$defaults = { < hash of defaults > }

file {
  default: 
    * => $defaults,;

  '/tmp/motd':
    content => 'message of the day',;

  '/tmp/motd_tomorrow':
    content => 'tomorrows message of the day',;
}
```

Bad: Unrelated resources grouped:

```json
file {
  '/tmp/testfile':
    owner    => 'admin',
    mode     => '0644',
    contents => 'this is the content',;

  '/opt/myapp':
    owner  => 'myapp-admin',
    mode   => '0644',
    source => 'puppet://<someurl>',;

  # etc
}
```

You cannot set any attribute more than one time for a given resource; if you try, Puppet raises a compilation error. This means:

- If you use a hash to set attributes for a resource, you cannot set a different, explicit value for any of those attributes. For example, if mode is present in the hash, you can’t also set `mode => "0644"` in that resource body.
- You can’t use the `*` attribute multiple times in one resource body, because `*` itself acts like an attribute.
- To use some attributes from a hash and override others, either use a hash to set per-expression defaults, or use the `+` (merging) operator to combine attributes from two hashes (with the right-hand hash overriding the left-hand one).

### Symbolic links

Declare symbolic links with an ensure value of `ensure => link`. To inform the user that you are creating a link, specify a value for the `target` attribute.

Good:

```json
file { '/var/log/syslog':
  ensure => link,
  target => '/var/log/messages',
}
```

Bad:

```json
file { '/var/log/syslog':
  ensure => '/var/log/messages',
}
```

### File modes

- POSIX numeric notation must be represented as 4 digits.
- POSIX symbolic notation must be a string.
- You should not use file mode with Windows; instead use the [acl module](https://forge.puppet.com/puppetlabs/acl).
- You should use numeric notation whenever possible.
- The file mode attribute should always be a quoted string or (unquoted) variable, never an integer.

Good:

```json
file { '/var/log/syslog':
  ensure => file,
  mode   => '0644',
}
```

Bad:

```json
file { '/var/log/syslog':
  ensure => present,
  mode   => 644,
}
```

### Multiple resources

Multiple resources declared in a single block should be used only when there is also a default set of options for the resource type.

Good:

```json
file {
  default:
    ensure => 'file',
    mode   => '0666',;

  '/owner':
    user => 'owner',;

  '/staff':
    user => 'staff',;
}
```

Good: Give the defaults a name if used several times: 

```json
$our_default_file_attributes = { 
  'ensure' => 'file', 
  'mode'   => '0666', 
}
 
file {
  default:
    * => $our_default_file_attributes,;

  '/owner':
    user => 'owner',;

  '/staff':
    user => 'staff',;
}
```

Good: Spell out 'magic' iteration:

```json
['/owner', '/staff'].each |$path| {
  file { $path:
    ensure => 'file',
  }
}
```

Good: Spell out 'magic' iteration: 

```json
$array_of_paths.each |$path| {
  file { $path:
    ensure => 'file',
  }
}
```

Bad:

```json
file {
  '/owner':
    ensure => 'file',
    user   => owner,
    mode   => '0666',;

  '/staff':
    ensure => 'file',
    user   => staff,
    mode   => '0774',;
}

file { ['/owner', '/staff']:
  ensure => 'file',
}
 
file { $array_of_paths:
  ensure => 'file',
}
```

### Legacy style defaults

Avoid legacy style defaults. If you do use them, they should occur only at top scope in your site manifest. This is because resource defaults propagate through dynamic scope, which can have unpredictable effects far away from where the default was declared.

Acceptable: `site.pp`:

```json
Package {
  provider => 'zypper',
}
```

Bad: `/etc/puppetlabs/puppet/modules/apache/manifests/init.pp`:

```json
File {
  owner => 'nobody',
  group => 'nogroup',
  mode  => '0600',
}

concat { $config_file_path:
  notify  => Class['Apache::Service'],
  require => Package['httpd'],
}
```

### Attribute alignment

Resource attributes must be uniformly indented in two spaces from the title.

Good:

```json
file { '/owner':
  ensure => 'file',
  owner  => 'root',
}
```

Bad: Too many levels of indentation:

```json
file { '/owner':
    ensure => 'file',
    owner  => 'root',
}
```

Bad: No indentation:

```json
file { '/owner':
ensure => 'file',
owner  => 'root',
}
```

Bad: Improper and non-uniform indentation:

```json
file { '/owner':
  ensure => 'file',
   owner => 'root',
}
```

Bad: Indented the wrong direction:

```json
  file { '/owner':
ensure => 'file',
owner  => 'root',
  }
```

For multiple bodies, each title should be on its own line, and be indented. You may align all arrows across the bodies, but arrow alignment is not required if alignment per body is more readable.

```json
file {
  default:
    * => $local_defaults,;
 
  '/owner':
    ensure => 'file',
    owner  => 'root',
}
```

### Defined resource types

Because defined resource types can have multiple instances, resource names must have a unique variable to avoid duplicate declarations.

Good: Template uses `$listen_addr_port`:

```json
define apache::listen {
  $listen_addr_port = $name

  concat::fragment { "Listen ${listen_addr_port}":
    ensure  => present,
    target  => $::apache::ports_file,
    content => template('apache/listen.erb'),
  }
}
```

Bad: Template uses `$name`:

```json
define apache::listen {

  concat::fragment { 'Listen port':
    ensure  => present,
    target  => $::apache::ports_file,
    content => template('apache/listen.erb'),
  }
}
```

## Classes and defined types 

Classes and defined types should follow scope and organization guidelines.

### Separate files

Put all classes and resource type definitions (defined types) as separate files in the `manifests` directory of the module. Each file in the manifest directory should contain nothing other than the class or resource type definition.

Good: `etc/puppetlabs/puppet/modules/apache/manifests/init.pp`:

```json
class apache { }
```

Good: `etc/puppetlabs/puppet/modules/apache/manifests/ssl.pp`:

```json
class apache::ssl { }
```

Good: `etc/puppetlabs/puppet/modules/apache/manifests/virtual_host.pp`:

```json
define apache::virtual_host () { }
```

Separating classes and defined types into separate files is functionally identical to declaring them in `init.pp`, but has the benefit of highlighting the structure of the module and making the function and structure more legible.

When a resource or include statement is placed outside of a class, node definition, or defined type, it is included in all catalogs. This can have undesired effects and is not always easy to detect.

Good: `manifests/init.pp`:

```json
# class ntp
class ntp {
  ntp::install
}
# end of file
```

Bad: `manifests/init.pp`:

```json
class ntp {
  #...
}
ntp::install
```

### Internal organization of classes and defined types

Structure classes and defined types to accomplish one task.

Documentation comments for Puppet Strings should be included for each class or defined type. If used, documentation comments must precede the name of the element. For complete documentation recommendations, see the Modules section.

Put the lines of code in the following order:

1. First line: Name of class or type.
2. Following lines, if applicable: Define parameters. Parameters should be [typed](https://puppet.com/docs/puppet/7.3/lang_data_type.html#lang_data_type).
3. Next lines: Includes and validation come after parameters are defined. Includes may come before or after validation, but should be grouped separately, with all includes and requires in one group and all validations in another. Validations should validate any parameters and fail catalog compilation if any parameters are invalid. See [puppetlabs-ntp](https://github.com/puppetlabs/puppetlabs-ntp/blob/3.3.0/manifests/init.pp#init) for an example.
4. Next lines, if applicable: Should declare local variables and perform variable munging.
5. Next lines: Should declare resource defaults.
6. Next lines: Should override resources if necessary.

The following example follows the recommended style.

In `init.pp`:

- The `myservice` class installs packages, ensures the state of `myservice`, and creates a tempfile with given content. If the tempfile contains digits, they are filtered out.

- `@param service_ensure` the wanted state of services.

- `@param package_list` the list of packages to install, at least one must be given, or an error of unsupported OS is raised.

- `@param tempfile_contents` the text to be included in the tempfile, all digits are filtered out if present.

  ```json
  class myservice (
    Enum['running', 'stopped'] $service_ensure,
    String                     $tempfile_contents,
    Optional[Array[String[1]]] $package_list = undef,
  ) {
  ```

- Rather than just saying that there was a type mismatch for `$package_list`, this example includes an additional assertion with an improved error message. The list can be "not given", or have an empty list of packages to install. An assertion is made that the list is an array of at least one String, and that the String is at least one character long.

  ```json
    assert_type(Array[String[1], 1], $package_list) |$expected, $actual| {
      fail("Module ${module_name} does not support ${facts['os']['name']} as the list of packages is of type ${actual}")
    }
  
    package { $package_list:
      ensure => present,
    }
  
    file { "/tmp/${variable}":
      ensure   => present,
      contents => regsubst($tempfile_contents, '\d', '', 'G'),
      owner    => '0',
      group    => '0',
      mode     => '0644',
    }
  
    service { 'myservice':
      ensure    => $service_ensure,
      hasstatus => true,
    }
   
    Package[$package_list] -> Service['myservice']
  }
  ```

In `hiera.yaml`: The default values can be merged if you want to extend with additional packages. If not, use `default_hierarchy` instead of `hierarchy`.

```json
---
version: 5
defaults:
  data_hash: yaml_data
 
hierarchy:
- name: 'Per Operating System'
  path: "os/%{os.name}.yaml"
- name: 'Common'
  path: 'common.yaml'
```

In `data/common.yaml`:

```json
myservice::service_ensure: running
```

In `data/os/centos.yaml`:

```json
myservice::package_list:
- 'myservice-centos-package'
```

### Public and private

Split your module into public and private classes and defined types where possible. Public classes or defined types should contain the parts of the module meant to be configured or customized by the user, while private classes should contain things you do not expect the user to change via parameters. Separating into public and private classes or defined types helps build reusable and readable code.

Help indicate to the user which classes are which by making sure all public classes have complete comments and denoting public and private classes in your documentation. Use the documentation tags “@api private” and “@api public” to make this clear. For complete documentation recommendations, see the Modules section.

### Chaining arrow syntax

Most of the time, use [relationship metaparameters](https://puppet.com/docs/puppet/7.3/lang_relationships.html#lang_relationships) rather than [chaining arrows](https://puppet.com/docs/puppet/7.3/lang_relationships.html#lang_relationships). When you have many [interdependent or order-specific items](https://github.com/puppetlabs/puppetlabs-mysql/blob/3.1.0/manifests/server.pp#server), chaining syntax may be used. A chain operator should appear on the same line as its right-hand operand. Chaining arrows must be used left to right.

Good: Points left to right:

```json
Package['httpd'] -> Service['httpd']
```

Good: On the line of the right-hand operand:

```json
Package['httpd']
-> Service['httpd']
```

Bad: Arrows are not all pointing to the right:

```json
Service['httpd'] <- Package['httpd']
```

Bad: Must be on the right-hand operand's line:

```json
Package['httpd'] ->
Service['httpd']
```

### Nested classes or defined types

Don't define classes and defined resource types within other classes or defined types. Declare them as close to node scope as possible. If you have a class or defined type which requires another class or defined type, put graceful failures in place if those required classes or defined types are not declared elsewhere.

Bad:

```json
class apache {
  class ssl { ... }
}
```

Bad:

```json
class apache {
  define config() { ... }
}
```

### Display order of parameters

In parameterized class and defined resource type definitions, you can list required parameters before optional parameters (that is, parameters with defaults). Required parameters are parameters that are not set to anything, including undef. For example, parameters such as passwords or IP addresses might not have reasonable default values.

You can also group related parameters, order them alphabetically, or in the order you encounter them in the code. How you order parameters is personal preference.

Note that treating a parameter like a namevar and defaulting it to `$title` or `$name` does not make it a required parameter. It should still be listed following the order recommended here.

Good:

```json
class dhcp (
  $dnsdomain,
  $nameservers,
  $default_lease_time = 3600,
  $max_lease_time     = 86400,
) {}
```

Bad:

```json
class ntp (
  $options   = "iburst",
  $servers,
  $multicast = false,
) {}
```

### Parameter defaults

Adding default values to the parameters in classes and defined types makes your module easier to use. Use Hiera data in your module to set parameter defaults. See [Defining classes](https://puppet.com/docs/puppet/7.3/lang_classes.html#lang_class_define) for details about setting parameter defaults with Hiera data. In simple cases, you can also specify the default values directly in the class or defined type.

Be sure to declare the data type of parameters, as this provides automatic type assertions.

Good: Parameter defaults set in the class with references to Hiera data:

```json
class my_module (
  String $source,
  String $config,
) {
  # body of class
}
```

A `hiera.yaml` in the root of the module sets the hierarchy for assigning defaults:

```json
---
version: 5
default_hierarchy: 
- name: 'defaults'
  path: 'defaults.yaml'
  data_hash: yaml_data
```

And the file `data/defaults.yaml` specifies the actual default values:

```json
my_module::source: 'default source value'
my_module::config: 'default config value'
```

This example places the values in the defaults hierarchy, which means that the defaults are not merged into overriding values. To merge the defaults into those values, change the `default_hierarchy` to `hierarchy`.

If you are maintaining old code created prior to Puppet 4.9, you might encounter the use of a `params.pp` pattern. This pattern makes maintenance and troubleshooting difficult — refactor such code to use the Hiera data-in-modules pattern instead. See [Adding Hiera data to a module](https://puppet.com/docs/puppet/7.3/hiera_migrate.html#adding_hiera_data_module) for a detailed example showing how to replace `params.pp` with data.

Bad: `params.pp`

```json
class my_module ( 
  String $source = $my_module::params::source,
  String $config = $my_module::params::config,
) inherits my_module::params {
  # body of class
}
```

### Exported resources

Exported resources should be opt-in rather than opt-out. Your module should not be written to use exported resources to function by default unless it is expressly required.

When using exported resources, name the property `collect_exported`.

Exported resources should be exported and collected selectively using a [search expression](https://puppet.com/docs/puppet/7.3/lang_collectors.html), ideally allowing user-defined tags as parameters so tags can be used to selectively collect by environment or custom fact.

Good:

```json
define haproxy::frontend (
  $ports            = undef,
  $ipaddress        = [$::ipaddress],
  $bind             = undef,
  $mode             = undef,
  $collect_exported = false,
  $options          = {
    'option' => [
      'tcplog',
    ],
  },
) {
  # body of define
}
```

### Parameter indentation and alignment

Parameters to classes or defined types must be uniformly indented in two spaces from the title. The equals sign should be aligned.

Good:

```json
class profile::myclass (
  $var1    = 'default',
  $var2    = 'something else',
  $another = 'another default value',
) {

}
```

Good:

```json
class ntp (
  Boolean                        $broadcastclient = false,
  Optional[Stdlib::Absolutepath] $config_dir      = undef,
  Enum['running', 'stopped']     $service_ensure  = 'running',
  String                         $package_ensure  = 'present',
  # ...
) {
# ...
}
```

Bad: Too many level of indentation:

```json
class profile::myclass (
      $var1    = 'default',
      $var2    = 'something else',
      $another = 'another default value',
) {

}
```

Bad: No indentation:

```json
class profile::myclass (
$var1    = 'default',
$var2    = 'something else',
$another = 'another default value',
) {

}
```

Bad: Misaligned equals sign: json

```json
class profile::myclass (
  $var1 = 'default',
  $var2  = 'something else',
  $another = 'another default value',
) {

}
```

### Class inheritance

In addition to scope and organization, there are some additional guidelines for handling classes in your module.

Don't use class inheritance; use data binding instead of `params.pp` pattern. Inheritance is used only for `params.pp`, which is not recommended in Puppet 4.

If you use inheritance for maintaining older modules, do not use it across module namespaces. To satisfy cross-module dependencies in a more portable way, include statements or relationship declarations. Only use class inheritance for `myclass::params` parameter defaults. Accomplish other use cases by adding parameters or conditional logic.

Good:

```json
class ssh { ... }

class ssh::client inherits ssh { ... }

class ssh::server inherits ssh { ... }
```

Bad:

```json
class ssh inherits server { ... }

class ssh::client inherits workstation { ... }

class wordpress inherits apache { ... }
```

### Public modules

When declaring classes in publicly available modules, use `include`, `contain`, or `require` rather than class resource declaration. This avoids duplicate class declarations and vendor lock-in.

### **Type signatures** 

We recommend always using type signatures for class and defined type parameters. Keep the parameters and `=` signs aligned.

When dealing with very long type signatures, you can define type aliases and use short definitions. Good naming of aliases can also serve as documentation, making your code easier to read and understand. Or, if necessary, you can turn the 140 line character limit off. For more information on type signatures, see [the `Type` data type](https://puppet.com/docs/puppet/7.3/lang_data_type.html#lang_data_type).

**Related information**

- [Modules](https://puppet.com/docs/puppet/7.3/style_guide.html#style_guide_modules)

## Variables 

Reference variables in a clear, unambiguous way that is consistent with the Puppet style.

### Referencing facts

When referencing facts, prefer the `$facts` hash to plain top-scope variables (such as `$::operatingsystem`).

Although plain top-scope variables are easier to write, the `$facts` hash is clearer, easier to read, and distinguishes facts from other top-scope variables.

### Namespacing variables

When referencing top-scope variables other than facts, explicitly specify absolute namespaces for clarity and improved readability. This includes top-scope variables set by the node classifier and in the main manifest.

This is not necessary for:

- the `$facts` hash.
- the `$trusted` hash.
- the `$server_facts` hash.

These special variable names are protected; because you cannot create local variables with these names, they always refer to top-scope variables.

Good:

```json
$facts['operatingsystem']
```

Bad:

```json
$::operatingsystem
```

Very bad:

```json
$operatingsystem
```

### Variable format

When defining variables you must only use numbers, lowercase letters, and underscores. Do not use upper-case letters within a word, such as “CamelCase”, as it introduces inconsistency in style. You must not use dashes, as they are not syntactically valid.

Good:

```json
$server_facts
$total_number_of_entries
$error_count123
```

Bad:

```json
$serverFacts
$totalNumberOfEntries
$error-count123
```

## Conditionals 

Conditional statements should follow Puppet code guidelines.

### Simple resource declarations

Avoid mixing conditionals with resource declarations. When you use conditionals for data assignment, separate conditional code from the resource declarations.

**Good:**

```json
$file_mode = $facts['operatingsystem'] ? {
  'debian' => '0007',
  'redhat' => '0776',
   default => '0700',
}

file { '/tmp/readme.txt':
  ensure  => file,
  content => "Hello World\n",
  mode    => $file_mode,
}
```

**Bad:**

```json
file { '/tmp/readme.txt':
  ensure  => file,
  content => "Hello World\n",
  mode    => $facts['operatingsystem'] ? {
    'debian' => '0777',
    'redhat' => '0776',
    default  => '0700',
  }
}
```

### Defaults for case statements and selectors

Case statements must have default cases. If you want the default case to be "do nothing," you must include it as an explicit `default: {}` for clarity's sake.

Case and selector values must be enclosed in quotation marks.

Selectors should omit default selections only if you explicitly want catalog compilation to fail when no value matches.

**Good:**

```json
case $facts['operatingsystem'] {
  'centos': {
    $version = '1.2.3'
  }
  'ubuntu': {
    $version = '3.2.1'
  }
  default: {
    fail("Module ${module_name} is not supported on ${::operatingsystem}")
  }
}
```

When setting the default case, keep in mind that the default case should cause the catalog compilation to fail if the resulting behavior cannot be predicted on the platforms the module was built to be used on.

### Conditional statement alignment 

When using if/else statements, align in the following way:

```json
if $something {
  $var = 'hour'
} elsif $something_else {
  $var = 'minute'
} else {
  $var = 'second'
}
```

For more information on if/else statements, see [Conditional statements and expressions](https://puppet.com/docs/puppet/7.3/lang_conditional.html#lang_conditional).

## Modules 

Develop your module using consistent code and module structures to make it easier to update and maintain.

### Versioning

Your module must be versioned, and have metadata defined in the `metadata.json` file.

We recommend semantic versioning.

Semantic versioning, or [SemVer](http://semver.org/), means that in a version number given as x.y.z:

- An increase in 'x' indicates major changes: backwards incompatible changes or a complete rewrite.
- An increase in 'y' indicates minor changes: the non-breaking addition of new features.
- An increase in 'z' indicates a patch: non-breaking bug fixes.

### Module metadata

Every module must have metadata defined in the `metadata.json` file.

Your metadata should follow the following format:

```json
{
  "name": "examplecorp-mymodule",
  "version": "0.1.0",
  "author": "Pat",
  "license": "Apache-2.0",
  "summary": "A module for a thing",
  "source": "https://github.com/examplecorp/examplecorp-mymodule",
  "project_page": "https://github.com/examplecorp/examplecorp-mymodule",
  "issues_url": "https://github.com/examplecorp/examplecorp-mymodules/issues",
  "tags": ["things", "stuff"],
  "operatingsystem_support": [
    {
      "operatingsystem":"RedHat",
      "operatingsystemrelease": [
        "5.0",
        "6.0"
      ]
    },
    {
      "operatingsystem": "Ubuntu",
      "operatingsystemrelease": [ 
        "12.04",
        "10.04"
     ]
    }
  ],
  "dependencies": [
    { "name": "puppetlabs/stdlib", "version_requirement": ">= 3.2.0 <5.0.0" },
    { "name": "puppetlabs/firewall", "version_requirement": ">= 0.4.0 <5.0.0" },
  ]
}
```

For additional information regarding the `metadata.json` format, see [Adding module metadata in metadata.json](https://puppet.com/docs/puppet/7.3/modules_publishing.html#modules_publishing).

### Dependencies

Hard dependencies must be declared explicitly in your module’s metadata.json file.

Soft dependencies should be called out in the README.md, and must not be enforced as a hard requirement in your metadata.json. A soft dependency is a dependency that is only required in a specific set of use cases. For an example, see the [rabbitmq module](https://forge.puppet.com/puppetlabs/rabbitmq#module-dependencies).

Your hard dependency declarations should not be unbounded.

### README

Your module should have a README in `.md` (or `.markdown`) format. READMEs help users of your module get the full benefit of your work.

The [Puppet README template ](https://github.com/puppetlabs/pdk-templates/blob/master/moduleroot_init/README.md.erb)offers a basic format you can use. If you create modules with Puppet Development Kit or the `puppet module generate` command, the generated README includes the template. Using the .md/.markdown format allows your README to be parsed and displayed by Puppet Strings, GitHub, and the Puppet Forge.

You can find thorough, detailed information on writing a great README in [Documenting modules](https://puppet.com/docs/puppet/7.3/modules_documentation.html#modules_documentation), but in general your README should:

- Summarize what your module does.
- Note any setup requirements or limitations, such as "This module requires the `puppetlabs-apache` module and only works on Ubuntu."
- Note any part of a user’s system the module might impact (for example, “This module overwrites everything in `animportantfile.conf`.”).
- Describe  how to customize and configure the module.
- Include usage examples and code samples for the common use cases for your module.

### Documenting Puppet code

Use [Puppet Strings](https://github.com/puppetlabs/puppet-strings) code comments to document your Puppet classes, defined types, functions, and resource types and providers. Strings processes the README and comments from your code into HTML or JSON format documentation. This allows you and your users to generate detailed documentation for your module.

Include comments for each element (classes, functions, defined types, parameters, and so on) in your module. If used, comments must precede the code for that element. Comments should contain the following information, arranged in this order:

- A description giving an overview of what the element does.
- Any additional information about valid values that is not clear from the data type. For example, if the data type is `[String]`, but the value must specifically be a path.
- The default value, if any, for that element,

Multiline descriptions must be uniformly indented by at least one space:

```json
# @param config_epp Specifies a file to act as a EPP template for the config file.
#  Valid options: a path (absolute, or relative to the module path). Example value: 
#  'ntp/ntp.conf.epp'. A validation error is thrown if you supply both this param **and**
#  the `config_template` param.
```

If you use Strings to document your module, include information about Strings in the Reference section of your README so that your users know how to generate the documentation. See [Puppet Strings](https://github.com/puppetlabs/puppet-strings) documentation for details on usage, installation, and correctly writing documentation comments.

If you do not include Strings code comments, you should include a Reference section in your README with a complete list of all classes, types, providers, defined types, and parameters that the user can configure. Include a brief description, the valid options, and the default values (if any).

For example, this is a parameter for the `ntp` module’s `ntp` class: `package_ensure`:

```json
Data type: String.

Whether to install the NTP package, and what version to install. Values: 'present', 'latest', or a specific version number.

Default value: 'present'.
```

For more details and examples, see the [module documentation guide](https://puppet.com/docs/puppet/7.3/modules_documentation.html).

### CHANGELOG

Your module should include a change log file called `CHANGELOG.md` or `.markdown`. Your change log should:

- Have entries for each release.
- List bugfixes and features included in the release.
- Specifically call out backwards-incompatible changes.

### Examples

In the `/examples` directory, include example manifests that demonstrate major use cases for your module.

```json
modulepath/apache/examples/{usecase}.pp
```

The example manifest should provide a clear example of how to declare the class or defined resource type. It should also declare any classes required by the corresponding class to ensure `puppet apply` works in a limited, standalone manner.

### Testing

Use one or more of the following community tools for testing your code and style:

- [puppet-lint](http://puppet-lint.com/) tests your code for adherence to the style guidelines.
- [metadata-json-lint](https://github.com/voxpupuli/metadata-json-lint) tests your `metadata.json` for adherence to the style guidelines.
- For testing your module, we recommend rspec. [rspec-puppet](https://github.com/rodjek/rspec-puppet/#rspec-tests-for-your-puppet-manifests--modules) can help you write rspec tests for Puppet.

## Installing Puppet Server

**Sections**

- Before you begin
  - [Supported operating systems](https://puppet.com/docs/puppet/7.3/server/install_from_packages.html#supported-operating-systems)
  - [Java support](https://puppet.com/docs/puppet/7.3/server/install_from_packages.html#java-support)
- Install Puppet Server
  - [What to do next](https://puppet.com/docs/puppet/7.3/server/install_from_packages.html#what-to-do-next)
- [Running Puppet Server on a VM](https://puppet.com/docs/puppet/7.3/server/install_from_packages.html#running-puppet-server-on-a-vm)

Puppet Server is a required application that runs on the Java Virtual Machine (JVM). It controls the configuration information for one or more managed agent nodes.

> Note: If you have any issues with the steps below, submit these to our [bug tracker](https://tickets.puppet.com/browse/SERVER).

## Before you begin

Review the supported operating systems and make sure you have a supported version of Java.

### Supported operating systems

Puppet provides official packages that install Puppet Server and all of its prerequisites on x86_64 architectures for the following platforms:

- Red Hat Enterprise Linux 6, 7
- Debian 8 (Jessie), 9 (Stretch), 10 (Buster)
- Ubuntu 16.04 (Xenial), 18.04 (Bionic)
- SLES 12 SP1

> Note: Unlike Puppet agent, Puppet Server is not supported on MacOS.

### Java support

Puppet Server versions are tested against the following versions of Java:

| Puppet Server | Java                 |
| ------------- | -------------------- |
| 2.x           | 7, 8                 |
| 5.x           | 8                    |
| 6.0-6.5       | 8, 11 (experimental) |
| 6.6 and later | 8, 11                |

Some Java versions may work with other Puppet Server versions, but we do not test or support those cases. Community submitted patches for support greater than Java 11 are welcome. Both Java 8 and 11 are considered long-term support versions and are planned to be supported by upstream maintainers until 2022 or later.

> Note: Java 8 runtime packages do not exist in the standard repositories for Debian 8 (Jessie) or Ubuntu 18.04 (Bionic). To install Puppet Server on Jessie, [configure the `jessie-backports` repository](https://backports.debian.org/Instructions/). To install Puppet Server on Bionic, enable the [universe repository](https://help.ubuntu.com/community/Repositories/Ubuntu).

## Install Puppet Server

Puppet Server is configured to use 2 GB of RAM by default. If you're just testing an installation on a Virtual Machine, this much memory is not necessary. To change the memory allocation, see [Running Puppet Server on a VM](https://puppet.com/docs/puppet/7.3/server/install_from_packages.html#Running-Puppet-Server-on-a-VM).

1. [Enable the Puppet package repositories](https://puppet.com/docs/puppet/7.3/install_puppet.html#enable_the_puppet_platform_repository), if you haven't already done so.
2. Install the Puppet Server package by running one of the following commands.

Red Hat operating systems:

```bash
yum install puppetserver
```

Debian and Ubuntu:

```bash
apt-get install puppetserver
```

There is no `-` in the package name.

> Note: If you're upgrading, stop any existing `puppetserver` service by running `service <service_name> stop` or `systemctl stop <service_name>`.

1. Start the Puppet Server service:

```bash
sudo systemctl start puppetserver
```

1. To check you have installed the Puppet Server package correctnly, run the following command to check the version:

```bash
puppetserver -v
```

### What to do next

Now that Puppet Server is installed, move on to these next steps:

1. [Install a Puppet agent](https://puppet.com/docs/puppet/latest/install_agents.html)
2. [Install PuppetDB](https://puppet.com/docs/puppetdb/latest/install_via_module.html) (optional) ⁠— if you would like to to enable extra features, including enhanced queries and reports about your infrastructure.

## Running Puppet Server on a VM

By default, Puppet Server is configured to use 2GB of RAM. However, if you want to experiment with Puppet Server on a VM, you can safely allocate as little as 512MB of memory. To change the Puppet Server memory allocation, you can edit the init config file.

- For RHEL or CentOS, open `/etc/sysconfig/puppetserver`
- For Debian or Ubuntu, open `/etc/default/puppetserver`

1. In your settings, update the line:

   ```json
    # Modify this if you'd like to change the memory allocation, enable JMX, etc
    JAVA_ARGS="-Xms2g -Xmx2g"
   ```

   Replace 2g with the amount of memory you want to allocate to Puppet Server. For example, to allocate 1GB of memory, use `JAVA_ARGS="-Xms1g -Xmx1g"`; for 512MB, use `JAVA_ARGS="-Xms512m -Xmx512m"`.

   For more information about the recommended settings for the JVM, see [Oracle's docs on JVM tuning.](http://docs.oracle.com/cd/E15523_01/web.1111/e13814/jvm_tuning.htm)

2. Restart the `puppetserver` service after making any changes to this file.

# Deploying Puppet to Clients

## Puppet Nodes

When managing fleets of computers, we usually want **some rules to apply to every computer**, and **other rules to apply only to a subset of systems**. Let's say you're managing all your servers with Puppet. You might want to install a basic set of tools on all of them, but only install the packages for serving web pages in your web servers. And only install the packages for sending and receiving email in your mail servers. There's a bunch of different ways that we can do this. 

In an earlier video, we saw how to conditionally apply some rules using **facts from the machines**. Another way to apply different rules to different systems is to use **separate node definitions**. In Puppet terminology, a **node** is any system where we can run a **Puppet agent**. It could be a physical workstation, a server, a virtual machine, or even a network router, as long as it has a Puppet agent and can apply the given rules. So we can set up Puppet to give some basic rules to all the nodes, but then apply some specific rules to the nodes that we want to be different. Let's check out an example of how this could look. When setting up Puppet, we usually have a default node definition that lists the classes that should be included for all the nodes. For example, it could look something like this.

```json
node default {
    class { 'sudo': }
	class { 'ntp': 
		servers => ['ntp1.example.com', 'ntp2.example.com']
	}
}
```

Here, the default node is including two classes, the sudo class and the ntp class. For the ntp class, we're setting an additional servers parameter that lists the servers we can use to get the network time.

As you can see here, when defining a node, you can include a class by just using its name if there's no additional settings, or include the class and set additional parameters if necessary. All right, that's the default node, so it will apply to computers in the fleet by default. What if you want some settings to only apply to some specific nodes? 

You can do that by adding **more node definitions** that list the **classes** that you want them to include, like this. 

```json
node webserver.example.com {
    class { 'sudo': }
	class { 'ntp': 
		servers => ['ntp1.example.com', 'ntp2.example.com']
	}
	class { 'apache': }
}
```

We can see here that specific nodes in the fleet are identified by their **FQDNs**, or fully qualified domain names. In this case, we have the node definition for a host called `webserver.example.com`. For this node, we're including the same **sudo** and **ntp** classes as before, and we're adding the **apache** class on top. We're listing the same classes because the classes included in the default node definition are only applied to the nodes that don't have an explicit entry. 

In other words, when a node requests which rules it should apply, Puppet will look at the node definitions, figure out which one matches the node's FQDN, and then give only those rules. To avoid repeating the inclusion of all the common classes, we might define a base class that does the work of including all the classes that are common to all node types. 

Now, where's this information stored? **The node definitions** are typically stored in a file called `site.pp`, which isn't part of any module. Instead, it just defines what classes will be included for what nodes. This is another step towards helping us organize our code in a way that makes it easier to maintain. Up next, we'll look into the infrastructure used by Puppet to verify if a node really has the name that it claims to have.

## Puppet’s Certificate Infrastructure

We've called that a few times that in typical Puppet deployments, all managed machines and the fleet connect to a Puppet server. The client send their facts to the server, and the server then processes the manifests, generates the corresponding catalog, and sends it back to the clients who apply it locally. In our last video, we mentioned that we can apply different rules to different nodes depending on their **names**. 

The client send their name to the server when they connect, but how can the server **trust that a client is really who he claims to be**? It's a dangerous world out there. Well, this is a complex subject that touches on some important security concepts. We'll do a quick rundown here. If you're interested in learning more, you might want to check out the security course in the Google IT support professional certificate program led by my colleague, Gian, who explains it in more detail. Puppet uses **public key infrastructure, or PKI**, to establish secure connections between the server and the clients. 

There's a bunch of different types of public key technologies. The one used by Puppet is **secure sockets layer or SSL**. This is the same technology used for encrypting transmissions over HTTPS. The clients use this infrastructure to check the server's identity, and the server uses it to check the client's identity, and all communication is done over an encrypted channel that uses these identities so it can't be intercepted by other parties. So how does this work? Each machine involved has **a pair of keys** related to each other, a **private key** and a **public key**. The private key is secret, only known to that specific machine, the public key is shared with other machines involved. Machines can then use the standardized process to validate the identity of any other machine. The sender signs a message using the private key and the receiver validates the signature using the corresponding public key. Okay. But how do machines know which public keys to trust? This is where a **certificate authority, or CA** comes in. 

The CA verifies the identity of the machine and then creates a certificate stating that the public key goes with that machine. After that, other machines can rely on that certificate to know that they can **trust the public key**, since it means the machine's identity has been verified. Puppet comes with its **own certificate authority**, which can be used to create certificates for each clients. So you can use that one, or if your company already has a CA that validates the identity of the machines in your fleet, you can **integrate it with Puppet**, so you only validate the identities once. 

Now, let's assume you're using the baked-in certificate infrastructure and dive into how this process works. When a node **checks** into the Puppet master for the first time, it **requests the certificate**. The Puppet master looks at this request and if it can verify the nodes identity, it **creates a certificate for that node**. The system administrator can check the identity manually or use a process that does this automatically using additional information about the machines to verify their identity. When the agent node picks up this certificate, it knows it can trust the Puppet master, and the node can use the certificate from then on to identify itself when **requesting a catalog.** 

You might be wondering, why do we care so much about the identity of the nodes? There's a bunch of reasons. First, Puppet rules can sometimes include confidential information that you don't want to fall in the wrong hands. But even if none of the rules hold confidential info, you want to be sure that the machine you're setting up as your web server really is your web server and not a rogue machine that just claims to have the same name. All sorts of things could go wrong if random computers start popping up in your network with the wrong settings. If you're creating a test deployment to try out how Puppet rules get applied, and so you're only managing tests machines, you can configure Puppet to **automatically sign all requests**, but you should never do this for real computers being used by real users. Remember that it's better to be safe than sorry. So always take the time to authenticate your machines. When starting out with Puppet, it's common to use the **manual signing approach.** In this case, when the node connects to the master, it will generate a certificate request, which we'll go into a queue in the Puppet master machine. 

You'll then need to verify that the machine's identity is correct and the baked-in CA will issue the corresponding certificate. **If your fleet is large, this manual approach won't really work**. Instead, you'll want to write a script that verifies the identity of the machines automatically for you. One way to do this is by **copying a unique piece of information into the machines when they get provisioned** and then **use this pre-shared data as part of the certificate request.** That way, your script can verify that the machines are who they claim to be without involving any humans. Great, you now have a broad idea of the infrastructure that Puppet uses to identify the nodes when they connect to the master. Up next, we'll see what the typical Puppet setup using a separate Puppet server and client looks like in practice.

## Setting up Puppet Clients and Servers

We're now ready to see a Puppet deployment in action. We've already installed the Puppet master package on this computer, so we'll use it as the master. Since this is a test deployment to demonstrate Puppet, we'll configure it to automatically sign the certificate requests of the nodes we add. But remember, if we were deploying this to real computers, we'd have to **manually sign the requests or implement a proper validating script**. We'll do this by calling the Puppet command with the `config` parameter, and then saying that in this section master we want to set auto sign to true. 

```bash
sudo puppet config --section master set autosign true
```

All right. With that, we can connect to the client that we want to manage using Puppet. We'll connect using SSH to a machine called `webserver`. On this machine, we'll install the Puppet client which is shipped by the Puppet package.

```bash
sudo apt install puppet
```

Nice. We have the Puppet agent installed. Now we need to configure it to talk to the Puppet server that we're running on the other machine. To do that, we'll use Puppet config like before but this time we'll tell it that we want to set the server to `ubuntu.example.com`.

```bash
sudo puppet config set server ubuntu.example.com
```

Great. Now that we've configured the server, we can test the connection to the Puppet master by using the Puppet agent command passing dash v as before to get verbose output, and dash dash test to do a test run. 

```bash
sudo puppet agent -v --test
```

As usual, Puppet tells us everything it did. It first created an SSL key for the machine. It then read a bunch of information from the machine and used this to create a certificate request. The agent shows us the **fingerprint** of the certificate requested. If we were using manual signing, we could use this fingerprint to verify that the request and the server matches the one generated on the machine. The certificate was then generated on our puppet master. We don't see any entries for that because it happened on the other computer. But we see that this computer **received a certificate and stored it locally**. 

Once the certificate exchange completed, the agent retrieved all the information from the machine and sent it to the master. In exchange, it got back a catalog and applied it. The catalog applied almost immediately because we haven't actually configured any rules to be applied to our clients. We should go ahead and do that now. We'll go back to our Puppet master and create a couple of node definitions. As we called out, node definitions are stored in a manifest file called `site.pp`, which is stored **at the root of the nodes environment**. We'll talk more about environments in a later video. For now, we just need to know that our client is trying to access the production environment. So the file that we need to create will be located in `/etc/puppet/code/environments/production/manifests`, and it will be called `site.pp`.

In this file, we'll create a couple of node definitions. We want to install Apache in our web server, so we'll create a node definition for the web server with the Apache class and node parameters for now,and we'll also add a default node definition. We'll keep it empty for now. We can add more classes in the future. All right. With that, we have our very basic node definition. We can now save this and run the Puppet agent on our web server machine again.

```json
node webserver.example.com {
    class { 'apache': }
}
```

This time, the Puppet agent connected to the Puppet master and got a catalog that told it to install and configure the Apache package. This included setting up a bunch of different services. 

Up to now, we've been doing **manual runs** of the Puppet agent for testing purposes. Now that we know it's working fine, we want to keep Puppet running **automatically**. That way, if we make changes to the configuration, clients will automatically apply those changes without us having to do any manual steps. So to do that, we'll use the `systemctl` command, which lets us control the services that are enabled when the machine starts and those that are currently running. So we'll first tell the systemctl to enable the puppet service so that the agent gets started whenever the machine reboots, and then we'll tell systemctl to start the puppet service so that it starts running. Last step, we'll ask systemctl for the status of the Puppet service to check that it's actually running. 

```bash
sudo systemctl enable puppet
sudo systemctl start puppet
sudo systemctl status puppet
```

Awesome. That worked. The Puppet agent will keep regularly checking in with the master and ask if there are any changes that need to be applied to the machine. With that, you've seen Puppet in action using the server client model. We use the configuration we set in the Puppet master to manage the installation and configuration of software in our web server, and we set up the Puppet agent in the web server to keep running so that the configuration stays up to date. We've only seen the very basics of how to configure Puppet, but this can already give you an idea of how powerful configuration management can be. Pretty exciting, right? Up next, we've gathered more info on how to do the client-server set-up and after that, a quick quiz to check that everything is still making sense.

# Puppet SSL explained

The [puppet-users](http://groups.google.com/group/puppet-users) or [#puppet freenode irc channel](http://projects.puppetlabs.com/projects/puppet/wiki/IRC_Channel) is full of questions or people struggling about the [puppet SSL PKI](http://projects.puppetlabs.com/projects/puppet/wiki/Certificates_And_Security). To my despair, there are also people wanting to completely get rid of any security.

While I don’t advocate the *live happy, live without security* motto of some puppet users (and I really think a corporate firewall is only one layer of defense among many, not the ultimate one), I hope this blog post will help them shoot themselves in their foot :)

I really think SSL or the X509 PKI is simple once you grasped its underlying concept. If you want to know more about SSL, I really think everybody should read Eric Rescola’s excellent “[SSL and TLS: Designing and Building Secure Systems](http://www.amazon.com/dp/0201615983)”.

I myself had to deal with SSL internals and X509 PKI while I implemented a java secured network protocol in a previous life, including a cryptographic library.

## Purpose of Puppet SSL PKI

The current puppet security layer has 3 aims:

1. authenticate any node to the master (so that no rogue node can get a catalog from your master)
2. authenticate the master on any node (so that your nodes are not tricked into getting a catalog from a rogue master).
3. prevent communication eavesdropping between master and nodes (so that no rogue users can grab configuration secrets by listening to your traffic, which is useful in the cloud)

## A notion of PKI

PKI means: [Public Key Infrastructure](http://en.wikipedia.org/wiki/Public_key_infrastructure). But whats this?

A PKI is a framework of computer security that allows authentication of individual components based on public key cryptography. The most known system is the [x509](http://en.wikipedia.org/wiki/X.509) one which is used to protect our current web.

A public key cryptographic system works like this:

- every components of the system has a secret key (known as the *private key*) and a *public key* (this one can be shared with other participant of the system). The public and private keys are usually bound by a cryptographic algorithm.
- authentication of any component is done with a simple process: a component signs a message with its own private key. The receiver can authenticate the message (ie know the message comes from the original component) by validating the signature. To do this, only the public key is needed.

There are different public/private key pair cryptosystem, the most known ones are RSA, DSA or those based on Elliptic Curve cryptography.

Usually it is not good that all participants of the system must know each other to communicate. So most of the current PKI system use a hierarchical validation system, where all the participant in the system must only know one of the parent in the hierarchy to be able to validate each others.

## X509 PKI

X509 is an ITU-T standard of a PKI. It is the base of the SSL protocol authentication that puppet use. This standard specifies certificates, certificate revocation list, authority and so on…

A given X509 certificate contains several information like those:

- Serial number (which is unique for a given CA)
- Issuer (who created this certificate, in puppet this is the CA)
- Subject (who this certificate represents, in puppet this is the node certname or fqdn)
- Validity (valid from, expiration date)
- Public key (and what kind of public key algorithm has been used)
- Various extensions (usually what this certificate can be used for,…)

You can check [RFC1422](http://www.ietf.org/rfc/rfc1422) for more details.

The certificate is usually the [DER encoding](http://en.wikipedia.org/wiki/Distinguished_Encoding_Rules) of the [ASN.1](http://en.wikipedia.org/wiki/Abstract_Syntax_Notation_One) representation of those informations, and is usually stored as [PEM](http://en.wikipedia.org/wiki/Privacy_Enhanced_Mail) for consumption.

A given X509 certificate is signed by what we call a [Certificate Authority](http://en.wikipedia.org/wiki/Certificate_authority) (CA for short). A CA is an infrastructure that can sign new certificates. Anyone sharing the public key of the CA can validate that a given certificate has been validated by the CA.

Usually X509 certificate embeds a RSA public key with an exponent of 0x100001 (see below).  Along with a certificate, you need a private key (usually also PEM-encoded).

So basically the X509 system works with the following principle: CA are using their own private keys to sign components certificates, it is the CA role to sign only trusted component certificates. The trust is usually established out-of-bound of the signing request.

Then every component in the system knows the CA certificate (ie public key). If one component gets a message from another component, it checks the attached message signature with the CA certificate. If that validates, then the component is authenticated. Of course the component should also check the certificate validity, if the certificate has been revoked (from OCSP or a given CRL), and finally that the certificate subject matches who the component pretends to be (usually this is an hostname validation against some part of the certificate *Subject*)

## RSA system

Most of X509 certificate are based on the RSA cryptosystem, so let’s see what it is.

The RSA cryptosystem is a public key pair system that works like this:

### Key Generation

To generate a RSA key, we chose two prime number *p* and *q*.

We compute *n=pq*. We call *n* the modulus.

We compute *φ*(*pq*) = (*p* − 1)(*q* − 1).

We chose e so that e>1 and e<*φ*(*pq*) (e and *φ*(*pq*) must be coprime). *e* is called the exponent. It usually is 0x10001 because it greatly simplifies the computations later (and you know what I mean if you already implemented this :)).

Finally we compute *d=e^-1 mod((p-1)(q-1))*. This will be our secret key. Note that it is not possible to get d from only e (and since p and q are never kept after the computation this works).

In the end:

- *e* and *n* form the public key
- *d* is our private key

### Encryption

So the usual actors when describing cryptosystems are Alice and Bob. Let’s use them.

Alice wants to send a message *M* to Bob. Alice knows Bob’s public key *(e,n)*. She transform *M* in a number < *n _(this is called padding) that we’ll call _m*, then she computes: _c = m^e . mod(n) _

### Decryption

When Bob wants to decrypt the message, he computes with his private key *d*: *m = c^d . mod(n)*

### Signing message

Now if Alice wants to sign a message to Bob. She first computes a hash of her message called *H*, then she computes: _s = H^(d mod n). _So she used her own private key. She sends both the message and the signature.

Bob, then gets the message computes _H _and computes _h’ = H^(e mod n) _with Alice’s public key. If _h’ = h, _then only Alice could have sent it.

### Security

What makes this scheme work is the fundamental that finding p and q from n is a hard problem (understand for big values of n, it would take far longer than the validity of the message). This operation is called factorization. Current certificate are numbers containing  2048 bits, which roughly makes a 617 digits number to factor.

### Want to know more?

Then there are a couple of books really worth reading:

- [Applied Cryptography](http://amazon.com/dp/0471117099) - Bruce Schneier
- [Handbook of Applied Cryptography](http://amazon.com/dp/0849385237) - Alfred Menezes, Paul van Oorschot, Scott Vanstone

## How does this fit in SSL?

So SSL (which BTW means Secure Socket Layer) and now TLS (SSL successor) is a protocol that aims to provide security of communications between two peers. It is above the transport protocol (usually TCP/IP) in the OSI model. It does this by using [symmetric encryption](http://en.wikipedia.org/wiki/Symmetric-key_algorithm) and [message authentication code](http://en.wikipedia.org/wiki/Message_authentication_code) (MAC for short). The standard is (now) described in [RFC5246](http://tools.ietf.org/html/rfc5246).

It works by first performing an handshake between peers. Then all the remaining communications are encrypted and tamperproof.

This handshake contains several phases (some are optional):

1. Client and server finds the best encryption scheme and MAC from the common list supported by both the server and the clients (in fact the server choses).
2. The server then sends its certificate and any intermediate CA that the client might need
3. The server may ask for the client certificate. The client may send its certificate.
4. Both peers may validate those certificates (against a common CA, from the CRL, etc…)
5. They then generate the session keys. The client generates a random number, encrypts it with the server public key. Only the server can decrypt it. From this random number, both peers generate the symmetric key that will be used for encryption and decryption.
6. The client may send a signed message of the previous handshake message. This way the server can verify the client knows his private key (this is the client validation). This phase is optional.

After that, each message is encrypted with the generated session keys using a symmetric cipher, and validated with an agreed on MAC. Usual symmetric ciphers range from RC4 to AES. A symmetric cipher is used because those are usually way faster than any asymmetric systems.

## Application to Puppet

Puppet defines it’s own Certificate Authority that is usually running on the master (it is possible to run a CA only server, for instance if you have more than one master).

This CA can be used to:

- generate new certificate for a given client out-of-bound
- sign a new node that just sent his Certificate Signing Request
- revoke any signed certificate
- display certificate fingerprints

What is important to understand is the following:

- Every node knows the CA certificate. *This allows to check the validity of the master from a node*
- *The master doesn’t need the node certificate*, since it’s sent by the client when connecting. It just need to make sure the client knows the private key and this certificate has been signed by the master CA.

It is also important to understand that when your master is running behind an Apache proxy (for Passenger setups) or Nginx proxy (ie some mongrel setups):

- The proxy is the SSL endpoint. It does all the validation and authentication of the node.
- Traffic between the proxy and the master happens in clear
- The master knows the client has been authenticated because the proxy adds an HTTP header that says so (usually _X-Client-Verify _for Apache/Passenger).

When running with webrick, webrick runs inside the puppetmaster process and does all this internally. Webrick tells the master internally if the node is authenticated or not.

When the master starts for the 1st time, it generates its own CA certificate and private key, initializes the CRL and generates a special certificate which I will call the *server certificate*. This certificate will be the one used in the SSL/TLS communication as the server certificate that is later sent to the client. This certificate subject will be the current master FQDN. If your master is also a client of itself (ie it runs a puppet agent), I recommend using this certificate as the client certificate.

The more important thing is that this server certificate advertises the following extension:

```
X509v3 Subject Alternative Name:
                DNS:puppet, DNS:$fqdn, DNS:puppet.$domain
```

What this means is that this certificate will validate if the connection endpoint using it has any name matching puppet, the current fqdn or puppet in the current domain.

By default a client tries to connect to the “*puppet*” host (this can be changed with –server which I don’t recommend and is usually the source of most SSL trouble).

If your DNS system is well behaving, the client will connect to *puppet.$domain*. If your DNS contains a CNAME for puppet to your *real master fqdn*, then when the client will validate the server certificate it will succeed because it will compare “puppet” to one of those DNS: entries in the aforementioned certificate extension. BTW, if you need to change this list, you can use the –certdnsname option (note: this can be done afterward, but requires to re-generate the server certificate).

The whole client process is the following:

1. if the client runs for the 1st time, it generates a [Certificate Signing Request](http://en.wikipedia.org/wiki/Certificate_signing_request) and a private key. The former is an x509 certificate that is self-signed.
2. the client connects to the master (at this time the client is not authenticated) and sends its CSR, it will also receives the CA certificate and the CRL in return.
3. the master stores locally the CSR
4. the administrator checks the CSR and can eventually sign it (this process can be automated with autosigning). I strongly suggest verifying certificate fingerprint at this stage.
5. the client is then waiting for his signed certificate, which the master ultimately sends
6. All next communications will use this client certificate. Both the master and client will authenticate each others by virtue of sharing the same CA.

## Tips and Tricks

### Troubleshooting SSL

#### Certificate content

First you can check any certificate content with this:

```bash
openssl x509 -text -in /var/lib/puppet/ssl/certs/puppet.pem


Certificate:    Data:
        Version: 3 (0x2)
        Serial Number: 2 (0x2)
        Signature Algorithm: sha1WithRSAEncryption
        Issuer: CN=Puppet CA: master.domain.com
        Validity
            Not Before: Nov 13 14:29:23 2010 GMT
            Not After : Nov 12 14:29:23 2015 GMT
        Subject: CN=server.domain.com
        Subject Public Key Info:
            Public Key Algorithm: rsaEncryption
            RSA Public Key: (1024 bit)
                Modulus (1024 bit):
                    00:be:11:7d:0e:32:4d:c4:da:40:7d:7a:17:30:2c:
                    00:c4:c5:a8:c7:91:31:21:71:50:ef:07:77:79:1a:
                    07:d6:57:d4:4d:e0:01:b3:78:73:ec:84:dd:71:30:
                    62:cd:e5:26:fd:54:46:da:e3:3b:be:3b:05:9a:87:
                    44:9a:5e:b4:41:b7:15:de:20:1d:9d:26:50:44:bc:
                    e6:64:67:d1:93:ee:3f:20:a6:86:0e:11:5c:de:b1:
                    da:e5:fb:b5:f1:e1:e9:2e:14:39:47:f2:b8:a4:40:
                    84:89:18:86:5a:df:3b:68:a4:64:7f:a9:99:93:60:
                    29:e8:fe:d5:a3:e0:6e:ba:4b
                Exponent: 65537 (0x10001)
        X509v3 extensions:
            Netscape Comment: 
                Puppet Ruby/OpenSSL Generated Certificate
            X509v3 Basic Constraints: critical
                CA:FALSE
            X509v3 Subject Key Identifier: 
                F4:FA:5A:03:EF:D5:0C:C3:B6:A0:35:47:D1:49:98:74:D4:09:B4:A9
            X509v3 Key Usage: 
                Digital Signature, Key Encipherment
            X509v3 Extended Key Usage: 
                TLS Web Server Authentication, TLS Web Client Authentication, E-mail Protection
            X509v3 Subject Alternative Name: 
                DNS:puppet, DNS:puppet.domain.com
    Signature Algorithm: sha1WithRSAEncryption
        70:e3:7c:04:c4:e1:66:07:db:5c:58:d9:64:bb:0a:e7:55:4c:
        93:9d:61:0a:2a:a6:3f:de:aa:98:a9:e5:40:45:40:87:62:78:
        d3:af:a7:01:a7:b9:ca:ee:b2:44:ff:02:be:8b:54:aa:65:45:
        0b:94:2a:56:fa:1d:67:fe:cd:52:09:29:89:bc:2f:4f:6b:30:
        cb:de:6a:01:35:43:74:1e:d6:14:2e:f0:43:ac:38:e9:7c:ec:
        2c:e6:b8:50:8c:15:07:2f:72:35:82:7f:ad:9c:3a:4f:a7:5c:
        d6:e8:87:f9:19:20:1f:8f:2e:2e:28:4c:9f:ea:d7:26:5e:c5:
        18:57
```

#### Simulate a SSL connection

You can know more information about a SSL error by simulating a client connection. Log in the trouble node and:

```shell
# this simulates how a puppet agent will connect
openssl s_client -host puppet -port 8140 -cert /path/to/ssl/certs/node.domain.com.pem -key /path/to/ssl/private_keys/node.domain.com.pem -CAfile /path/to/ssl/certs/ca.pem


# outputs:


CONNECTED(00000004)
depth=1 /CN=Puppet CA: master.domain.com
verify return:1
depth=0 /CN=macbook.local
verify return:1
---
Certificate chain
 0 s:/CN=macbook.local
   i:/CN=Puppet CA: master.domain.com
 1 s:/CN=Puppet CA: master.domain.com
   i:/CN=Puppet CA: master.domain.com
---
Server certificate
-----BEGIN CERTIFICATE-----
MIICgjCCAeugAwIBAgIBAjANBgkqhkiG9w0BAQUFADAjMSEwHwYDVQQDDBhQdXBw
ZXQgQ0E6IG1hY2Jvb2subG9jYWwwHhcNMTAxMTEzMTQyOTIzWhcNMTUxMTEyMTQy
OTIzWjAYMRYwFAYDVQQDDA1tYWNib29rLmxvY2FsMIGfMA0GCSqGSIb3DQEBAQUA
A4GNADCBiQKBgQC+EX0OMk3E2kB9ehcwLADExajHkTEhcVDvB3d5GgfWV9RN4AGz
eHPshN1xMGLN5Sb9VEba4zu+OwWah0SaXrRBtxXeIB2dJlBEvOZkZ9GT7j8gpoYO
EVzesdrl+7Xx4ekuFDlH8rikQISJGIZa3ztopGR/qZmTYCno/tWj4G66SwIDAQAB
o4HQMIHNMDgGCWCGSAGG+EIBDQQrFilQdXBwZXQgUnVieS9PcGVuU1NMIEdlbmVy
YXRlZCBDZXJ0aWZpY2F0ZTAMBgNVHRMBAf8EAjAAMB0GA1UdDgQWBBT0+loD79UM
w7agNUfRSZh01Am0qTALBgNVHQ8EBAMCBaAwJwYDVR0lBCAwHgYIKwYBBQUHAwEG
CCsGAQUFBwMCBggrBgEFBQcDBDAuBgNVHREEJzAlggZwdXBwZXSCDW1hY2Jvb2su
bG9jYWyCDHB1cHBldC5sb2NhbDANBgkqhkiG9w0BAQUFAAOBgQBw43wExOFmB9tc
WNlkuwrnVUyTnWEKKqY/3qqYqeVARUCHYnjTr6cBp7nK7rJE/wK+i1SqZUULlCpW
+h1n/s1SCSmJvC9PazDL3moBNUN0HtYULvBDrDjpfOws5rhQjBUHL3I1gn+tnDpP
p1zW6If5GSAfjy4uKEyf6tcmXsUYVw==
-----END CERTIFICATE-----
subject=/CN=puppet.domain.com
issuer=/CN=Puppet CA: master.domain.com
---
No client certificate CA names sent
---
SSL handshake has read 1794 bytes and written 1656 bytes
---
New, TLSv1/SSLv3, Cipher is DHE-RSA-AES256-SHA
Server public key is 1024 bit
Compression: NONE
Expansion: NONE
SSL-Session:
    Protocol  : TLSv1
    Cipher    : DHE-RSA-AES256-SHA
    Session-ID: DB29414CCB1E094675238999C8C00AF3173F441030C44A67D773648E83D76F75
    Session-ID-ctx: 
    Master-Key: 92430ADC9E52BA22023D5E37DED7D9A274B9E5E461CB46C47F1E9B14BE1956B7615FADC2319D9DA091784EC91ED777B3
    Key-Arg   : None
    Start Time: 1289747911
    Timeout   : 300 (sec)
    Verify return code: 0 (ok)
---
```

Check the last line of the report, it should say “Verify return code: 0 (ok)” if both the server and client authenticated each others. Check also the various information bits to see what certificate were sent. In case of error, you can learn about the failure by looking that the verification error message.

#### ssldump

Using [ssldump](http://www.rtfm.com/ssldump/) or [wireshark](http://www.wireshark.org/) you can also learn more about ssl issues. For this to work, it is usually needed to force the cipher to use a simple cipher like RC4 (and also ssldump needs to know the private keys if you want it to decrypt the application data).

#### Some known issues

Also, in case of SSL troubles make sure your master isn’t using a different $ssldir than what you are thinking. If that happens, it’s possible your master is using a different dir and has regenerated its CA. If that happens no one node can connect to it anymore. This can happen if you upgrade a master from gem when it was installed first with a package (or the reverse).

If you regenerate a host, but forgot to remove its cert from the CA (with puppetca –clean), the master will refuse to sign it. If for any reason you need to fully re-install a given node without changing its fqdn, either use the previous certificate or clean this node certificate (which will automatically revoke the certificate for your own security).

#### Looking to the CRL content:

```shell
# it is possible to get the content of the CRL:
openssl crl -text -in /var/lib/puppet/ssl/ca/ca_crl.pem 


Certificate Revocation List (CRL):
        Version 2 (0x1)
        Signature Algorithm: sha1WithRSAEncryption
        Issuer: /CN=Puppet CA: master.domain.com
        Last Update: Nov 14 15:47:42 2010 GMT
        Next Update: Nov 13 15:47:42 2015 GMT
        CRL extensions:
            X509v3 CRL Number: 
                1
Revoked Certificates:
    Serial Number: 03
        Revocation Date: Nov 14 15:47:42 2010 GMT
        CRL entry extensions:
            X509v3 CRL Reason Code: 
                Key Compromise
    Signature Algorithm: sha1WithRSAEncryption
        a2:cb:cf:d6:95:34:5d:7e:aa:95:cf:cd:7f:ea:1a:da:b0:f4:
        15:1f:df:03:28:64:b7:e0:a9:2d:53:df:b7:25:05:64:3e:15:
        08:2a:02:6d:42:7f:ad:37:f1:8f:72:66:f5:ed:f0:0b:59:d2:
        9f:16:77:18:eb:dc:dd:2e:f0:c4:ea:80:51:cf:35:43:ed:cd:
        7d:64:c0:43:dc:85:13:0f:5f:e2:88:78:a9:fc:bf:c3:a5:c6:
        e2:0e:8e:9d:95:1e:19:63:03:bb:26:89:9c:52:78:d6:a0:79:
        82:1d:2c:44:15:7d:75:42:52:4e:6a:a8:e5:d7:40:c5:b8:4a:
        24:d2
```

Notice how the certificate serial number 3 has been revoked.

### Fingerprinting

Since puppet 2.6.0, it is possible to fingerprint certificates. If you manually sign your node, it is important to make sure you are signing the correct node and not a rogue system trying to pretend it is some genuine node. To do this you can get the certificate fingerprint of a node by running puppet agent –fingerprint, and when listing on the master the various CSR, you can make sure both fingerprint match.

```shell
# on the node
puppet agent --test --fingerprint               
notice: 14:45:FD:59:F2:CC:83:62:4C:4A:D2:2A:37:4F:12:96


# on the master
puppetca --list node.domain.com --fingerprint
node.domain.com 14:45:FD:59:F2:CC:83:62:4C:4A:D2:2A:37:4F:12:96
```

### Dirty Trick

Earlier I was saying that when running with a reverse proxy in front of Puppet, this one is the SSL endpoint and it propagates the authentication status to Puppet.

**I strongly don’t recommend implementing the following. This will compromise your setup security.**

This can be used to severely remove Puppet security for instance you can:

- make so that every nodes are authenticated for the server by always returning the correct header
- make so that nodes are authenticated based on their IP addresses or fqdn

You can even combine this with a mono-certificate deployment. The idea is that every node share the same certificate. This can be useful when you need to provision tons of short-lived nodes. Just generate on your master a certificate:

```shell
# Generate a certificate and private key to be used for a node
puppetca --generate node.domain.com


notice: node.domain.com has a waiting certificate requestnotice: Signed certificate request for node.domain.com
notice: Removing file Puppet::SSL::CertificateRequest node.domain.com at '/tmp/master/ssl/ca/requests/node.domain.com.pem'
notice: Removing file Puppet::SSL::CertificateRequest node.domain.com at '/tmp/master/ssl/certificate_requests/node.domain.com.pem'
```

You can then use those generated certificate (which will end up in /var/lib/puppet/ssl/certs and /var/lib/puppet/private_keys) in a pre-canned $ssldir, provided you rename it to the local fqdn (or symlink it). Since this certificate is already signed by the CA, it is valid. The only remaining issue is that the master will serve the catalog of this certificate certname. I proposed a patch to fix this, this patch will be part of 2.6.3. In this case the master will serve the catalog of the given connecting node and not the connecting certname. Of course you need a relaxed auth.conf:

```
...
path ~ ^/catalog/([^/]+)$
method find
allow $1
allow node.domain.com
...
```

Caveat: I didn’t try, but it should work. YMMV :)

**Of course if you follow this and shoot yourself in the foot, I can’t be held responsible for any reasons, you are warned**. Think twice and maybe thrice before implementing this.

### Multiple CA or reusing an existing CA

This goes beyond the object of this blog post, and I must admit I never tried this. Please refer to: [Managing Multiple Certificate Authorities ](http://projects.puppetlabs.com/projects/puppet/wiki/Multiple_Certificate_Authorities)and  [Puppet Scalability](http://projects.puppetlabs.com/projects/puppet/wiki/Puppet_Scalability)

## Conclusion

If there is one: **security is necessary when dealing with configuration management**. We don’t want any node to trust rogue masters, we don’t want masters to distribute sensitive configuration data to rogue nodes. We even don’t want a rogue user sharing the same network to read the configuration traffic. Now that you fully understand SSL, and the X509 PKI, I’m sure you’ll be able to design some clever attacks against a Puppet setup :)

# Updating Deployments

## Modifying and Testing Manifests

As we've called out when we change the manifest modifying a setting that's already managed by puppet. Puppet applies this change to the notes, the puppet agent does whatever is needed to bring the nodes to the new desired state, so you can make a small change in your manifests and have that modify all the machines in your fleet. This is super powerful. But with great power comes great responsibility in the next few videos, we'll look into how we can test our changes to make sure they do what we want them to do and then apply them onto our fleet without causing trouble.

It's pretty common for IT specialist working on configuration management to **test out new rules** on their machines by simply forcing the machine to apply the manifest they want to test. We've done this in some of our examples where we **applied the rules locally before applying them to remote machines**, this approach can backfire though. Say you're trying to use puppet to change the permissions of some files on the nodes locking down some paths that you don't think that your users will need. Now imagine you try out the rules on your computer and discover you made a mistake and locked yourself out. 

Oops. So what can you do instead? There's a bunch of things to consider. A simple first step is to use the `puppet parser validate` command that **checks that the syntax of the manifests is correct** on top of that we can also run the rules using the `--noop` parameter the name comes from no operations and it makes puppet **simulate what it would do** without actually doing it. You can look at the list of actions that it would take and check that they're exactly what you wanted puppet to do.

But if the change is complex, it's likely that we'll miss something important when looking at the planned actions, another option you could use is **having test machines** that are used only for testing out changes. You can apply the rules there and after a puppet has run check that everything's working correctly. But again, this is a manual process and we might forget to verify something important. How can we automate it kind of like the python automatic tests that we checked out in an earlier course. Puppet also lets us test our manifests automatically by using **rspec tests** . In these tests we can set the facts involved different values and check that the catalog ends up stating what we wanted it to, let's check out an example.

```json
describe 'gksu', :type => :class do
  let (:facts) { { 'is_virtual' => 'false' } }
  it { should contain_package('gksu').with_ensure('latest') }
end
```

Here we're setting the is **virtual fact to false**. And then we asked the test infrastructure to verify that the **gksu** package is included with the insurer parameter set to latest tests. Test like this one can be a useful way to check that. Our catalog is written correctly and they can be super helpful when a rule is used a lot of facts that interact with each other and we want to check that the result is actually what we intended. We can write a bunch of these tests and run them automatically whenever there is a change to the rules this way we can be sure that the rules stay valid and know that the new changes didn't break the old rules, but that's just checks that the catalog contains the rules that we set should contain. How can we verify that these rules actually have the effects we want like enabling the corporate website or setting up a strict firewall. We need to apply the rules on the nodes and check that the result is correct.

We can automate this process to, to do this we can use the set of test machines where we first apply the catalog and then use scripts to check that the machines are behaving correctly. Now, let's assume all your tests were successful and the change is ready to be published. How do you push it safely to your whole fleet that's coming up in our next video.

## Safety Rolling out Changes and Validating Them

Once you've prepared and tested the changes that you want to make, it's time to roll them out, but not so fast. Even if you've tested the change on your computer or on a test computer and it worked just fine, it doesn't mean that the change will work correctly on all machines running in production. First, what do we mean by production? In an infrastructure context, **production is the parts of the infrastructure where a service is executed and served to its users**. 

If you host a website, the servers that deliver the website content to the users are the production servers. Inside your company, the servers that validate users passwords are the production authentication servers, you get the idea. Making changes to the production servers can be tricky because if something goes wrong, the service can go down. So how can we roll out changes safely? The key is to always run them through a test environment first. **The test environment should have one or more machines running the exact same configuration as the production environment**. But these machines aren't actually serving any users of the service. This way, there's a problem when deploying the changes should be able to fix it without any actual users seeing it. 

As we briefly touched on in an earlier video, Puppet has **environments** picked in. Each environment has **its own directory with its own set of manifests and modules**. Puppet environments lets us fully isolate the configurations that the agent sees depending on what environment they're running. This isn't just what nodes install which modules, it's also the **whole contents of the modules**. For example, we can use this to try out a whole new version of the Apache module for the machines in the test environment while still using the old version for the production environments. You can define as many environments as you need. For example, you could have a development environment for IT specialists to try out new Puppet rules before they even reach the test environment, or say you're developing a very tricky new feature for your system and you don't know when it'll be ready. You could have an environment for testing just that specific feature. Now, let's assume that you have a bunch of changes ready to roll out. You'll usually push them to the machines in the test environment first and check that everything works well there. This can include both manual verification and automated checking. 

Say the changes worked fine in the test environment, **how do you roll them out to the other machines** in your fleets? You might be tempted to just apply the changes to all the machines and be done with it. But pushing changes to every machine at the same time is usually not a great idea. It's always possible that we missed some special case when preparing the change which wasn't part of our test environment and suddenly, half our fleet is offline. So instead of pushing the changes to all nodes, **we usually do it in batches**. There's a bunch of ways you can do this depending on how your fleet is arranged. You could have some machines with the fact that marks them as early adopters or **canaries**. 

Like the canaries that coal miners used to detect toxic gases in the mines, these nodes detect potential issues before they reach the other computers. So you could push the changes to the canaries on one day, check that everything's working fine, and then deploy them to the rest of the fleet on the next day. That way, if there's an issue with the changes that wasn't caught in testing, only a subset of the users might see it. As soon as you get notified of the problem, you can roll it back and avoid it hitting the rest of the fleet. 

Now, we've been talking about changes without going into detail on what those changes are. It's a good idea for these changes to be small and self-contained. That way, if something breaks, it's much easier to figure out where the problem was. Imagine you're trying to push six months worth of changes to your fleet of computers. When you push this to the machines in the test environment, you discover that they stop responding all together. You now need to come through all the changes that were bundled together to try to find out which one is causing the problem X. 

Instead, you could aim to **roll out your changes every one or two weeks**. This would mean that whenever a problem is detected, there's only a small list of changes to go through to figure out the culprit. Of course, there's a lot more to say about testing and releasing changes safely. But you don't need to put all the best practices in place to get started. You could start small and make improvements as you go. As your manifests get more complex, you want to improve the automated testing of all the pieces. As you managed with your configuration management system grows in size, you want to increase the size of your testing environment, move some nodes to canaries and so on. Up next, there's a reading with more information on using these testing practices in your projects and then a quick quiz.

## Why should you test your Puppet modules?

At first glance, writing tests for your Puppet modules appears to be no more than simply duplicating your manifests in a different language and, for basic “package/file/service” modules, it is.

However, when you start leveling up your modules to include dynamic content from templates, support multiple operating systems or take different actions when passed parameters, these tests become invaluable when adding new functionality to your modules, protecting against regressions when refactoring or upgrading to a new Puppet release.

## What should you be testing?

There are a lot of people confused by the purpose of these tests as they can’t test the result of the manifest on a live system. That is not the point of rspec-puppet.

Rspec-puppet tests are there to test the behaviour of Puppet when it compiles your manifests into a catalogue of Puppet resources. For example, you might want to test that your `apache::vhost` defined type creates a `file` resource with a `path` of `/etc/apache2/sites-available/foo` when run on a Debian host.

When writing your test cases, you should only test the first level of resources in your manifest. By this I mean, when testing your ‘webserver’ role class, you would test for the existence of the `apache::vhost` types, but not for the `file` resources created by them, that’s the job of the tests for `apache::vhost`.

## Basic structure of a test file

Whether you’re testing classes, defined types, hosts or functions the structure of your test file is always the same.

```ruby
require 'spec_helper'

describe '<name of the thing being tested>' do
  # Your tests go in here
end
```

The important thing is what you name your test file and where you put it. Test files should always end in `_spec.rb` (generally, they’re named `<thing being tested>_spec.rb`). Class tests should be placed in `spec/classes`, defined type tests should go in `spec/defines`, host tests should be placed in `spec/hosts` and function tests should go in `spec/functions`.

## Writing your first test cases

*This is not intended to be an RSpec tutorial, just an explanation of how to use the extended functionality that rspec-puppet provides. If you are not familiar with the basics of RSpec, I highly recommend you take some time before continuing to read through the [RSpec documentation](https://www.relishapp.com/rspec).*

Lets say you’re writing tests for a `logrotate::rule` type that does two things:

1. Includes the `logrotate::setup` class which handles installing logrotate
2. A `file` resource that drops your logrotate rule into `/etc/logrotate.d`

First off, lets create a skeleton spec file for your defined type (`modules/logrotate/spec/defines/rule_spec.rb`)

```ruby
require 'spec_helper'

describe 'logrotate::rule' do

end
```

As this is a defined type, the first thing we need to do is give it a title (the string after the `{` in your manifests).

```ruby
  let(:title) { 'nginx' }
```

Now, lets test that we’re including that `logrotate::setup` class

```ruby
  it { is_expected.to contain_class('logrotate::setup') }
```

Remember, we don’t want to test what `logrotate::setup` does, we’ll leave that to the test cases you’re going to be writing for that class.

At this point, your spec file should look like this

```ruby
require 'spec_helper'

describe 'logrotate::rule' do
  let(:title) { 'nginx' }

  it { is_expected.to contain_class('logrotate::setup') }
end
```

OK, on to dealing with that `file` resource, lets use the title of the `logrotate::rule` resource as the name of the file you’re dropping into `/etc/logrotate.d/`.

```ruby
  it { is_expected.to contain_file('/etc/logrotate.d/nginx') }
```

As it currently stands, this test is pretty useless as it doesn’t actually check anything about the file. We can check values of the parameters passed to the file resource by chaining the `with` method onto our test and passing it a hash of expected parameters and values. Lets say we want to set some sane values: present, owned by root and read only:

```ruby
  it do 
    is_expected.to contain_file('/etc/logrotate.d/nginx').with({
      'ensure' => 'present',
      'owner'  => 'root',
      'group'  => 'root',
      'mode'   => '0444',
    })
  end
```

You should now have a spec file that looks like this

```ruby
require 'spec_helper'

describe 'logrotate::rule' do
  let(:title) { 'nginx' }

  it { is_expected.to contain_class('logrotate::setup') }

  it do
    is_expected.to contain_file('/etc/logrotate.d/nginx').with({
      'ensure' => 'present',
      'owner'  => 'root',
      'group'  => 'root',
      'mode'   => '0444',
    })
  end
end
```

What about the most important part of the file, its contents? Before we get to that, we’re going to make your type take a boolean parameter called `compress`. If this value is `true`, a line containing `compress` should exist in the file. If this value is `false`, a line containing `nocompress` should exist in the file.

```ruby
  context 'with compress => true' do
    let(:params) { {'compress' => true} }

    it do
      is_expected.to contain_file('/etc/logrotate.d/nginx') \
        .with_content(/^\s*compress$/)
    end
  end

  context 'with compress => false' do
    let(:params) { {'compress' => false} }

    it do
      is_expected.to contain_file('/etc/logrotate.d/nginx') \
        .with_content(/^\s*nocompress$/)
    end
  end
```

You’ll note that we’re now specifying the parameters that should be sent to our `logrotate::rule` type by setting params to a hash. Similarly, you can also specify the value of facts by using `let(:facts) { }`. The other thing we did was chain a `with_content` method onto our test and passed it a regex that the value should match. You can do this with any other parameter as well, eg `with_ensure`, `with_owner`, `with_foobarbaz`.

As our type can only handle two possible values for `compress`, let’s be nice and make sure that compilation will fail if someone passes something else to it.

```ruby
  context 'with compress => foo' do
    let(:params) { {'compress' => 'foo'} }

    it { is_expected.to compile.and_raise_error(/compress must be true or false/) }
  end
```

The final version of your spec file should be:

```ruby
require 'spec_helper'

describe 'logrotate::rule' do
  let(:title) { 'nginx' }

  it { is_expected.to contain_class('logrotate::setup') }

  it do
    is_expected.to contain_file('/etc/logrotate.d/nginx').with({
      'ensure' => 'present',
      'owner'  => 'root',
      'group'  => 'root',
      'mode'   => '0444',
    })
  end

  context 'with compress => true' do
    let(:params) { {'compress' => true} }

    it do
      is_expected.to contain_file('/etc/logrotate.d/nginx') \
        .with_content(/^\s*compress$/)
    end
  end

  context 'with compress => false' do
    let(:params) { {'compress' => false} }

    it do
      is_expected.to contain_file('/etc/logrotate.d/nginx') \
        .with_content(/^\s*nocompress$/)
    end
  end

  context 'with compress => foo' do
    let(:params) { {'compress' => 'foo'} }

    it do
      expect {
        is_expected.to contain_file('/etc/logrotate.d/nginx')
      }.to raise_error(Puppet::Error, /compress must be true or false/)
    end
  end
end
```

Congratulations, you’ve just written a set of tests for a defined type without writing a single line of Puppet code. You should now head over to the [documentation](https://rspec-puppet.com/documentation/) to learn more.

Now go write the manifests needed to make these tests pass!

# Module Review

## Module 2 Wrap Up: Deploying Puppet

Over the last few videos, we've looked at some ways that we can implement configuration management at your company using Puppet. We saw how we can write Puppet manifests to manage packages, files, and services on one computer, and then extend that to managing more computers by using the server client model. We also checked out how we can use Puppet modules written by other sysadmins or write our own Puppet modules when the existing ones don't meet our needs. We wrapped all this up by looking into how we can test changes to our manifests, and how we can safely roll out changes to our fleet. 

You've now seen the power of Puppet for managing the configuration of machines in your fleet. You've also seen how a small change can affect a large set of machines, and that's only the tip of the iceberg. There's a ton more things you can do with Puppet that we didn't get to cover. In my team at Google, we're constantly running experiments to test the impact of new features, and see how they might affect the performance of our servers or dependencies. Using configuration management lets us track where these experiments are running, which servers they apply to, and where. They also let us show who's running them, and why, and even indicate how to turn them on or off. The manifest files that we wrote in this module were all text files that you can edit with any text editor. This means we can make the most out of tracking these files with a version control system. We store our infrastructure as code and can rollback or cherry pick changes if we need. 

Personally, I think being able to easily track changes is one of the most useful parts of having infrastructure as code. At Google, we have a system that records lots of changes people make to the production environment. This might be something like pushing a new configuration to your servers to increase the amount of memory they should use. Our monitoring systems then take these events and overlay them on top of things like graphs of errors, which makes it super easy to tie potential causes to effects. Say you made a configuration change and right after, there was a spike in server errors. When you have both pieces of information together, it's much easier to understand what's going on. Now, you can benefit from this as well. Up next, there's another lab to help you get more familiar with Puppet. You'll have to get the deployment ready and make it do what you want it to. If this sounds like a lot, don't worry, you've totally got this.

# Cloud Computing

## Intro to Module 3: Automation in the Cloud

Welcome back and congrats on solving yet another tricky lab. In this module will be switching gears a bit. We'll still be talking about automation and configuration management. But now we'll focus on the cloud. If you work in IT, you've probably heard people talking about the cloud a lot. Sometimes people talk about the cloud as if it's a magical way of getting infinite resources for our services. In truth, there's nothing magic about the cloud. But it is a super useful tool in IT for increasing our productivity. In the next few videos we'll dive into the details of the different services available, when it makes sense to use them, and how we can get the most out of our cloud deployments. Even if you've never worked with the cloud directly, you've certainly interacted with the services running in the cloud. For example throughout this course and other courses in this program, you've been using the Qwikabs online learning environment to practice solving problems and creating automation based on real-world scenarios. 

Qwiklabs is one of the many services today that are powered by the cloud. And you've probably used others as well, maybe without even realizing that they were using cloud resources. Before diving into how we can automate at scale using the cloud, we'll do a quick recap of some cloud related concepts to make sure we're all on the same page. We'll check out how cloud deployments can help us quickly scale our services. And we'll cover some things that might be different when running IT infrastructure on-premise versus running it in the cloud. After that, we'll look at how we can use a variety of different tools to manage instances running in the cloud. We'll start with looking at how we can spin up a single virtual machine. And then check out a bunch of ways to manage a whole fleet of virtual machines. As usual, we'll wrap up with a Qwiklabs exercise. This time, you'll use the automation tools that we'll cover to deploy a bunch of web servers running in the cloud. How does that sound? Pretty cool, right? So let's get to it.

## Cloud Services Overview

So when we say that a service is running in the Cloud, what do we actually mean? It has nothing to do with those white fluffy things in the sky, it simply means that the service is running somewhere else either in a data center or in other remote servers that we can reach over the Internet. These data centers house a large variety of machines, different types of machines are used for different services. For example, some machines may have local solid-state drive or SSD, for increased performance while others may rely on virtual drives mounted over the network to lower costs. 

Cloud providers typically offer a bunch of different service types, the ones used most by users are in the Software as a Service category. Software as a Service or SaaS, is when a Cloud provider delivers an entire application or program to the customer. If you choose a Cloud e-mail solution like Gmail, a Cloud storage solution like Dropbox, or a Cloud productivity suite like Microsoft Office 365, there are only a small number of options for you to select or customize. The Cloud provider manages everything related to the service for you including deciding where it's hosted, ensuring the service has enough capacity to serve your needs, performing backups frequently and reliably, and a lot more. 

There's a lot of software being offered as a service by many different Cloud providers or other Internet companies. But of course, not all of our needs can be solved by prepackaged software, sometimes we need to develop our own. For some of the components of our software, we might choose to use Platform as a Service. Platform as a Service or PaaS, is when a Cloud provider offers a preconfigured platform to the customer. When we say platform here, it can be a bit confusing because there are lots of different platforms that exist under a PaaS model. 

Let's check out an example to understand this better. Say you need an SQL database to store some of your applications data, you could choose to host the database in your own hardware. To do this, you'd need to install an operating system on that computer and then install the SQL software on top of the chosen OS. This requires a basic understanding of all of these different pieces just to get the database running. There's a bunch of things that could go wrong and even if you can eventually solve all of them, it can take awhile. Instead, you could decide to use a Cloud provider that offers an SQL database as a service, that way you can just focus on writing SQL queries and using the platform, and let the Cloud provider take care of the rest. 

There's a bunch of different platforms offered as a service by Cloud providers, but of course they are unlikely to cover all of your needs. If you need a high level of control over the software you're running and how it interacts with other pieces in your system, you might want to choose Infrastructure as a Service. Infrastructure as a Service or IaaS, is when a Cloud provider supplies only the bare-bones computing experience. Generally, this means a virtual machine environment and any networking components needed to connect virtual machines, the Cloud provider won't care what you're using the VMs for. 

You could use them to host a web server, a mail server, your own SQL database with your own configuration settings, or a whole lot more possibilities. Running your IT infrastructure on the Cloud provider's IaaS offering is a very popular choice. There's a lot of different providers out there, big and small that offer a service where you can run virtual machines in their Cloud. Some IaaS products include: Amazon's EC2, Google Compute Engine, and Microsoft Azure Compute. 

Now no matter the service model and the provider you use, when you set up Cloud resources you'll need to consider **regions**. **A region is a geographical location containing a number of data centers**, regions contain **zones** and zones can contain one or more **physical data centers**. If one of them fails for some reason, the others are still available and services can be migrated without notably affecting users. Large Cloud providers usually offer their services in lots of different regions around the world. Generally, the region and zone you select should be closest to your users, the further your users are from the physical data center the more latency they may experience. 

This might sound a bit strange but imagine if you are on vacation overseas, you might notice that your bank website loads a little slower. That's why it's common practice to locate data centers close to where users actually live, work, and bank. Latency isn't the only factor to take into account when selecting a region or zone, some organizations require their data to be stored in specific cities or countries for legal or policy reasons. If your service uses other services as dependencies, it's a good idea to host the service physically close to its dependencies. 

For example, if a mail server requires a database server to send an e-mail, it makes sense to host the database server and the mail server in the same zone. Recall that earlier, that Qwiklabs is a service using Cloud infrastructure. So what kind of Cloud service does Qwiklabs use? Qwiklabs uses Infrastructure as a Service, the VMs get provisioned with just the OS and the lab automation then deploys any additional files and software into the OS. Up next, we'll talk about how we can use the services offered by Cloud providers to help us scale our applications.

## Scaling in the Cloud

One of the coolest features of deploying solutions to the Cloud is how easily and quickly we can scale our deployments. In a traditional IT setting, if your team needs an extra server to improve the service, you need to buy additional hardware, install the operating system and application software and then integrate the new computer with the rest of the infrastructure. Doing all of these takes time so it's not easy to quickly scale up or down if the service gets more or less usage. In other words, it takes a significant amount of time to modify the capacity of the deployment. In this context, capacity is how much the service can deliver. The available capacity is tied to the number and size of servers involved. We get more capacity by adding more servers or replacing them with bigger servers. 

The way we measure the capacity of a system depends on what the system is doing. If we're storing data, we might care about the total disk space available. If we have a web server responding to queries from external users, we might care about the number of queries that can be answered in a second which is called **queries per second or QPS**. Or maybe the total **bandwidth** served in an hour. We can measure capacity in other fun ways like the number of cat videos served in an hour or the number of digits of pi a system can calculates. 

Our capacity needs can change over time. Say you're hosting an e-commerce site that needs a hundred servers to meet user demands. As the service becomes more popular, demand might grow and you'll need to increase the available capacity. Eventually, the system could need a thousand servers to meet user demands. This capacity change is called **scaling**. In particular, we call it **upscaling** when we increase our capacity and **downscaling** when we decrease it. This could happen for example if the demand for a product decreased or if the system was improved to need fewer resources. 

Cloud providers typically have a lot of available capacity that can be used by their customers. When we choose to host our infrastructure in the Cloud, we're purchasing and using some of the providers capacity to supplement or completely replace our on-premise capacity. This lets us easily **scale** our service to satisfy demand. There are a couple of different ways that we can scale our service in the Cloud, **horizontally** and **vertically**. To scale a deployment horizontally, we add more nodes into the pool that's part of a specific service. Say your web service is using Apache to serve web pages. By default, Apache is configured to support a 150 concurrent connections. If you want to be able to serve 1,500 connections at the same time, you can deploy 10 Apache web servers and distribute the load across them. This is called horizontal scaling. You add more servers to increase your capacity. If the traffic goes up you could just add more servers to keep up with it. 

On the flip side, if you're scaling a deployment vertically, it means you're making your nodes **bigger**. When we say bigger here we're talking about the resources assigned to the nodes like memories, CPU, and disk space. For example, a database server with a 100 gigabytes of disk space can store more data than with only 10 gigabytes of space. To scale this deployment we can just add a bigger disk to the machine and the same idea works for a CPU and memory too. Say you have a caching server and you notice it's using 95 percent of the available memory. You can deal with that by adding more memory to the node. 

Depending on our deployment and our needs, we might need to scale both horizontally and vertically to scale the capacity of our service. In other words, adding more and bigger nodes to our pool. This approach to scaling isn't too different from what you'd need to do if you have your servers running on-premise. Instead of sending someone to change the physical deployment, for example adding more physical RAM to a server or adding 10 more physical machines in a server rack, we just modify our deployment by clicking some buttons in a web UI or using a configuration management system to automate the scaling for us. The infrastructure built by the Cloud provider will deploy any additional resources we need. 

When talking about scaling in the Cloud, another aspect we need to take into account is whether the scaling is done **automatically** or **manually**. When we set our service to use automatic scaling, we're using a service offered by the Cloud provider. This service uses **metrics** to automatically increase or decrease the capacity of the system. Say you have a system that currently has the capacity to serve 1,000 cat videos per minutes. If the demand for these videos increases to 10,000 per minute and it will, the software in-charge of the automatic scaling will add resources and increase the overall capacity to meet this demand. When the users stop watching cat videos, the automation will remove any unused resources, so the operating costs stay small. But really who wants to stop watching cat videos? But make sure you set a reasonable **quotas** for your autoscaling systems. Otherwise, that viral video of a cute cat wearing a hat might surprise you with a very uncute big bill from your Cloud provider. 

On the flip side, using manual scaling means that changes are controlled by humans instead of software. Manual scaling has its pros and cons too. When the Cloud deployment isn't very complex, it's usually easier for smaller organizations to use manual scaling practices. Say your company currently has a single mail server and you know that you'll want to have another one in six months. In that case, there's no need to overcomplicate that system with an autoscaler. You could simply add the extra server sometime along the way. 

The trade-off here is that without good monitoring or alerting, a system without autoscaling technologies might suffer from unexpected increases in demand. If you're using manual scaling for a service that becomes popular and demand grows quickly, you might not be able to increase the capacity quickly enough. This can store up lots of problems ranging from poor performance to an actual outage. In this video, we've covered concepts that are central to any solution hosted in the Cloud like capacity and scaling. As you probably noticed, Cloud technology offers a ton of benefits for an IT team. But it also can be a little intimidating. Up next, we'll go into some of the reasons why IT teams might be hesitant to migrate to the Cloud and how to overcome those fears.

## Evaluating the Cloud

If you've always worked in a traditional IT environment with servers that are physically owned by your company, the idea of migrating to the cloud can be pretty scary. When you're running the service yourself, if something breaks, you can either physically walk up to the server to fix it or SSH into it from inside the same network. You can apply a quick fix and have your users back to being productive in no time.

As part of the IT team, you own the hardware, software, the network connections, and anything in between, which lets you have a lot of control over what's going on in the whole system. In the case of cloud solutions, we need to give up some of this control to the cloud provider.

We have different levels of control depending on the service model that we choose, whether that's software, platform, or infrastructure as a service. When choosing to use software as a service, we're basically giving the provider complete control of how the application runs. We have a limited amount of settings that we can change, but we don't need to worry about making the system work. This can be a great option when the software provided fulfills all of our needs and we'd rather just focus on using the software instead. 

But as we called out, there's only a limited amount of applications being offered in such a prepackaged way. If we need to create our own applications, we can use platform as a service. With this option, we're in charge of the code, but we aren't in control of running the application. Or we can choose infrastructure as a service, where we can still keep a high level of control. We decide the operating system that runs on the virtual machines, the applications that are installed on it, and so on. We'll still depend on the vendor for other aspects of the deployment, like the network configuration or the services availability. If something does break, you might need to get support from the vendor to fix the problem.

So when choosing a cloud provider, it's important to know what kind of support is available and select the one that fits your needs. I know it sounds strange to give away your control over the hardware, and the network, and the overall infrastructure. But personally, I find that it's pretty great to not have to worry about maintaining the machines that are running our services. It means we can treat the servers executing the workloads as a commodity, instead of special snowflakes. One aspect that might make you hesitant to move to the cloud is that you don't know exactly what security measures are being put in place. So when selecting which provider to use, it's important that you check how they're keeping your instances and your data secure. 

There are a bunch of certifications like SOC 1, ISO 27001, and other industry recognized credentials that you can look for to verify that your provider has invested in security. Once you're sure that your provider is taking the right security measures, it might be tempting to just leave security to the professionals and forget about it. But as cloud users, we also have a responsibility to follow reasonable security practices. Google, Amazon, Microsoft, and other cloud providers invest heavily in security research. But that won't matter if the root password of your cloud instance password one or the instance doesn't use a firewall. In other words, we should always use reasonable judgment to protect the machines that we deploy ,whether that's on physical server is running on-premise or on virtual machines in the Cloud. It's also important to keep in mind that security systems can be expensive to implement correctly. 

Some highly sensitive deployments might warrant specialized security procedures, like multi-factor authentication, encrypted file systems, or public key cryptography. But these processes can also be expensive to implement. It's worth considering if using these techniques is necessary for your specific use case. If your application stores recent patient health records, that's super important data that needs to be protected. You want to apply the most stringent security practices. But if you're dealing with patient health records from the 1800s, you'll need less comprehensive security measures, since this data is much less sensitive, given its age. 

There's a bunch of other reasons why you might have doubts about cloud providers. For example, you might be worried of where your data is going to be stored. Or you might fear that the support offered won't satisfy your needs. No matter the reason, It's important that you carefully read the terms of service to understand the conditions and figure out if the service offered will satisfy your needs. In a way, cloud services are a little like actual clouds. They come in all different shapes and sizes. And sometimes a dark stormy one comes along to rain on your productive day.

But if you prepare an advance with the right security measures and maybe an umbrella, working in the cloud will be nothing but a breeze. So let's say you've decided to migrate part of your infrastructure to the cloud. What do you do next?

Migrating to the cloud is a big topic, and it's coming up in our next video.

## Migrating to the Cloud

A lot of companies today are looking into migrating at least part of their IT infrastructure to the Cloud. The details of the migration will depend on what your infrastructure currently looks like, and what you're trying to achieve by migrating to a Cloud provider. 

In general, we're looking at a trade-off between how much control we have over the computers providing the services and how much work we need to do to maintain them. We've called out that when we use Infrastructure as a Service or IaaS, we deploy our services using virtual machines running on the Cloud providers infrastructure. We have a lot of control over how the infrastructure is designed which can be super useful. For example, we can decide which of the many available machine types to use and what kind of storage to attach to them. 

IaaS is especially useful to administrators using a **lift and shift strategy**. So what does that mean? Say you work at a small organization that's expanding. As the company grows, physical space for employees; desks, ping pong tables, and printers becomes scarce. Eventually, the whole office might need to move to a larger space. This means moving not just the desks and printers, but also any servers running on-premise. If physical servers need to be moved, you might need to take a server from the old office, turn it off during a maintenance window, load it onto a truck, and physically drive it to the new location. This could be the new office or maybe even a small data center. So you're literally lifting the server and moving it to a new location, that's where the lift in lift and shift comes from. 

When migrating to the Cloud, the process is somewhat similar. But instead of moving the physical server in the back of a truck, you migrate your physical servers running on-premise to a virtual machine running in the Cloud. In this case, you're shifting from one way of running your servers to another. The key thing to note with both approaches, is that the servers core configurations stay the same. It's the same software that needs to be installed on the machine to provide its functionality, no matter if the server is hosted physically on-site or virtually in the Cloud. If you've already been using configuration management to deploy and configure your physical servers, moving to a Cloud setup can be pretty easy. You just have to apply the same configuration to the VMs that are running in the Cloud and you'll have replicated the setup. 

On the flip side, using this strategy means that you still have to install and configure the applications yourself. You need to make sure that both the OS and the software stay up to date, that no functionality breaks when they get updated, and a bunch of other things depending on which specific application the server is running. One alternative in this case is using Platform as a Service or PaaS. This is well-suited for when you have a specific infrastructure requirement, but you don't want to be involved in the day-to-day management of the platform. In an earlier video, we mentioned the example of an SQL database that could be used in this way. 

By leaving the management of the database to the Cloud provider, you don't need to worry about having the right disks attached to the computer, configuring the database or any other task related to the machine setup. Instead, you can focus on just using the database. 

Another example of Platform as a Service are **managed web applications**. When using this service, you only have to care about writing the code for the web app. You don't need to care about the framework for running it. This can accelerate development because developers don't have to spend time managing the platform and can just focus on writing code. Some popular managed web application platforms include Amazon Elastic Beanstalk, Microsoft App Service, and Google App Engine. While these platforms are very similar, they aren't fully compatible. So migrating from an on-premise framework and switching between vendors will require some code changes. 

Another related concept that you might have heard of is containers. Containers are applications that are packaged together with their configuration and dependencies. This allows the applications to run in the same way no matter the environment used to run them. In other words, if you have a container running an application, you can deploy it to your on-premise server, to a Cloud provider, or a different Cloud provider. Whichever you choose, it will always run in the same way. This makes migrating from one platform to the other super easy. When talking about migrating to the Cloud, you may also hear about public Clouds, private Clouds, hybrid Clouds, and multi-Clouds. Let's check out what each of these mean. 

- We call **public** Cloud the Cloud services provided to you by a third party. It's called public because Cloud providers offer services to, you guessed it, the public. 
- A **private** Cloud is when your company owns the services and the rest of your infrastructure, whether that's on-site or in a remote data center. It's private because it's just for your company, like having your own Cloud in the sky. 
- A **hybrid** Cloud is a mixture of both public and private Clouds. In this scenario, some workloads are run on servers owned by your company, while others are run on servers owned by a third party. The trick to making the most of the hybrid Cloud is ensuring that everything is integrated smoothly. This way, you can access, migrate, and manage data seamlessly no matter where it's hosted. 
- Finally, **multi-Cloud** is a mixture of public and/or private Clouds across vendors. For example, a multi-Cloud deployment may include servers hosted with Google, Amazon, Microsoft, and on-premise. A hybrid Cloud is simply a type of multi-Cloud, but the key difference is that multi-Clouds will use several vendors, sometimes in addition to on-site services. Using multi-Clouds can be expensive, but it gives you extra protection. If one of your providers has a problem, your service can keep running on the infrastructure provided by a different provider. 

In the last few videos, we've covered a lot of different concepts related to Cloud infrastructure, Cloud services, and how we can use them to scale in the Cloud. Coming up, we've got a quiz to check that all of these concepts are making sense. After that, we'll look into how using Cloud infrastructure looks in practice.

# Managing Instances in the Cloud

## Spinning up VMs in the Cloud

We've been talking a lot about how the Cloud works, what the different concepts that play are, and what they mean. In the next few videos, we'll be showing you how some common actions that you might perform on the Cloud look in practice. As we've called out, there's a bunch of different Cloud providers that you can use for your projects, each with some specific advantages depending on what you're trying to achieve. And while some terms used by one provider might not exactly match the ones used by other providers, the concepts are the same. In these videos, we'll use the Google Cloud platform to demonstrate our examples because, well, it's the platform we know best. 

All Cloud providers give you a console that lets you manage the services that you're using. This console includes pointers to a lot of different services that the providers offer. Seeing all of the options available, it can be a little dizzying at first. So it's a good idea to start just by familiarizing yourself with the platform before you try to do something with it. 

This can mean, for example, looking at the available menus and options, and figuring out where the sections that let you use infrastructure-as-a-service are located. No matter the exact menu entries, when you want to create a VM running in the Cloud, there are a bunch of parameters that you need to set. These parameters are used by the Cloud infrastructure to spin up the machine with the settings that we want. You'll start by choosing the **name** assigned to the instance. This name will later let you identify the instance if you want to connect to it, modify it, or even delete it.

You'll also have to choose the **region** and **zone** where the instance is running. As we called out in an earlier video, you'll generally want to choose a region that's close to your users so that you provide better performance. Another important option that you'll need to select is the **machine type** for your VM. Cloud providers allow users to configure the **characteristics** of their virtual machines to fit their needs. This means selecting how many processing units, or virtual CPUs, and how much memory the virtual machine will be allocated. You might be tempted to select the most powerful VM available, but of course the more powerful the VM, the more money it will cost to run it. 

As a sysadmin, you may need to decide between **costs** and **processing power** to fit the needs of your organization. When setting up instances like these, it's a good idea to start small and **scale as needed.** 

On top of the CPU and memory available, you'll also need to select the **boot disk** that the VM will use. Each virtual machine running in the Cloud has an associated disk that contains the operating system it runs and some extra disk space. When you create the VM, you select both how much space you want to allocate for the virtual disk and what operating system you want the machine to run. 

To create these resources, we can use the web interface or the command line interface. The web UI can be very useful for quickly inspecting the parameters that we need to set. The UI will let us compare the different options available and even show us an estimation of how much money our selected VM would cost per month. This is great for experimenting, but it doesn't scale well if we need to quickly create a bunch of machines or if we want to automate the creation. In those cases, we'll use the command line interface, which lets us specify what we want once, and then use the same parameters many times. 

Using the command line interface lets us create, modify, and even delete virtual machines from our scripts. This is a great step towards automation, but it doesn't stop there. We can also **automate the preparation of the contents** of those virtual machines. Imagine spending an afternoon installing and configuring your new web server. You can do this on one machine, and the process is fairly straightforward. You install any necessary software, you modify any configuration settings, and then make sure that it's working correctly. But it would be hard to reproduce this exactly on another machine, and impossible to do it on thousands of machines. This is where reference images and templating come into play. Reference images store the contents of a machine in a reusable format, while templating is the process of capturing all of the system configuration to let us create VMS in a repeatable way. That exact format of the reference image will depend on the vendor. 

But often, the result is a file called a disk image. A disk image is a snapshot of a virtual machine's disk at a given point in time. Good **templating software** lets you copy an entire virtual machine and use that copy to generate new ones. Depending on the software, the disk image might not be an exact copy of the original machine because some machine data changes, like the hostname and IP address. But it will have the data that we need to make it reusable on lots of virtual machines. This can be super helpful if we want to build a cluster of 10,000 machines which all have identical software. Up next, we'll do a few demos of this process. We'll show you how we can create new VMs in Google Cloud Console, how we can customize those VMs, and how we can use templating and reference images to automate the creation.

## Creating a New VM Using the GCP Web UI

Okay, let's get started with creating a virtual machine on our GCP project. We'll kick things off by navigating to `console.cloud.google.com`, which is where you'll find the cloud console for GCP. Here, the first step is to **create a project** so that our VMs are associated to that project. We need to give our project a **name**, let's name it First Cloud Steps.

Our project is being created, it takes a couple of seconds.

Now that we have a project, our dashboard has a lot more info. Next, we want to go to the menu entry that lets us create virtual machines. To do that, we'll go into the **Compute Engine** menu, and select the **VM instances** entry.

This screen is pretty empty because we don't have any VMs yet. We can create a VM by pressing the **Create** button.

Here we're showing the many different options that we can set for this VM that we're creating. We can set the name, the region and zone, the machine type, the boot disk, and so on. We'll start by calling this machine `linux-instance`.

Now it's time to select the **region** and **zone**. If we click on the region drop-down, we can see all the regions that are currently available to create new VMs. If we click on the zone drop-down we can see the zones available in that region for new VMs. For this example, we'll just keep the default regions. But as we called out, if you're deploying a service, you should select something that's close to your users. Next, we need to select the **type** of machine that we want to use. We can select between **general purpose and memory optimized.** And among each of those families, we can select a bunch of different machine types. We can select how much CPU and how much memory we want our VM to have.

The right selection will depend on what we plan to do with the computer. For our example, we'll just keep the default machine. After selecting the VM, we need to select the disk that we want to use. The default disk is 10 gigabytes in size and comes with a Debian image on it. We can select a different size or different OS by clicking on the Change button.

There's a long list of available operating systems to choose from. The right option will depend on what you're trying to do with your instance. For this example, we'll choose one of the Ubuntu versions. We can select which type of disk we want to use, either the standard disk which is cheaper, or the SSD version which is faster. And we could also change the size if we needed extra storage for our server. For now, we'll just keep the default values here.

After the boot disk, we're shown options to determine how access to the machine will work. This can be very simple or very complex, depending on the rest of your project. The default access option allows you to access the instance remotely using **SSH**, so we'll go with that one for now.

And finally, the creation wizard lets us pre-configure some **firewall rules**. Selecting one of these two options would let HTTP or HTTPS traffic reach our machine.

Of course, there are more firewall rules that you might want to set. Those can be set later on, after the machine is created. In a later video, we'll want to connect to a web server on this machine, so let's turn HTTP on.

There are a lot more options we can set, which are tucked away under this link. We won't look into those now, since the defaults make sense for our test machine. But you can check them out on your own to see what other parameters you can set. We're basically ready to create our VM, but before we do that, let's click on the **command line link**. This will show us how we would create the same VM through the command line.

Wow, that's a long command line, but don't worry, you don't need to understand all of those parameters. The takeaway here is that you could select all the options that you want to create the VM that you need, and then copy this command to create a bunch of VMs that are all exactly the same as the one you selected. For now, we'll close this window and then create the VM using the Create button.

Our instance is being created, this takes a bit of time. The system is assigning the necessary resources to our machine, deploying the operating system image, connecting the network interfaces, and so on. Once it's done setting up, we can connect to it using SSH.

Again, it takes a little while for the system to set up the **keys** that we'll use to log on. But once it's done, we can use the machine remotely.

Let's check that the machine we created is using the OS we selected.

And with that, we've just created a VM using the web interface and connected to it using SSH, how cool is that? Once you're logged into the machine, you can treat it like any normal Linux machine, which is pretty awesome. For example, we can get a text version of the weather in our current location by calling the `curl` command, which we can use to access web pages from the command line, and passing in `wttr.in` as the website.

Looks like it's overcast in the cloud.

Up next, we'll start experimenting with our VM by deploying a simple web application to it.

## Customizing VMs in GCP

In our last video, we checked out how to create a single virtual machine in the cloud. That's cool, but not too useful at cloud scale. Remember, cloud scale deployments are often comprised of hundreds or thousands of machines. So creating a single server is only the beginning. Let's make some changes to that VM so that we can deploy it at scale. Once we're done, we'll use the instance that we configured as the base for our reference image. Remember that a reference image is just a file or configuration that we can deploy repeatedly and with automated tools. This is important because it lets us build scalable services very quickly. Let's start by logging into the virtual machine we created in the last video.

We'll use git which will let us clone the repository with the code for the app we want to deploy.

The repo we've cloned includes a very simple web serving application written in Python. Let's run it to see what happens.

Our script prints a single line saying that it's listening for connections on port 8000. What's happening behind the scenes is that the application is opening a socket and listening for HTTP connections on that port. In this case, it's running on port 8000. And if we were running this locally on our machine, we could connect to that port. But this is running on a virtual machine in the cloud which has a firewall and only a couple of ports enabled. What are our options? The script actually lets us pass the port number that it will open as a parameter.

We want it to run on the HTTP port that we configured in our last video which is port 80. And because this is a system port, to let our application use it, we'll need to run it with admin privileges. So let's stop the running process now by pressing Ctrl+C. And then run it again with sudo and pass port 80 as the parameter.

`sudo ./hello_cloud.py 80`.

Now we can visit the website served by our VM and see its contents. Let's navigate to it.

Our web app is extra symbol. It just prints Hello Cloud to the web page generated when we make a request. It also prints the Hostname and IP Address of the machine. This will help us later on when we deploy the solution at scale. All right, we have a web serving application running on the HTTP port. That's nice, but we had to start the application manually so this doesn't scale. To get our application to start automatically, we need to configure this as a **service**. Fortunately, our repo already includes a service definition that we can use. Let's check out the contents of that file.

This is a **systemd** file, which is the initializing system used by most modern Linux distributions.

Don't worry if you don't understand what's going on here.

You don't need to understand the details of this file to know how to deploy services to the cloud. Just notice that the configuration expects the script that we want to execute to be in `/usr/local/bin`. We need to copy that file over to there and then copy the service file to `/etc/systemd/system`, which is the directory used for configuring systemd services. And finally, we need to tell the systemctl command that we want to enable this service so that it runs automatically. Okay, now that we've done this, anytime this machine starts, it will start the web app that we've configured and we'll be able to see the content that we saw before. Let's try it out by triggering a reboot.

We've rebooted the machine. This will take a while to complete. It tells us that the connection was lost and that we can ask our terminal to reconnect. This will take a bit of time until the machine has finished rebooting and is ready to receive connections, patience, my friend.

Okay, our VM has rebooted. We can check if our application is running by using the `ps ax` command to get a list of the running processes and filter it so we keep only the ones matching a pattern using the `grep` command. In this case, we'll use hello as the pattern.

Yay, our application is now running on startup. We're almost ready to turn our configured VM into a template for creating a lot more of them. But before we do that, we need to think about how we'll upgrade our web app when we want to make changes to it. There's a bunch of different options here. One option is to **create a different reference image each time there's a new version of the app**. This would mean deleting all the old VMs and creating new ones based on the new image.

Another option is to add a **configuration management system** to the images so that we can use that to manage any changes after the VM's created. We already know how to manage changes with Puppet. Remember our Puppet Master training from earlier videos? Let's install the Puppet client in this instance so it's ready to use Puppet in the future.

Now when we looked into the Puppet Server and client setup, we saw that there was a bunch of steps that we need to run on the client side to have it ready to apply the rules. The repo we cloned includes a script we can run which will do the initial configuration for us. It will also set the Puppet process to run automatically on boot. Let's run that now.

Setup, Now any time this machine starts, it will serve our website and we want to update that website's content. We can do that using our Puppet infrastructure. Nice, our VM is now ready to be used as a basis for a template, which we can use to create as many instances as we need. Up next, we'll check out how to create the template and how to create instances based on it.

## Templating a Customized VM

In the last few videos, we created a VM, and then made sure that it was set up to serve our web app, and to stay updated via Puppet. We can now use this VM as a basis for creating an **instance template**, and then use the template to create a bunch of VMs based on it. Let's do that.

To create a reference image, we need to have access to the current virtual disk that's running on the computer. So the first step to create the image is to **stop the VM**. It takes a while for the machine to shut down cleanly. Once it's finished, we can click on the machine's name to see all its details, and then we can click on the **boot disk**.

These are the details of the disk attached to the VM. We can create a **snapshot**, which is a full copy of the current state of the disk, or an image, which lets us create a template based on it. Let's click create image.

We'll call our image `webserver-image`. Here, the creation wizard shows that we'll be creating the image based on the Linux-instance disk, which is what we want. For this example, we'll leave the rest of the settings with the default values. Okay, let's create our image.

This is now creating the image that we'll use for our template. As we called out earlier, the tools will keep most of the contents of the image, but remove things that should be different across VMs. Once it's finished creating, it shows us the list of all images that we can access. As you can see, this is a long list that includes a bunch of stuff along with our image. The other images are public images that we can use to deploy different types of VMs. All right. We're now ready to create our instance template. To do that, we'll go to the instance template option, and then click **create new instance template**. As usual, we're shown a wizard that includes a bunch of different options that we can set. We'll keep most of the defaults, and change only a couple of things. We'll name our template `webserver- template`. We'll change the boot disk to use the image we've created.

In this screen, we can see the list of all the available images. By default, the list shows the official operating system images provided by the platform. For our template, we want to use the custom Image we've created.

And finally, we'll also want to enable HTTP access to the instances created with this template. That's it. We're ready to create our new template.

This takes a little bit of time to create. Once it's done, we can create instances based on our images. We'll do it once more from the web interface, and then we'll check out how to do it from the command line. Let's go back to the VM instances entry, and then click on create instance.

This time, instead of creating an instance from scratch, we'll use the template we've prepared. We'll name our instance `webserver-one`. Everything else we'll leave as is. Check out how it says that it will use the base image we selected, and that HTTP traffic will be allowed.

All right, we've created our second VM based on the template. We didn't have to change any options, because all of the values were already pre-selected in the template. And the web app that we want is ready to run, without us having to configure anything. Let's check that out.

Yes, our application is already running successfully on this machine. This is great, but it's still a bit cumbersome if we want to create ten VMs like this one.

For a batch action like that, it's better to use the command line interface. So let's do that. To interact with Google Cloud, we'll be using the gcloud command. We've already installed the gcloud command on this machine. You'll find pointers on how to install gcloud on different platforms in the next reading. We'll start by running the `gcloud init` command, which sets up the authentication mechanisms between this computer and Google Cloud.

We need to authenticate to the Google Cloud system to be able to use the gcloud command to interact with it. Let's say yes here.
This opened a new tab in our browser that we can use to authenticate with our account. Let's follow the process here, and authenticate.

We're now logged into our cloud account. We can choose which will be our default project. Let's select one here.

We've selected the default project. On top of that, the initializing wizard lets us select the default region and zone. It's a good idea to select this, as the commands that we use in the future will use that zone and region if we don't specify a different one. This is a long list. There are a lot of different zones available for our instances. As we called out earlier, when selecting where to run your services, you should go with the one that's closest to you. For this example, we'll just go with Zone 1. Once we've completed this authentication, we can use the gcloud command to operate on our Cloud project. We can modify the VMs we've created, create new ones, delete some of the existing ones, and a lot more. For our example, we'll use it to create five additional VMs. It goes like this. First, we call gcloud, then we pass the compute parameter that's used for everything that has to do with virtual machines. Then we pass the instances parameter, as we'll be dealing with the VM instances themselves.

So then, we pass create, as we want to create instances. We'll see that we want to use the source instance template called web server- template. And finally, we'll give the name of the instances that we want to deploy. Let's call them `ws1, ws2, ws3, ws4, and ws5`. It takes only a short while until all instances are created. This is definitely much faster than going through the web interface, and much easier to automate through our scripts.

And with that, we've seen how we can create a virtual machine, customize it, create a template out of it, and use that template to create a bunch of new identical virtual machines. I hope you're starting to see how useful this can be when creating new IT deployments. Up next, there's a reading where you'll find a bunch more information about all the tools that we've demonstrated, and then a quick quiz to practice everything that you've just learned.

# Automating Cloud Deployments

## Cloud Scale Deployments

Over the past few videos, we've checked out some of the features we can use when running services in the Cloud. As we called out before, the biggest advantage of using Cloud services is how easily we can scale our services up and down. Now, to make the most out of this advantage, we need to do some preparation. 

We'll set up our services so that we can easily increase their capacity by adding more nodes to the pool. These nodes could be virtual machines, containers, or even specific applications providing one service. Whenever we have a service with a bunch of different instances serving the same purpose, we'll use a **load balancer**. 

A load balancer ensures that each node receives a **balanced number of requests**. When a request comes in, the load balancer picks a node to serve the response. There's a bunch of different strategies load balancer uses to select the node. The simplest one is just to give each node one request called **round robin**. More complex strategies include always selecting the same node for requests coming from the same origin, selecting the node that's closest to the requester, and selecting the one with the least current load. 

As we called out, instance groups like these are usually configured to spin up more nodes when there's more demand, and to shut some nodes down when the demand falls. This capability is called **autoscaling**. It allows the service to increase or reduce capacity as needed while the service owner only pays for the cost of the machines that are in use at any given time. Since some nodes will shut down when demand is lower, their local disks will also disappear and should be considered **ephemeral or short-lived**. If you need **data persistence**, you'll have to create separate storage resources to hold that data and connect that storage to the nodes. 

That's why the services that we run in the Cloud are usually connected to a database which is also running in the Cloud. This database will also be served by multiple nodes behind a load balancer, but this is typically managed by the Cloud provider using the platform as a service model. To check out how this works in practice, let's look at an example of a web application with a lot of users. 

When you connect to a site through the Internet, your web browser first retrieves an IP address for the website that you want to visit. This IP address identifies a specific computer, the entry point for the sites. Commonly there will be a bunch of different **entry points** for a single website. This allows the service to stay up even if one of them fails. On top of that, it's possible to select an entry point that's closer to the user to reduce latency. 

In a small-scale application, this entry point could be the web server that serves the pages, and that would be it. For large applications where speed and availability matter, there will be a couple of layers in between the entry point and the actual web service. 

The first layer will be a **pool of web caching servers with a load balancer** to distribute the requests among them. One of the most popular applications for this caching is called **Varnish**, but of course it's not the only one. The **Nginx** web server and software also includes this caching functionality. There's a bunch of providers that do web caching as a service like **Cloudflare** and **Fastly**. No matter the software used, the result is basically the same. 

When a request is made, the caching servers first check if the content is already stored in their memory. If it's there, they respond with the contents, if it's not, they ask their configured **backend** for the content and then store it so that it's present for future requests. This configured backend is the actual web service that generates the webpages for the site, and it will also normally be a pool of nodes running under a load balancer. To get any necessary data, this service will connect to a database. But because getting data from a database can be slow, there's usually an extra layer of **caching**, specific for the database contents. 

The most popular applications for this level of caching are Memcached and Redis. As you can see, there is a lot of different nodes in this scheme. Fortunately, once you've done your homework and prepared your setup, you can rely on the capabilities offered by the Cloud provider to automatically scale the system up and down as necessary. The infrastructure will take care of adding and removing instances, distributing the load, making sure that each geographical region has the right capacity, and a bunch more things. Up next, we'll talk about some of the things we can do when we need to have more control over the instances that are running our service.

## What is Orchestration?

Throughout this course and the entire program, we've been talking about **automation**. As a reminder, automation is the **process of replacing a manual step with one that happens automatically**. In the past few videos, we've mentioned a few ways that let us automate the creation of Cloud instances. 

We can use templating to create new virtual machines, we can run a command line tool that automatically creates new instances for us, or we can choose to enable auto-scaling and let the infrastructure tools take care of that depending on the demand. But all of this automatic creation of new instances needs to be coordinated so that the instances **correctly interact with each other** and that's where **orchestration** comes into play. 

**Orchestration is the automated configuration and coordination of complex IT systems and services**. In other words, orchestration means automating a lot of different things that need to talk to each other. This will always include a lot of different automated tasks and will generally involve configuring a bunch of different systems. Taking the example of the website infrastructure that we saw in our last video, we've seen how we can automate the creation of each instance in the system. 

Now, say you wanted to deploy a new copy of the system in a separate data center where you have no instances yet, you'll need to also automate the whole configuration of the system, the different instance types involved, how will each instance finesse the others, what the internal network looks like, and so on. So how does this work? 

The key here is that the configuration of the overall system needs to be automatically repeatable. There's a bunch of different tools that we can use to do that. These tools typically don't communicate with the Cloud systems through the web interface or the command line. They normally use an application programming interface or API that lets us interact with the Cloud infrastructure directly from our scripts. We'll talk more about other APIs in a later course. In the case of Cloud provider APIs, they typically let you handle the configuration that you want to sit directly from your **scripts** or **programs** without having to call a separate command. 

This combines the power of programming with all of the available Cloud resources. The APIs offered by the Cloud providers let us perform all the tasks that we mentioned earlier like creating, modifying, and deleting instances and also deploying complex configurations for how these instances will talk to each other. All of these actions can also be completed through the web interface or the command line. But doing them from our programs gives us **extra flexibility** which can be key when automating complex setups. 

Say you wanted to deploy a system that combines some services running on a Cloud provider and some services running on-premise, this is known as a hybrid Cloud setup, or only part of the services are in the Cloud. The setup is super common in the industry right now. Orchestration tools can be a pretty useful tool to make sure that both the on-premise services and the Cloud services know how to talk to each other and are configured with the right settings. Going back to the website example that we discussed earlier to make sure that the service is running smoothly, we should set up a **monitoring** and **alerting**. 

This lets us detect and correct any problems with our service before users even notice. This is a critical piece of infrastructure but setting it up correctly can take quite some time. By using orchestration tools, we can automate the configuration of any monitoring rules that we need to set, which metrics we want to look for, when we want to be alerted, and so on, and automatically apply these to a complete deployment no matter which datacenter the services are running in. This might seem like a super complex task, but fortunately there are tools available to make our lives easier. We'll talk about those in our next video.

## Cloud Infrastructure as Code

In our last video, we talked about how we need to orchestrate complex Cloud setups. This includes handling a bunch of different nodes with different workloads, managing the complexity of deploying a hybrid setup, or modifying deployments across several Data centers. 

Back at the beginning of the course, we talked about infrastructure as Code, and we called out that storing our infrastructure in a code like format, lets us create repeatable infrastructure, and that using Version control for the storage, means that we can keep a history of what we've done and easily rollback mistakes. 

These principles also apply to Cloud infrastructure. The way we store it might be a little different depending on the tools that we use, but we'll still be storing this configuration in a code like format using **Version control** to keep track of the changes. This lets us manage large-scale solutions with a small team. We can very quickly have an idea of what the deployment looks like, by looking at the configuration. We can try new things out and roll back if anything goes wrong. We can look at the history of changes to figure out why a specific change was made, and much more. 

Most Cloud providers offer their own tool for managing resources as code. Amazon has Cloud Formation, Google has Cloud Deployment Manager, Microsoft has Azure Resource Manager, and OpenStack has Heat Orchestration Templates. These tools are specific to the Cloud provider, which means it can be complex and cumbersome to move to a different provider or combine a Cloud deployment with an on-premise deployments. An option that's becoming really popular in the Orchestration field, is called **Terraform**. 

Similar to Puppet, Terraform uses its own **Domain-specific language** which lets us specify what we want our Cloud infrastructure to look like. The cool thing about Terraform is that it knows how to interact with a lot of different Cloud providers and automation vendors. So you can write your **Terraform rules** to deploy something on one Cloud provider, and then use very similar rules to deploy the service to a different Cloud provider. Terraform uses each Cloud provider's API to accomplish this. This **keeps you from having to learn a new API** when moving to a different Cloud provider, and lets you focus on the infrastructure design. We saw in earlier videos how we can have a puppet rule that specifies that a computer should install a given package, and that the local puppet agent analyzes the computer and decides which installation mechanism to use depending on the operating system, the specific Linux distro and so on.

A similar thing happens with Terraform. The **rules** that define the resources like the VMs or containers to use, will use specific **values** related to the Cloud provider like selecting which machine type to use or in what region to deploy it. But a lot of the overall configuration is independent of the provider, and can be reused if we decide to move our configuration to a different provider or we want to use a hybrid setup. 

Of course Terraform isn't the only option. Puppet itself also ships with a bunch of plug-ins that can be used to interact with the different Cloud providers to create and modify the desired Cloud infrastructure. Finally, let's spend a moment talking about the contents of the nodes or instances managed by the Orchestration tools. When dealing with nodes in the Cloud, there are basically two options. 

Either they're **long-lived** and their contents need to be periodically updated, or they are **short-lived** and updates are made by deleting the old instances and deploying new ones. Long-lived instances are typically servers that are not expected to go away. Things like your company's internal mail server or internal document sharing servers, will manage these instances using a configuration management system like Puppet, which can deploy any necessary changes to the machines while they're running. This keeps them updated to the latest state. 

On the flip side, short-lived instances come and go very quickly. For these cases, it makes less sense to apply changes while they're running. Instead, we normally apply the configuration that we want the instances to have when they start, and we deploy any future changes by replacing the instances with new ones. 

We can still use Puppet for the initial setup, but we don't need to run the agent periodically, only at the start. If all this sounds super complex, that's okay. There's a lot to learn about Cloud Orchestration, and many of these concepts will make more sense once you've tried them out. Up next, we've gathered some additional info you can use if you want to find out more. Then there is a quick quiz to put all of these concepts together.

# Getting started with Terraform on Google Cloud

One of the things I find most time consuming when starting on a new stack or technology is moving from reading documentation to a working prototype serving HTTP requests. This can be especially frustrating when trying to tweak configurations and keys, as it can be hard to make incremental progress. However, once I have a shell of a web service stood up, I can add features, connect to other APIs, or add a datastore. I'm able to iterate very quickly with feedback at each step of the process. To help get through those first set up steps I've written this tutorial to cover the following:

- Using [Terraform](https://cloud.google.com/docs/terraform) to create a VM in Google Cloud
- Starting a basic Python Flask server

## Before you begin

You will be starting a single Compute Engine VM instance, which can incur real, although usually minimal, costs. Pay attention to the pricing on the account. If you don't already have a Google Cloud account, you can [sign up for a free trial](https://cloud.google.com/free) and get $300 of free credit, which is more than you'll need for this tutorial.

Have the following tools locally:

- [An existing SSH key](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)
- [Terraform](https://www.terraform.io/intro/getting-started/install.html)

This tutorial is written using Terraform 0.12 syntax. If you're using a different version of Terraform, some of the syntax will be slightly different.

## Create a Google Cloud project

A default project is often set up by default for new accounts, but you will start by creating a new project to keep this separate and easy to tear down later. After creating it, be sure to copy down the project ID as it is usually different then the project name.

![How to find your project ID.](https://storage.googleapis.com/gcp-community/tutorials/getting-started-on-gcp-with-terraform/gcp_project_id.png)

### Getting project credentials

Next, set up a service account key, which Terraform will use to create and manage resources in your Google Cloud project. Go to the [create service account key page](https://console.cloud.google.com/apis/credentials/serviceaccountkey). Select the default service account or create a new one. If you're creating a new service account for this tutorial, you can use the Project Owner role, but we recommend that you remove the service account or restrict its scope after you have completed the tutorial. Select JSON as the key type and click **Create**.

This downloads a JSON file with all the credentials that will be needed for Terraform to manage the resources. This file should be located in a secure place for production projects, but for this example move the downloaded JSON file to the project directory.

### Setting up Terraform

Create a new directory for the project to live and create a `main.tf` file for the Terraform config. The contents of this file describe all of the Google Cloud resources that will be used in the project.

```HCL
// Configure the Google Cloud provider
provider "google" {
 credentials = file("CREDENTIALS_FILE.json")
 project     = "flask-app-211918"
 region      = "us-west1"
}
```

Set the project ID from the first step to the `project` property and point the credentials section to the file that was downloaded in the last step. The `provider “google”` line indicates that you are using the [Google Cloud Terraform provider](https://www.terraform.io/docs/providers/google/index.html) and at this point you can run `terraform init` to download the latest version of the provider and build the `.terraform` directory.

```
terraform init

Initializing provider plugins...
- Checking for available provider plugins on https://releases.hashicorp.com...
- Downloading plugin for provider "google" (1.16.2)...

The following providers do not have any version constraints in configuration,
so the latest version was installed.

To prevent automatic upgrades to new major versions that may contain breaking
changes, it is recommended to add version = "..." constraints to the
corresponding provider blocks in configuration, with the constraint strings
suggested below.

* provider.google: version = "~> 1.16"

Terraform has been successfully initialized!
```

### Configure the Compute Engine resource

Next you will create a single Compute Engine instance running Debian. For this demo you can use the smallest instance possible (check out [all machine types here](https://cloud.google.com/compute/docs/machine-types)) but you can upgrade to a larger instance later. Add the `google_compute_instance` resource to the `main.tf`:

```HCL
// Terraform plugin for creating random ids
resource "random_id" "instance_id" {
 byte_length = 8
}

// A single Compute Engine instance
resource "google_compute_instance" "default" {
 name         = "flask-vm-${random_id.instance_id.hex}"
 machine_type = "f1-micro"
 zone         = "us-west1-a"

 boot_disk {
   initialize_params {
     image = "debian-cloud/debian-9"
   }
 }

// Make sure flask is installed on all new instances for later steps
 metadata_startup_script = "sudo apt-get update; sudo apt-get install -yq build-essential python-pip rsync; pip install flask"

 network_interface {
   network = "default"

   access_config {
     // Include this section to give the VM an external ip address
   }
 }
}
```

The [`random_id` Terraform plugin](https://www.terraform.io/docs/providers/random/r/id.html) allows you to create a somewhat random instance name that still complies with the Google Cloud instance naming requirements but requires an additional plugin. To download and install the extra plugin, run `terraform init` again.

### Validate the new Compute Engine instance

You can now validate the work that has been done so far. Run `terraform plan` which will:

- Verify the syntax of `main.tf`is correct
- Ensure the credentials file exists (contents will not be verified until `terraform apply`)
- Show a preview of what will be created

Output:

```
An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  + google_compute_instance.default
      id:                                                  [computed]
...

  + random_id.instance_id
      id:                                                  [computed]
...


Plan: 2 to add, 0 to change, 0 to destroy.
```

Now it's time to run `terraform apply` and Terraform will call Google Cloud APIs to set up the new instance. Check the [VM Instances page](https://console.cloud.google.com/compute/instances), and the new instance will be there.

## Running a server on Google Cloud

There is now a new instance running in Google Cloud, so your next steps are getting a web application created, deploying it to the instance, and exposing an endpoint for consumption.

### Add SSH access to the Compute Engine instance

You will need to add a public SSH key to the Compute Engine instance to access and manage it. Add the local location of your public key to the `google_compute_instance` metadata in `main.tf` to add your SSH key to the instance. [More information on managing ssh keys is available here](https://cloud.google.com/compute/docs/instances/adding-removing-ssh-keys).

```HCL
resource "google_compute_instance" "default" {
 ...
metadata = {
   ssh-keys = "INSERT_USERNAME:${file("~/.ssh/id_rsa.pub")}"
 }
}
```

Be sure to replace `INSERT_USERNAME` with your username and then run `terraform plan` and verify the output looks correct. If it does, run `terraform apply` to apply the changes.

The output shows that it will modify the existing compute instance:

```Shell
An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:
  ~ update in-place

Terraform will perform the following actions:

  ~ google_compute_instance.default
      metadata.%:       "0" => "1"
…

Apply complete! Resources: 0 added, 1 changed, 0 destroyed.
```

### Use output variables for the IP address

Use [a Terraform output variable](https://www.terraform.io/intro/getting-started/outputs.html) to act as a helper to expose the instance's ip address. Add the following to the Terraform config:

```HCL
// A variable for extracting the external IP address of the instance
output "ip" {
 value = google_compute_instance.default.network_interface.0.access_config.0.nat_ip
}
```

Run `terraform apply` followed by `terraform output ip` to return the instance's external IP address. Validate that everything is set up correctly at this point by connecting to that IP address with SSH.

This tutorial needs the `default` network's `default-allow-ssh` firewall rule to be in place before you can use SSH to connect to the instance. If you are starting with a new project, this can take a few minutes. You can check the [firewall rules list](https://console.cloud.google.com/networking/firewalls/list) to make sure that the firewall rule has been created.

```Shell
ssh `terraform output ip`
```

## Building the Flask app

You will be building [a Python Flask app](http://flask.pocoo.org/) for this tutorial so that you can have a single file describing your web server and test endpoints. Inside the VM instance, add the following to a new file called `app.py`:

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_cloud():
   return 'Hello Cloud!'

app.run(host='0.0.0.0')
```

Then run this command:

```Shell
python app.py
```

Flask serves traffic on `localhost:5000` by default. Run `curl` in a separate SSH instance to confirm that your greeting is being returned. To connect to this from your local computer, you must expose port 5000.

Run this command to validate the server:

```Shell
curl http://0.0.0.0:5000
```

The output from this command is `Hello Cloud`.

### Open port 5000 on the instance

Google Cloud allows for opening ports to traffic via firewall policies, which can also be managed in your Terraform configuration. Add the following to the config and proceed to run plan/apply to create the firewall rule.

```HCL
resource "google_compute_firewall" "default" {
 name    = "flask-app-firewall"
 network = "default"

 allow {
   protocol = "tcp"
   ports    = ["5000"]
 }
}
```

Congratulations! You can now point your browser to the instance's IP address and port 5000 and see your server running.

## Cleaning up

Now that you are finished with the tutorial, you will likely want to delete everything that was created so that you don't incur any further costs. Thankfully, Terraform will let you remove all the resources defined in the configuration file with `terraform destroy`:

```
terraform destroy
random_id.instance_id: Refreshing state... (ID: ZNS6E3_1miU)
google_compute_firewall.default: Refreshing state... (ID: flask-app-firewall)
google_compute_instance.default: Refreshing state... (ID: flask-vm-64d4ba137ff59a25)

An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:
  - destroy

Terraform will perform the following actions:

  - google_compute_firewall.default

  - google_compute_instance.default

  - random_id.instance_id
...

google_compute_firewall.default: Destroying... (ID: flask-app-firewall)
google_compute_instance.default: Destroying... (ID: flask-vm-64d4ba137ff59a25)
google_compute_instance.default: Still destroying... (ID: flask-vm-64d4ba137ff59a25, 10s elapsed)
google_compute_firewall.default: Still destroying... (ID: flask-app-firewall, 10s elapsed)
google_compute_firewall.default: Destruction complete after 11s
google_compute_instance.default: Destruction complete after 18s
random_id.instance_id: Destroying... (ID: ZNS6E3_1miU)
random_id.instance_id: Destruction complete after 0s
```

# Terraform Enterprise GCP Reference Architecture

## Introduction

This document provides recommended practices and a reference architecture for HashiCorp Terraform Enterprise implementations on GCP.

## Implementation Modes

Terraform Enterprise can be installed and function in different implementation modes with increasing capability and complexity:

- *Standalone:* The base architecture with a single application node that supports the standard implementation requirements for the platform.
- *Active/Active:* This is an extension of *Standalone* mode that adds multiple active node capability that can expand horizontally to support larger and increasing execution loads.

Since the architectures of the modes progresses logically, this guide will present the base *Standalone* mode first and then discuss the differences that alter the implementation into the *Active/Active* mode.

## Required Reading

Prior to making hardware sizing and architectural decisions, read through the [pre-install checklist](https://www.terraform.io/docs/enterprise/before-installing/index.html) to familiarize yourself with the application components and architecture. Further, read the [reliability and availability guidance](https://www.terraform.io/docs/enterprise/system-overview/reliability-availability.html) as a primer to understanding the recommendations in this reference architecture.

## Infrastructure Requirements

**Note:** This reference architecture focuses on the *External Services* operational mode.

Depending on the chosen [operational mode](https://www.terraform.io/docs/enterprise/before-installing/index.html#operational-mode-decision), the infrastructure requirements for Terraform Enterprise range from a single Cloud Compute VM instance for demo installations to multiple instances connected to Cloud SQL and Cloud Storage for a stateless production installation.

The following table provides high-level server guidelines. Of particular note is the strong recommendation to avoid non-fixed performance CPUs, or “Shared-core machine types” in GCP terms, such as f1-series and g1-series instances.

### Terraform Enterprise Server (Compute Engine VM via Regional Managed Instance Group)

| Type    | CPU    | Memory    | Disk        | GCP Machine Types |
| :------ | :----- | :-------- | :---------- | :---------------- |
| Minimum | 4 core | 15 GB RAM | 50GB/200GB* | n1-standard-4     |
| Scaled  | 8 core | 30 GB RAM | 50GB/200GB* | n1-standard-8     |

#### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#hardware-sizing-considerations)Hardware Sizing Considerations

- *Terraform Enterprise requires 50GB for installation, but [GCP documentation for storage performance](https://cloud.google.com/compute/docs/disks/#performance) recommends "to ensure consistent performance for more general use of the boot device, use either an SSD persistent disk as your boot disk or use a standard persistent disk that is at least 200 GB in size."
- The minimum size would be appropriate for most initial production deployments, or for development/testing environments.
- The scaled size is for production environments where there is a consistent high workload in the form of concurrent Terraform runs.

### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#postgresql-database-cloud-sql-postgresql-production-)PostgreSQL Database (Cloud SQL PostgreSQL Production)

| Type    | CPU    | Memory    | Storage | GCP Machine Types            |
| :------ | :----- | :-------- | :------ | :--------------------------- |
| Minimum | 4 core | 16 GB RAM | 50GB    | Custom PostgreSQL Production |
| Scaled  | 8 core | 32 GB RAM | 50GB    | Custom PostgreSQL Production |

#### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#hardware-sizing-considerations-1)Hardware Sizing Considerations

- The minimum size would be appropriate for most initial production deployments, or for development/testing environments.
- The scaled size is for production environments where there is a consistent high workload in the form of concurrent Terraform runs.

### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#object-storage-cloud-storage-)Object Storage (Cloud Storage)

A [Regional Cloud Storage](https://cloud.google.com/storage/docs/storage-classes#regional) bucket must be specified during the Terraform Enterprise installation for application data to be stored securely and redundantly away from the Compute Engine VMs running the application. This Cloud Storage bucket must be in the same region as the Compute Engine and Cloud SQL instances. Vault is used to encrypt all application data stored in the Cloud Storage bucket. This allows for further [server-side encryption](https://cloud.google.com/storage/docs/encryption/). by Cloud Storage.

### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#other-considerations)Other Considerations

#### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#additional-gcp-resources)Additional GCP Resources

In order to successfully provision this reference architecture you must also be permitted to create the following GCP resources:

- [Project](https://cloud.google.com/resource-manager/docs/creating-managing-projects)
- [VPC Network](https://cloud.google.com/vpc/docs/vpc)
- [Subnet](https://cloud.google.com/vpc/docs/using-vpc)
- [Firewall](https://cloud.google.com/vpc/docs/firewalls)
- [Target Pool](https://cloud.google.com/load-balancing/docs/target-pools)
- [Forwarding Rule](https://cloud.google.com/load-balancing/docs/forwarding-rules)
- [Compute Instance Template](https://cloud.google.com/compute/docs/instance-templates/)
- [Regional Managed Instance Group](https://cloud.google.com/compute/docs/instance-groups/distributing-instances-with-regional-instance-groups)
- [Cloud DNS (optional)](https://cloud.google.com/dns/)

#### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#network)Network

To deploy Terraform Enterprise in GCP you will need to create new or use existing networking infrastructure. The below infrastructure diagram highlights some of the key components (network, subnets) and you will also have firewall and gateway requirements. These elements are likely to be very unique to your environment and not something this Reference Architecture can specify in detail.

#### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#dns)DNS

DNS can be configured external to GCP or using [Cloud DNS](https://cloud.google.com/dns/). The fully qualified domain name should resolve to the Forwarding Rules associated with the Terraform Enterprise deployment. Creating the required DNS entry is outside the scope of this guide.

#### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#ssl-tls-certificates-and-load-balancers)SSL/TLS Certificates and Load Balancers

An SSL/TLS certificate signed by a public or private CA is required for secure communication between clients, VCS systems, and the Terraform Enterprise application server. The certificate can be specified during the UI-based installation or in a configuration file used for an unattended installation.

### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#infrastructure-diagram-standalone)Infrastructure Diagram - Standalone

![gcp-infrastructure-diagram](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/assets/RA-TFE-SA-GCP-SingleRegion-de176179.png)

The above diagram shows the infrastructure components at a high-level.

### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#application-layer)Application Layer

The Application Layer is composed of a Regional Managed Instance Group and an Instance Template providing an auto-recovery mechanism in the event of an instance or Zone failure.

### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#storage-layer)Storage Layer

The Storage Layer is composed of multiple service endpoints (Cloud SQL, Cloud Storage) all configured with or benefiting from inherent resiliency provided by GCP.

#### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#additional-information)Additional Information

- [Cloud SQL high-availability](https://cloud.google.com/sql/docs/postgres/high-availability).
- [Regional Cloud Storage](https://cloud.google.com/storage/docs/storage-classes).

## [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#infrastructure-provisioning)Infrastructure Provisioning

The recommended way to deploy Terraform Enterprise is through use of a Terraform configuration that defines the required resources, their references to other resources, and associated dependencies.

## [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#normal-operation)Normal Operation

### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#component-interaction)Component Interaction

The Forwarding Rule routes all traffic to the Terraform Enterprise instance, which is managed by a Regional Managed Instance Group with maximum and minimum instance counts set to one.

The Terraform Enterprise application is connected to the PostgreSQL database via the Cloud SQL endpoint and all database requests are routed via the Cloud SQL endpoint to the database instance.

The Terraform Enterprise application is connected to object storage via the Cloud Storage endpoint for the defined bucket and all object storage requests are routed to the highly available infrastructure supporting Cloud Storage.

### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#monitoring)Monitoring

There is not currently a full monitoring guide for Terraform Enterprise. The following pages include information relevant to monitoring:

- [Logging](https://www.terraform.io/docs/enterprise/admin/logging.html)
- [Diagnostics](https://www.terraform.io/docs/enterprise/support/index.html)
- [Reliability and Availability](https://www.terraform.io/docs/enterprise/system-overview/reliability-availability.html)

### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#upgrades)Upgrades

See [the Upgrades section](https://www.terraform.io/docs/enterprise/admin/upgrades.html) of the documentation.

## [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#high-availability-failure-scenarios)High Availability - Failure Scenarios

GCP provides guidance on [designing robust systems](https://cloud.google.com/compute/docs/tutorials/robustsystems). Working in accordance with those recommendations, the Terraform Enterprise Reference Architecture is designed to handle different failure scenarios with different probabilities. As the architecture evolves it will provide a higher level of service continuity.

### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#terraform-enterprise-server)Terraform Enterprise Server

By utilizing a Regional Managed Instance Group, a Terraform Enterprise instance can automatically recover in the event of any outage except for the loss of an entire region.

In the event of the Terraform Enterprise instance failing in a way that GCP can observe, [Live Migration](https://cloud.google.com/compute/docs/instances/live-migration) is used to move the instance to new physical hardware automatically. In the event that Live Migration is not possible the instance will crash and be restarted on new physical hardware automatically. Once launched, it reinitializes the software, and on completion, processing on this instance will resume as normal.

With *External Services* (PostgreSQL Database, Object Storage) in use, there is still some application configuration data present on the Terraform Enterprise server such as installation type, database connection settings, hostname. This data rarely changes. If the configuration on Terraform Enterprise changes you should update the Instance Template to include the updates so that any newly launched Compute Engine VM uses them.

### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#zone-failure)Zone Failure

In the event of the Zone hosting the main instances (Compute Engine and Cloud SQL) failing, the Regional Managed Instance Group for the Compute VMs will automatically begin booting a new one in an operational Zone.

- Cloud SQL automatically and transparently fails over to the standby zone. The [GCP documentation provides more detail](https://cloud.google.com/sql/docs/postgres/high-availability) on the exact behavior and expected impact.
- Cloud Storage is resilient to Zone failure based on its architecture.

See below for more detail on how each component handles Zone failure.

### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#postgresql-database)PostgreSQL Database

Using Cloud SQL as an external database service leverages the highly available infrastructure provided by GCP. From the GCP website:

> *A Cloud SQL instance configured for high availability is also called a regional instance. A regional instance is located in two zones within the configured region, so if it cannot serve data from its primary zone, it fails over and continues to serve data from its secondary zone. ([source](https://cloud.google.com/sql/docs/postgres/high-availability))*

### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#object-storage)Object Storage

Using Regional Cloud Storage as an external object store leverages the highly available infrastructure provided by GCP. Regional Cloud Storage buckets are resilient to Zone failure within the region selected during bucket creation. From the GCP website:

> *Regional Storage is appropriate for storing data in the same regional location as Compute Engine instances or Kubernetes Engine clusters that use the data. Doing so gives you better performance for data-intensive computations, as opposed to storing your data in a multi-regional location. ([source](https://cloud.google.com/storage/docs/storage-classes))*

## [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#disaster-recovery-failure-scenarios)Disaster Recovery - Failure Scenarios

GCP provides guidance on [designing robust systems](https://cloud.google.com/compute/docs/tutorials/robustsystems). Working in accordance with those recommendations the Terraform Enterprise Reference Architecture is designed to handle different failure scenarios that have different probabilities. As the architecture evolves it will continue to provide a higher level of service continuity.

### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#data-corruption)Data Corruption

The Terraform Enterprise application architecture relies on multiple service endpoints (Cloud SQL, Cloud Storage) all providing their own backup and recovery functionality to support a low MTTR in the event of data corruption.

### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#postgresql-database-1)PostgreSQL Database

Backup and restoration of PostgreSQL is managed by GCP and configured through the GCP management console or CLI.

Automated (scheduled) and on-demand backups are available in GCP. Review the [backup](https://cloud.google.com/sql/docs/postgres/backup-recovery/backups) and [restoration](https://cloud.google.com/sql/docs/postgres/backup-recovery/restore) documentation for further guidance.

More details of Cloud SQL (PostgreSQL) features are available [here](https://cloud.google.com/sql/docs/postgres/).

### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#object-storage-1)Object Storage

There is no automatic backup/snapshot of Cloud Storage by GCP, so it is recommended to script a bucket copy process from the bucket used by the Terraform Enterprise application to a “backup bucket” in Cloud Storage that runs at regular intervals. The [Nearline Storage](https://cloud.google.com/storage/docs/storage-classes#nearline) storage class is identified as a solution targeted more for DR backups. From the GCP website:

> *Nearline Storage is ideal for data you plan to read or modify on average once a month or less. For example, if you want to continuously add files to Cloud Storage and plan to access those files once a month for analysis, Nearline Storage is a great choice. Nearline Storage is also appropriate for data backup, disaster recovery, and archival storage. ([source](https://cloud.google.com/storage/docs/storage-classes#nearline))*

## [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#multi-region-deployment-to-address-region-failure)Multi-Region Deployment to Address Region Failure

Terraform Enterprise is currently architected to provide high availability within a single GCP Region only. It is possible to deploy to multiple GCP Regions to give you greater control over your recovery time in the event of a hard dependency failure on a regional GCP service. In this section, implementation patterns to support this are discussed.

An identical infrastructure should be provisioned in a secondary GCP Region. Depending on recovery time objectives and tolerances for additional cost to support GCP Region failure, the infrastructure can be running (Warm Standby) or stopped (Cold Standby). In the event of the primary GCP Region hosting the Terraform Enterprise application failing, the secondary GCP Region will require some configuration before traffic is directed to it along with some global services such as DNS.

- [Cloud SQL cross-region read replicas](https://cloud.google.com/sql/docs/postgres/replication/cross-region-replicas) can be used in a warm standby architecture. See also [Managing Cloud SQL read replicas](https://cloud.google.com/sql/docs/postgres/replication/manage-replicas).
  - Note that read replicas do not inherently provide high availability in the sense that there can be automatic failover from the primary to the read replica. As described in the above reference, the read replica will need to be promoted to a stand-alone Cloud SQL primary instance. Promoting a replica to a stand-alone Cloud SQL primary instance is an irreversible action, so when the failover needs to be reverted, the database must be restored to an original primary location (potentially by starting it as a read replica and promoting it), and the secondary read replica will need to be destroyed and re-established.
  - GCP now offers a [high availability option for Cloud SQL](https://cloud.google.com/sql/docs/mysql/high-availability) databases which could be incorporated into a more automatic failover scenario.*
- [Cloud SQL database backups](https://cloud.google.com/sql/docs/postgres/backup-recovery/restoring) can be used in a cold standby architecture.
  - GCP now offers a [Point-in-time recovery](https://cloud.google.com/sql/docs/postgres/backup-recovery/pitr) option for Cloud SQL databases which could be incorporated into a backup and recovery scheme with reduced downtime and higher reliability.*
- [Multi-Regional Cloud Storage replication](https://cloud.google.com/storage/docs/storage-classes#multi-regional) must be configured so the object storage component of the Storage Layer is available in multiple GCP Regions.
- DNS must be redirected to the Forwarding Rule acting as the entry point for the infrastructure deployed in the secondary GCP Region.
- Terraform Enterprise in the *Standalone* mode is an Active/Passive model. At no point should more than one Terraform Enterprise instance be actively connected to the same database instance.

\* **Note:** We are investigating incorporating these newer CloudSQL capabilities into this reference architecture, but do not have additional details at this time.

## [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#active-active-implementation-mode)Active/Active Implementation Mode

### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#overview)Overview

As stated previously, the *Active/Active* implementation mode is an extension of the *Standalone* implementation mode that increases the scalability and load capacity of the Terraform Enterprise platform. The same application runs on multiple Terraform Enterprise instances utilizing the same external services in a shared model. The primary architectural and implementation differences for *Active/Active* are:

- It can only be run in the *External Services* mode.
- The additional nodes are active and processing work at all times.
- In an addition to the existing external services, there is a memory cache which is currently implemented with cloud native implementations of Redis. This is used for the processing queue for the application and has been moved from the individual instance to be a shared resource that manages distribution of work.
- There are additional configuration parameters to manage the operation of the node cluster and the memory cache.

The following sections will provide further detail on the infrastructure and implementation differences.

### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#migration-to-active-active)Migration to Active/Active

If you are considering a migration from a *Standalone* implementation to *Active/Active*, it is straightforward and there is guidance available to assist with that effort. However, you should first make a determination if the move is necessary. The *Standalone* mode is capable of handling significant load and the first paths to supporting higher load can be simply increasing the compute power in the existing implementation. A discussion with your HashiCorp representatives may be warranted.

Also note that if your existing architecture does not already depict what is shown and discussed above, you will likely need to make adjustments to bring it into alignment. This could be either before or during the migration. Certain tenets of the reference architecture described here are highly recommended and potentially necessary to support *Active/Active* mode such as load balancers and scaling groups.

### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#infrastructure-diagram-active-active)Infrastructure Diagram - Active/Active

![gcp-aa-infrastructure-diagram](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/assets/RA-TFE-AA-GCP-SingleRegion-d453d5b9.png)

The above diagram shows the infrastructure components of an *Active/Active* implementation at a high-level.

### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#infrastructure-requirements-1)Infrastructure Requirements

#### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#active-nodes)Active Nodes

The diagram depicts two active nodes to be concise. Additional nodes can be added by altering your configuration to launch another instance that points to the same shared external services. The number and sizing of nodes should be based on load requirements and redundancy needs. Nodes should be deployed in alternate zones to accommodate zone failure.

The cluster is comprised of essentially independent nodes in a SaaS type model. There are no concerns of leader election or minimal or optimum node counts. When a new node enters the cluster it simply starts taking new work from the load balancer and from the memory cache queue and thus spreading the load horizontally.

#### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#memory-cache)Memory Cache

The GCP implementation of the memory cache is handled by [Google Cloud Memorystore services](https://https//cloud.google.com/memorystore). Specifically using [Memorystore for Redis](https://https//cloud.google.com/memorystore/docs/redis).

[Memorystore for Redis Overview](https://cloud.google.com/memorystore/docs/redis/redis-overview) provides a high level description of the implementation options for the memory cache. A primary differentiator is Basic Tier and Standard Tier. The primary difference is that the Standard Tier offers [high availability](https://cloud.google.com/memorystore/docs/redis/high-availability)] where instances are always replicated across zones and provides 99.9% availability SLAs (note that reading from a replica is not supported). A lower testing or sandbox environment could use the Basic Tier, however, a production level environment should always use Standard Tier to gain the HA features that coincide with the other external services in the Terraform Enterprise platform.

Memorystore for Redis service supports [realtime scaling of instance size](https://cloud.google.com/memorystore/docs/redis/scaling-instances). You can start the size off in a smaller range with some consideration of anticipated active load, and scale up or down as demand is understood with the aid of [monitoring ](https://cloud.google.com/memorystore/docs/redis/monitoring-instances).

Enterprise-grade security is inherently covered in the Memorystore for Redis implementation because Redis instances are protected from the Internet using private IPs, and access to instances is controlled and limited to applications running on the same Virtual Private Network as the Redis instance. Additional security measures can be instituted using [IAM based access control and permissions](https://cloud.google.com/memorystore/docs/redis/access-control). However, this may add additional complication to your realtime scaling of instances.

Terraform Enterprise supports Redis versions 4.0 and 5.0, but 5.0 is recommended unless there is strong reason to deviate. Memorystore for Redis supports 4.0 and 5.0 also so do explicitly specify the version.

### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#normal-operation-1)Normal Operation

#### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#component-interaction-1)Component Interaction

The Forwarding Rule routes traffic to the Terraform Enterprise node instances, which is managed by a Regional Managed Instance Group. This is a standard round-robin distribution for now, with no accounting for current load on the nodes. The instance counts on the Regional Managed Instance Group control the number of nodes in operation and can be used to increase or decrease the number of active nodes.

*Active/Active* Terraform Enterprise is not currently architected to support dynamic scaling based on load or other factors. The maximum and minimum instance counts on the Regional Managed Instance Group should be set to the same value. Adding a node can be done at will by setting these values. However, removing a node requires that the node be allowed to finish active work and stop accepting new work before being terminated. The operational documentation has the details on how to "drain" a node.

#### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#replicated-console)Replicated Console

The Replicated Console that allows access to certain information and realtime configuration for *Standalone* is not available in *Active/Active*. This functionality, including generating support bundles, has been replaced with CLI commands to be executed on the nodes. The operational documentation has the details on how to utilize these commands.

#### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#upgrades-1)Upgrades

Upgrading the Terraform Enterprise version still follows a similar pattern as with *Standalone*. However, there is not an online option with the Replicated Console. It is possible to upgrade a minor release with CLI commands in a rolling fashion. A "required" release or any change the potentially affects the shared external services will need to be done with a short outage. This involves scaling down to a single node, replacing that node, and then scaling back out. The operational documentation has the details on how these processes can operate.

### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#failure-scenarios)Failure Scenarios

#### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#memory-cache-1)Memory Cache

As mentioned, the Memorystore for Redis service in Standard Tier mode provides automatic replication and failover. In the event of a larger failure or any normal maintenance with proper draining, the memory cache will not be required to be restored. If it is damaged it can be re-paved, and if not it can be left to continue operation.

### [»](https://www.terraform.io/docs/enterprise/before-installing/reference-architecture/gcp.html#multi-region-implementation-to-address-region-failure)Multi-Region Implementation to Address Region Failure

Similar to *Standalone*, *Active/Active* Terraform Enterprise is currently architected to provide high availability within a single region. You cannot deploy additional nodes associated to the primary cluster in different regions. It is possible to deploy to multiple regions to give you greater control over your recovery time in the event of a hard dependency failure on a regional service. An identical infrastructure will still need to be instantiated separately with a failover scenario resulting in control of processing being transferred to the second implementation, as described in the earlier section on this topic. In addition, this identical infrastructure will require its own memory cache external service instance.

# Module Review

## Module 3 Wrap Up: Automation in the Cloud

Over the past few videos we've learned how to use the different Cloud resources available to us. We've gone through a bunch of different concepts like software or infrastructure-as-a-service, public or hybrid clouds, upscaling and downscaling, and a lot more. We've also demonstrated how to deploy single virtual machines and then turn them into a customized VM template. Creating a single VM can be useful for small to medium-sized organizations with lower technical requirements. But as the technical requirements for the organization grows, it's often necessary to deploy more and larger Cloud solutions. This is where using the template to create large system clusters becomes very handy. Using reference images and templating lets us clone a VM 100, 1,000, or more times, and this makes scaling our Cloud deployments super easy. We checked out a bunch of different ways to interact with the platform. We've seen how we can use both the web interface and the command line tool to create virtual machines in the Cloud. Using these tools we can control which machines are online or offline, modify their configuration, and a bunch of other things. At a small or medium scale, using these tools can be really effective. At a larger scale, we have to automate these deployments even further and that's where orchestration comes into play. Tools like Terraform let us define our Cloud infrastructure as code, allowing us to have a lot of control over how the infrastructure is managed, how the changes are applied, and so on. This lets us combine the power of using infrastructure as code with the flexibility of using Cloud resources. Hopefully by now, you're starting to see how you can make the best out of the different Cloud offerings to help your IT infrastructure quickly and easily scale as needed. Up next, you'll have the opportunity to practice all of this in the next lab. Instead of relying on the Quick Labs infrastructure to set up all the VMS for you, you'll be doing the setup yourself. Exciting, right?

# Building Software for the Cloud

## Intro to Module 4: Managing Cloud Instances at Scale

Welcome back. And guess what? This is the last module in the course. Congratulations on making it here. It's sure been an exciting ride and it's about to get even more interesting. As we've learned in the past modules Cloud providers offer us a bunch of different services. By now we've learned a lot about different hosting models. If you're working for a small company you might get by with pre-packaged applications offered in the software as a service model. But as the organization grows so to do the IT needs. Eventually, your company might grow so large you need to start developing your own applications based on the platforms and infrastructure models from Cloud providers. Why might you develop your own application? Well developing your own apps gives your IT team more control and flexibility over what the applications do but it also brings a new set of challenges. You'll need to figure out how the different pieces fit together, make sure that the services run reliably and troubleshoot problems when they come up. In the next few videos, we'll check out some of the options for building software for the Cloud. We'll look into the different types of storage available and how to decide which one to use. We'll also learn more about load balancing and how to distribute a service across many instances. We'll discuss how we can make changes to our systems without breaking everything. And we'll check out some of the limitations that you might run into when running software in the Cloud. We'll wrap up with some best practices for running reliable services. This includes measuring how your service is doing by using a monitoring system and also setting up alerts so you're automatically notified if things don't go as planned. Sometimes systems fail and that's okay. Using the tips you'll learn in this module you'll be prepared to deal with failure and troubleshoot issues when using Cloud services. Once we're done you'll get the chance to debug and fix a problem with an application running in the Cloud. Exciting stuff, right? There's a lot more ground to cover so let's dive in.

## Storing Data in the Cloud

Almost all IT systems need to store some data. Sometimes, it's a lot of data, sometimes, it's only bits and pieces of information. Cloud providers give us a lot of storage options. Picking the right solution for data storage will depend on what service you're building. You'll need to consider a bunch of factors, like; how much data you want to store, what kind of data that is, what geographical locations you'll be using it in, whether you're mostly writing or reading the data, how often the data changes, or what your budget is. This might sound like a lot of things to consider, but don't worry, it's not that bad. We'll check out some of the most common solutions offered by Cloud providers to give you a better idea of when to choose what. When choosing a storage solution in the Cloud, you might opt to go with the traditional storage technologies, like block storage, or you can choose newer technologies, like object or blob storage. Let's check out what each of these mean. As we saw in an earlier video, when we create a VM running in the Cloud, it has a local disk attached to it. These local disks are an example of block storage. This type of storage closely resembles the physical storage that you have on physical machines using physical hard drives. Block storage in the Cloud acts almost exactly like a hard drive. The operating system of the virtual machine will create and manage a file system on top of the block storage just as if it were a physical drive. There's a pretty cool difference though. These are virtual disks, so we can easily move the data around. For example, we can migrate the information on the disk to a different location, attach the same disk image to other machines, or create snapshots of the current state. All of this without having to ship a physical device from place to place. Our block storage can be either persistent or ephemeral. Persistent storage is used for instances that are long lived, and need to keep data across reboots and upgrades. On the flip side, ephemeral storage is used for instances that are only temporary, and only need to keep local data while they're running. Ephemeral storage is great for temporary files that your service needs to create while it's running, but you don't need to keep. This type of storage is especially common when using containers, but it can also be useful when dealing with virtual machines that only need to store data while they're running. In typical Cloud setups, each VM has one or more disks attached to the machine. The data on these disks is managed by the OS and can't be easily shared with other VMs. If you're looking to share data across instances, you might want to look into some shared file system solutions, that Cloud providers offer using the platform as a service model. When using these solutions, the data can be accessed through network file system protocols like NFS or CIFS. This lets you connect many different instances or containers to the same file system with no programming required. Block storage and shared file systems work fine when you're managing servers that need to access files. But if you're trying to deploy a Cloud app that needs to store application data, you'll probably need to look into other solutions like objects storage, which is also known as blob storage. Object storage lets you place in retrieve objects in a storage bucket. These objects are just generic files like photos or cat videos, encoded and stored on disk as binary data. These files are commonly called blobs, which comes from binary large object, and as we called out, these blobs are stored in locations known as buckets. Everything that you put into a storage bucket has a unique name. There's no file system. You place an object into storage with a name, and if you want that object back, you simply ask for it by name. To interact with an object store, you need to use an API or special utilities that can interact with the specific object store that you're using. On top of this, we've called out in earlier videos that most Cloud providers offer databases as a service. These come in two basic flavors, SQL and NoSQL. SQL databases, also known as relational, use the traditional database format and query language. Data is stored in tables with columns and rows that can be indexed, and we retrieve the data by writing SQL queries. A lot of existing applications already use this model, so it's typically chosen when migrating an existing application to the Cloud. NoSQL databases offer a lot of advantages related to scale. They're designed to be distributed across tons of machines and are super fast when retrieving results. But instead of a unified query language, we need to use a specific API provided by the database. This means that we might need to rewrite the portion of the application that accesses the DB. When deciding how to store your data, you'll also have to choose a storage class. Cloud providers typically offer different classes of storage at different prices. Variables like performance, availability, or how often the data is accessed will affect the monthly price. The performance of a storage solution is influenced by a number of factors, including throughput, IOPS, and latency. Let's check out what these mean. Throughput is the amount of data that you can read and write in a given amount of time. The throughput for reading and writing can be pretty different. For example, you could have a throughput of one gigabyte per second for reading and 100 megabytes per second for writing. IOPS or input/output operations per second measures how many reads or writes you can do in one second, no matter how much data you're accessing. Each read or write operation has some overhead. So there's a limit on how many you can do in a given second, and latency is the amount of time it takes to complete a read or write operation. This will take into account the impact of IOPS, throughput and the particulars of the specific service. Read latency is sometimes reported as the time it takes a storage system to start delivering data after a read request has been made, also known as time to first byte. While write latency is typically measured as the amount of time it takes for a write operation to complete. When choosing the storage class to use, you might come across terms like hot and cold. Hot data is accessed frequently and stored in hot storage while cold data is accessed infrequently, and stored in cold storage. These two storage types have different performance characteristics. For example, hot storage back ends are usually built using solid state disks, which are generally faster than the traditional spinning hard disks. So how do you choose between one and the other? Say you want to keep all the data you're service produces for five years, but you don't expect to regularly access data older than one year. You might choose to keep the last one year of data in hot storage so you have fast access to it, and after a year, you can move your data to cold storage where you can still get to it, but it will be slower and possibly costs more to access. There's a lot more to say about storage in the Cloud. It's really quite a hot topic, but we won't go into more detail here. We'll provide links to more info in the next reading in case you want to learn more. Up next, we're going to look at a different Cloud scale characteristic that we've already touched on using multiple machines for the same service.

## Load Balancing

In earlier videos, we saw a bunch of different reasons why we might want more than one machine or container running our service. For example, we might want to horizontally scale our service to handle more work, distribute instances geographically to get closer to our users. Or have backup instances to keep the service running if one or more of the instances fail. No matter the reason, we use orchestration tools and techniques to make sure that the instances are repeatable. And once we've set up replicated machines, we'll want to distribute the requests across instances. We called out earlier that this is where load balancing comes into play. Let's take a closer look at the different load balancing methods that we can use. A pretty common load balancing technique is round robin DNS. Round robin is a really common method for distributing tasks. Imagine you're giving out treats at a party. First, you make sure that each of your friends gets one cookie. Then you give everyone a second serving and so on until all of the treats are gone or your guests say, thank you, they're full. That's the round-robin approach to eating all the cookies. Now, if we want to translate a URL like my service.example.com into an IP address, we use the DNS protocol or domain name system. In the simplest configuration, the URL always gets translated into exactly the same IP address. But when we configure our DNS to use round robin, it'll give each client asking for the translation a group of IP addresses in a different order. The clients will then pick one of the addresses to try to reach the service. If an attempt fails, the client will jump to another address on the list.

This load balancing method is super easy to set up. You just need to make sure that the IPs of all machines in the pool are configured in your DNS server, but it has some limitations. First, you can't control which addresses get picked by the clients. Even if a server is overloaded, you can't stop the clients from reaching out to it. On top of that, DNS records are cached by the clients and other servers. So if you need to change the list of addresses for the instances, you'll have to wait until all of the DNS records that were cached by the clients expire. There's got to be a better way, right? Well, there sure is. To have more control over how the load's distributed and to make faster changes, we can set up a server as a dedicated load balancer. This is a machine that acts as a proxy between the clients and the servers. It receives the requests and based on the rules that we provide, it directs them to the selected back-end server.

Load balances can be super simple or super complex depending on the service needs. Say your service needs to keep track of the actions that a user has taken up till now. In this case, you'll want your load balancer to use sticky sessions. Using sticky sessions means all requests from the same client always go to the same back end server. This can be really useful for services than need it but can also cause headaches when migrating or maintaining your service. So you need to use it only if you really need it. 

Otherwise, you'll end up in a really sticky situation. Another cool feature of load balancers is that you can configure them to check the health of the backend servers. Typically, we do this by making a simple query to the servers and checking that the reply matches the expected reply. If a back-end server is unhealthy, the load balancer will stop sending new requests to it to keep only healthy servers in the pool. As we've called out a few times already, a cool feature of cloud infrastructure is how easily we can add or remove machines from a pool of servers providing a service. If we have a load balancer controlling the load of the machines, adding a new machine to the pool is as easy as creating the instance. And then letting the load balancer know that it can now route traffic to it. We can do this by manually creating and adding the instance or when our services under heavy load, we can just let the auto scaling feature do it. Cool, right? Okay, so imagine that you've built out your service with load balancers and you're receiving requests from all over the world.

How do you make sure that clients connect to the servers that are closest to them? You can use Geo DNS and geoip.

These are DNS configurations that will direct your clients to the closest geographical load balancer. The mechanism used to route the traffic relies on how the DNS servers respond to requests. For example, from machines hosted in North America, a DNS server in North America might be configured to respond with the IPs in, you guessed it, North America. It can be tricky to set this up on your own but most Cloud providers offer it as part of their services making it much easier to have a geographically distributed service. Let's take this one step further. There are some providers dedicated to bringing the contents of your services as close to the user as possible. These are the content delivery networks or CDNs. They make up a network of physical hosts that are geographically located as close to the end user as possible.

This means that CDN servers are often in the same data center as the users Internet service provider. CDNs work by caching content super close to the user. When a user requests say, a cute cat video, it's stored in the closest CDN server. That way, when a second user in the same region requests the same cat video, it's already cached in a server that's pretty close and it can be downloaded extra fast. Because no one should have to wait for their cat videos to load.

You now know a lot of stuff about load-balancing. Up next, we'll talk about another aspect of dealing with cloud services. How to deploy changes safely to our cloud service?

## Change Management

You've come a long way. You now know how to get your service running in the cloud. Next, let's talk about how to keep it running. Most of the time when something stops working, it's because something changed. If we want our cloud service to be stable, we might be tempted to avoid changes altogether. But change is a fact of cloud life. If we want to fix bugs and improve features in our services, we have to make changes. But we can make changes in a controlled and safe way. This is called change management, and it's what lets us keep innovating while our services keep running. Step one in improving the safety of our changes, we have to make sure they're well-tested. This means running unit tests and integration tests, and then running these tests whenever there's a change. In an earlier course, we briefly mentioned continuous integration, or CI, but here's a refresher. A continuous integration system will build and test our code every time there's a change.

Ideally, the CI system runs even for changes that are being reviewed. That way you can catch problems before they're merged into the main branch. You can use a common open source CI system like Jenkins, or if you use GitHub, you can use its Travis CI integration. Many cloud providers also offer continuous integration as a service. Once the change has committed, the CI system will build and test the resulting code. Now you can use continuous deployment, or CD, to automatically deploy the results of the build or build artifacts. Continuous deployment lets you control the deployment with rules. For example, we usually configure our CD system to deploy new builds only when all of the tests have passed successfully.

On top of that, we can configure our CD to push to different environments based on some rules. What do we mean by that? In an earlier video, we mentioned that when pushing puppet changes, we should have a test environment separate from the production environment.

Having them separate lets us validate that changes work correctly before they affect users. Here environment means everything needed to run the service. It includes the machines and networks used for running the service, the deployed code, the configuration management, the application configurations, and the customer data. Production, usually shortened to prod, is the real environment, the ones users see and interact with. Because of this, we have to protect, love, and nurture a prod. The test environment needs to be similar enough to prod that we can use them to check our changes work correctly. You could have your CD system configured to push new changes to the test environment. You can then check that the service is still working correctly there, and then manually tell your deployment system to push those same changes to production.

If the service is complex and there are a bunch of different developers making changes to it, you might set up additional environments where the developers can test their changes in different stages before releasing them. For example, you might have your CD system push all new changes to a development or dev environment, then have a separate environment called pre-prod, which only gets specific changes after approval. And only after a thorough testing, these changes get pushed to pro. Say you're trying to increase the efficiency of your surface by 20%, but you don't know if the change you made might crash part of your system.

You want to deploy it to one of those testing or development environments to make sure it works correctly before you ship it to prod.

Remember, these environments need to be as similar to prod as possible. They should be built and deployed in the same way. And while we don't want them to be breaking all the time, it's normal for some changes to break dev or even pre-prod. We're just happy that we can catch them early so that they don't break prod. Sometimes you might want to experiment with a new service feature. You've tested the code, you know it works, but you want to know if it's something that's going to work well for your users. When you have something that you want to test in production with real customers, you can experiment using A/B testing. In A/B testing, some requests are served using one set of code and configuration, A, and other requests are served using a different set of of code and configuration, B. This is another place where a load balancer and instance groups can help us out. You can deploy one instance group in your A configuration and a second instance group in your B configuration. Then by changing the configuration of the load balancer, you can direct different percentages of inbound requests to those two configurations. If your A configuration is today's production configuration and your B configuration is something experimental, you might want to start by only directing 1 % of your requests to B. Then you can slowly ramp up the percentage that you check out whether the B configuration performs better than A, or not. Heads up, make sure you have basic monitoring so that it's easy to tell if A or B is performing better or worse. If it's hard to identify the back-end responsible for serving A requests or B requests, then much of the value of A/B testing is lost to A/B debugging. So what happens if all the precautions we took aren't enough and we break something in production? Remember what we discussed in an earlier course about post-mortems. We learn from failure and we build the new knowledge into our change management.

Ask yourself, what did I have to do to catch the problem? Can I have one of my change management systems look for problems like that in the future? Can I add a test or a rule to my unit tests, my CI/CD system, or my service health checks to prevent this kind of failure in the future? So remember, if something breaks, give yourself a break. Sometimes in IT, these things happen, no matter how careful you are. And as you use and refine your change management systems and skills, you'll gain the confidence to make changes to your service more quickly and safely.

## Understanding Limitations

We've spent a while talking about how to make your service runs smoothly in the Cloud, now let's take a moment to talk about some of the problems that you might come across. Personally, I find that when writing software to run on the Cloud, it's important to keep in mind how my application will be deployed. The software I'm creating needs to be fault tolerant and capable of handling unexpected events. Instances might be added or removed from the pool as needed and if an individual machine crashes, my service needs to breeze along without introducing problems, and not every problem results in a crash, sometimes we run into quotas or limits, meaning that you can only perform a certain number of operations within a certain time period. For example, when using Blob Storage there might be a limit of 1,000 writes to the same blob in a given seconds. If your service performs a lot of these operations routinely, it might get blocked by these limits. In that case, you'll need to see if you can change the way you're doing the operations, for example by grouping all of the calls into one batch. Switching to a different service is sometimes an option too. Some API calls used in Cloud services can be expensive to perform, so most Cloud providers will enforce rate limits on these calls to prevent one service from overloading the whole system. For example, there might be a rate limit of one call per second for an expensive API call. On top of that, there are also utilization limits, which cap the total amount of a certain resource that you can provision. These quotas are there to help you avoid unintentionally allocating more resources than you wanted. Imagine you've configured your service to use auto scaling and it suddenly receives a huge spike in traffic. This could mean a lot of new instances getting deployed which can cost a lot of money. For some of these limits, you can ask for a quota increase from the Cloud provider if you want additional capacity, and you can also set a smaller quota in the default to avoid overspending. This can be a great idea when you're running a service on a tight budget. If your service performance expensive operations routinely, you should make sure you understand the limitations of the solution that you choose. A lot of platform as a service and infrastructure as a service offerings have costs directly related to how much they're used. They also have usage quotas. If the service you've built suddenly becomes very popular, you can run out of quota or run out of budget. By imposing a quota on an auto-scaling system, the system will grow to meet user demand until it reaches the configured limit. The trick here is to have good monitoring and alerting around behavior like this. If your system runs out of quota but there's an increased demand for a puppy videos, the system may have problems, degraded performance or worse yet an outage. So you want to be notified as soon as it happens that you can decide whether to increase your quota or not. Finally, let's talk about dependencies. When your service depends on a Platform as a Service offering like a hosted database or CICD system, you're handing the responsibility for maintenance and upgrades of that service off to your Cloud provider, that's great, fewer things to worry about and maintain, but it also means that you don't always get to choose what version of that software you're using. You might find yourself on either side of the upgrade cycle, either wanting to stay at a version that's working well for you or wanting the Cloud provider to hurry up and upgrade to resolve a bug that's affecting your service. Your Cloud provider has a strong incentive to keep its service software fairly up-to-date. Keeping software as a service solutions up to date ensures that customers aren't vulnerable to security flaws, that bugs are promptly fixed and that new features get released early. At the same time, the Cloud provider has to move carefully and test changes to keep destruction of its service to a minimum. They will communicate proactively about changes to the services that you use and in some cases, Cloud providers might give you access to early versions of these services. For example, you can set up a test environment for your service that uses the beta or prerelease version of a given software as a service solution, letting you test it before it impacts production. Hopefully, you're starting to get an idea of the trade-offs that you'll need to make to get the most from deploying your software to the Cloud. Now, head on over to the reading for links to additional information on all of this, then there's a quick quiz for you.

# Resource quotas in GCP

Compute Engine enforces [quotas](https://cloud.google.com/docs/quota) on resource usage for a variety of reasons. For example, quotas protect the community of Google Cloud users by preventing unforeseen spikes in usage. Google Cloud also offers [free trial quotas](https://cloud.google.com/free-trial/docs/free-trial-quotas) that provide limited access for projects to help you explore Google Cloud on a free trial basis.

Not all projects have the same quotas. As your use of Google Cloud expands over time, your quotas might increase accordingly. If you expect a notable upcoming increase in usage, you can proactively [request quota](https://cloud.google.com/compute/quotas#requesting_additional_quota) adjustments from the [**Quotas**](https://console.cloud.google.com/iam-admin/quotas) page in the Cloud Console.

**Important**:If you're using the [Google Cloud free trial](https://cloud.google.com/free/docs/gcp-free-tier#free-trial), you can't request a change to your quota.If your project's billing service is disrupted, your quota is reset to its default value.

## Permissions for checking and editing quota

To view your quotas, you must have `serviceusage.quotas.get` permission.
To change your quotas, you must have `serviceusage.quotas.update` permission.
This permission is included by default for the following [Basic roles](https://cloud.google.com/iam/docs/understanding-roles): Owner, Editor, and Quota Administrator.

## Checking your quota

Each project's quota is different. For information about VM instances quota, see [VM instances](https://cloud.google.com/compute/quotas#vm_instance_quota), later in this document.

To check the available quota for a project, go to the [**Quotas**](https://console.cloud.google.com/iam-admin/quotas) page in the Google Cloud Console.

To use the `gcloud` command-line tool, run the following command to check project-wide quotas:

```
gcloud compute project-info describe --project PROJECT_ID
```

Replace PROJECT_ID with your own project ID.

Note that the results don't list per-region quotas. To list quotas in a region, run:

```
gcloud compute regions describe REGION
```

Replace REGION with the name of the region where you want a list of quota information.

## Requesting an increase in quota

Request changes to quota from the [**Quotas**](https://console.cloud.google.com/iam-admin/quotas) page in the Cloud Console. There is no charge for requesting a quota increase. Your costs increase only if you use more resources.

1. In the Google Cloud Console, go to **Quotas** on the **IAM & Admin** page.

   [Go to Quotas](https://console.cloud.google.com/iam-admin/quotas)

The most efficient way to see your quotas is to use the **Filter table**.

1. Open the filter_list **Filter table** and select **Limit name:** to search for the quota you want to adjust.
2. Select the **Service** for which you want to adjust your quota.
3. Make your selection from the drop-down options.
4. Edit your quota limit.
5. Click **SAVE**.

A request to decrease quota is rejected by default. If you must reduce your quota, reply to the support email with an explanation of your requirements. A support representative from the Compute Engine team will respond to your request within 24 to 48 hours.

Plan and request additional resources at least a few days in advance to ensure that there is enough time to fulfill your request.

## Quotas and resource availability

Resource quotas are the maximum number of resources you can create of that resource type, if those resources are available. Quotas do not guarantee that resources are available at all times. If a resource is not available, or if the region you choose is out of the resource, you can't create new resources of that type, even if you have remaining quota in your region or project. For example, you might still have quota to create external IP addresses in `us-central1`, but there might not be available IP addresses in that region.

Similarly, even if you have a regional quota, a resource might not be available in a specific zone. For example, you might have quota in region `us-central1` to create VM instances, but you might not be able to create VM instances in the zone `us-central1-a` if the zone is depleted. In such cases, try creating the same resource in another zone, such as `us-central1-f`. To learn more about your options if zonal resources are depleted, see [General troubleshooting](https://cloud.google.com/compute/docs/troubleshooting/troubleshooting-instances#vm-not-created).

## Understanding quotas

When planning your virtual machine (VM) instance needs, there are a number of quotas to consider that affect how many VM instances you can create.

### Regional and global quotas

VM quotas are managed at the regional level. VM instance, instance group, CPU, and disk quotas can be consumed by any VM in the region, regardless of zone. For example, CPU quota is a regional quota, so there is a different limit and usage count for each region. To launch an `n2-standard-16` instance in any zone in the `us-central1` region, you need enough quota for at least 16 CPUs in `us-central1`.

Networking and load balancing quotas are required to create firewalls, load balancers, networks, and VPNs. These are global quotas that do not depend on a region. Any region can use a global quota. For example, in-use and static external IP addresses assigned to load balancers and HTTP(S) proxies consume global quotas.

### CPU quota

CPU quota is the total number of virtual CPUs across all of your VM instances in a region. CPU quotas apply to running instances and instance reservations. Both predefined and [preemptible instances](https://cloud.google.com/compute/docs/instances/preemptible) consume this quota.

To protect Compute Engine systems and other users, some new accounts and projects also have a global `CPUs (All Regions)` quota that applies to all regions and is measured as a sum of all your vCPUs in all regions.

For example, if you have 48 vCPUs remaining in a single region such as `us-central1` but only 32 vCPUs remaining for the `CPUs (All Regions)` quota, you can launch only 32 vCPUs in the `us-central1` region, even though there is remaining quota in the region. This is because you will reach the `CPU (All Regions)` quota and need to delete existing instances before you can launch new instances.

E2 and N1 machine types share a CPU quota pool. N2, N2D, M1, M2, and C2 machine types have unique, separate CPU quota pools. You must have committed use discount quota before you purchase a committed use discount contract.

| Machine type    | Quota pool    | CPU quota name     | Committed CPU quota name          |
| :-------------- | :------------ | :----------------- | :-------------------------------- |
| E2, N1          | shared pool   | `CPUS`             | `Committed_CPUS`                  |
| N2              | separate pool | `N2_CPUS`          | `Committed_N2_CPUS`               |
| N2D             | separate pool | `N2D_CPUS`         | `Committed_N2D_CPUS`              |
| M1              | separate pool | `M1_CPUS`          | `Committed_MEMORY-OPTIMIZED_CPUS` |
| M2              | separate pool | `M2_CPUS`          | `Committed_MEMORY-OPTIMIZED_CPUS` |
| C2              | separate pool | `C2_CPUS`          | `Committed_C2_CPUS`               |
| A2              | separate pool | `A2_CPUS`          | `Committed_A2_CPUS`               |
| Preemptible VMs | shared pool   | `PREEMPTIBLE_CPUS` | Not available for preemptible VMs |

### GPU quota

Similar to virtual CPU quota, GPU quota refers to the total number of virtual GPUs in all VM instances in a region. Check the [quotas page](https://console.cloud.google.com/iam-admin/quotas) to ensure that you have enough GPUs available in your project, and to request a quota increase. In addition, new accounts and projects have a global GPU quota that applies to all regions.

When you request a GPU quota, you must request a quota for the GPU models that you want to create in each region, and an additional global quota for the total number of GPUs of all types in all zones.

| NVIDIA | GPU quota name     | Committed GPU quota name     | Virtual workstation    | Preemptible GPUs               | Preemptible GPU virtual workstation |
| :----- | :----------------- | :--------------------------- | :--------------------- | :----------------------------- | :---------------------------------- |
| K80    | `NVIDIA_K80_GPUS`  | `COMMITTED_NVIDIA_K80_GPUS`  | N/A                    | `PREEMPTIBLE_NVIDIA_K80_GPUS`  | N/A                                 |
| P100   | `NVIDIA_P100_GPUS` | `COMMITTED_NVIDIA_P100_GPUS` | `NVIDIA_P100_VWS_GPUS` | `PREEMPTIBLE_NVIDIA_P100_GPUS` | `PREEMPTIBLE_NVIDIA_P100_VWS_GPUS`  |
| A100   | `NVIDIA_A100_GPUS` | `COMMITTED_NVIDIA_A100_GPUS` | `N/A`                  | `PREEMPTIBLE_NVIDIA_A100_GPUS` | `N/A`                               |
| P4     | `NVIDIA_P4_GPUS`   | `COMMITTED_NVIDIA_P4_GPUS`   | `NVIDIA_P4_VWS_GPUS`   | `PREEMPTIBLE_NVIDIA_P4_GPUS`   | `PREEMPTIBLE_NVIDIA_P4_VWS_GPUS`    |
| T4     | `NVIDIA_T4_GPUS`   | `COMMITTED_NVIDIA_T4_GPUS`   | `NVIDIA_T4_VWS_GPUS`   | `PREEMPTIBLE_NVIDIA_T4_GPUS`   | `PREEMPTIBLE_NVIDIA_T4_VWS_GPUS`    |
| V100   | `NVIDIA_V100_GPUS` | `COMMITTED_NVIDIA_V100_GPUS` | N/A                    | `PREEMPTIBLE_NVIDIA_V100_GPUS` | N/A                                 |

### VM instances

The VM instances quota is a regional quota and limits the number of VM instances that can exist in a given region, regardless of whether the VM is running or not. This quota is visible in the Google Cloud Console on the **Quotas** page. It is set automatically by Compute Engine to be 10x your regular CPU quota. You do not need to request this quota. If you need quota for more VM instances, request more [CPUs](https://cloud.google.com/compute/quotas#cpu-quota) because having more CPUs increases VM instance quota. The quota applies to both running and non-running VMs, and to normal and preemptible instances.

1. In the Google Cloud Console, go to **Quotas** on the **IAM & Admin** page.

   [Go to Quotas](https://console.cloud.google.com/iam-admin/quotas)

2. Open the filter_list **Filter table** and select **Service**.

3. Choose **Compute Engine API**.

4. Choose **Limit Name: VM instances**.

5. Click **All Quotas** to see a list of your VM instance quotas by region. Your region quotas are listed from highest to lowest usage.

6. Click the checkbox of the region whose quota you want to change.

7. Click create **EDIT QUOTAS**.

8. Complete the form.

9. Click **SUBMIT REQUEST**.

### Quotas for preemptible resources

To use preemptible CPUs or GPUs attached to preemptible VM instances, or to use local SSDs attached to preemptible VM instances, you must have available quota in your project for the respective resource.

You can [request](https://cloud.google.com/compute/quotas#requesting_additional_quota) special preemptible quotas for: `Preemptible CPUs`, `Preemptible GPUs`, or `Preemptible Local SSDs (GB)`. However, if your project does not have preemptible quota, you can still use the regular quota to launch preemptible resources.

After Compute Engine grants you preemptible quota in a region, all preemptible instances automatically count against preemptible quota.

### Disk quotas

The following persistent disk and local SSD quotas apply on a per-region basis:

- `Local SSD (GB)`. This is the total combined size of [local SSD](https://cloud.google.com/compute/docs/disks/local-ssd) disk partitions that can be attached to VMs in a region. Local SSD is a fast, ephemeral disk that should be used for scratch, local cache, or processing jobs with high fault tolerance because the disk is not intended to survive VM instance reboots. Local SSD partitions are sold in increments of 375 GB and up to 24 local SSD partitions can be attached to a single VM. In the `gcloud` tool and the API, this is referred to as `LOCAL_SSD_TOTAL_GB`.
- `Persistent disk standard (GB)`. This is the total size of [standard persistent disks](https://cloud.google.com/compute/docs/disks#pdspecs) that can be created in a region. As described in [Optimizing persistent disk and local SSD performance](https://cloud.google.com/compute/docs/disks/performance), standard persistent disks offer lower IOPS and throughput than SSD persistent disks or local SSD. It is cost effective when used as large durable disks for storage, as boot disks, and for serial write processes like logs. Standard persistent disks are durable and are available indefinitely to attach to a VM within the same zone. In the `gcloud` tool and the API, this is referred to as `DISKS_TOTAL_GB`. This quota also applies to [regional standard persistent disks](https://cloud.google.com/compute/docs/disks#repds), but regional disks consume twice the amount of quota per GB due to replication in two zones within a region.
- `Persistent disk SSD (GB)`. This is the total combined size of [SSD-backed persistent disks](https://cloud.google.com/compute/docs/disks) partitions that can be created in a region. SSD-backed persistent disks have multiple replicas and, as described in [Block storage performance](https://cloud.google.com/compute/docs/disks/performance), offer higher IOPS and throughput than standard persistent disks. SSD-backed persistent disks are available indefinitely to attach to a VM within the same zone. In the `gcloud` tool and the API, this is referred to as `SSD_TOTAL_GB`. This quota is separate from local SSD. This quota applies to the [disk types](https://cloud.google.com/compute/docs/disks#disk-types) listed below. [Regional persistent disks](https://cloud.google.com/compute/docs/disks#repds) consume twice the amount of quota per GB due to replication in two zones within a region.
  - Zonal and regional SSD persistent disk
  - Zonal and regional balanced persistent disk

### External IP addresses

You must have enough external IP addresses for every VM that needs to be directly reachable from the public internet. Regional IP quota is for assigning IPv4 addresses to VMs in that region. Global IP quota is for assigning IPv4 addresses to global networking resources such as load balancers. Google Cloud offers different types of IP addresses, depending on your needs. For information about costs, refer to [External IP address pricing](https://cloud.google.com/vpc/network-pricing#ipaddress). For information about quota specifics, see [Quotas and limits](https://cloud.google.com/vpc/docs/quota).

- **In-use external IP addresses**. Includes both ephemeral and static IP addresses that are currently being used by a resource.
- **Static External IP addresses**: External IP addresses reserved for your resources that persist through machine restarts. You can register these addresses with DNS and domain provider services to provide a user-friendly address. For example, www.example-site.com.
- **Static Internal IP addresses:** Static internal IP addresses provide the ability to reserve internal IP addresses from the internal IP range configured in the subnet. You can assign those reserved internal addresses to resources as needed.

### Instance groups

To use instance groups, you must have available quota for all of the resources that the group will use (for example, CPU quota) as well as available quota for the group resource itself. Depending on the type of group that you create, the following group resource quotas apply:

| Service type                                 | Service quota                                      |
| :------------------------------------------- | :------------------------------------------------- |
| Regional (multi-zone) managed instance group | `Regional instance group managers`                 |
| Zonal (single-zone) managed instance group   | Both of:`Instance group managers``Instance groups` |
| Unmanaged (single-zone) instance group       | `Instance groups`                                  |
| Regional (multi-zone) autoscaler             | `Regional autoscalers`                             |
| Zonal (single-zone) autoscaler               | `Autoscalers`                                      |

# AWS service quotas

Your AWS account has default quotas, formerly referred to as limits, for each AWS service. Unless otherwise noted, each quota is Region-specific. You can request increases for some quotas, and other quotas cannot be increased.

Service Quotas is an AWS service that helps you manage your quotas for over 100 AWS services, from one location. Along with looking up the quota values, you can also request a quota increase from the Service Quotas console.

**To view your quotas**

You can view your quotas using the following options:

- Open the [Service endpoints and quotas](https://docs.aws.amazon.com/general/latest/gr/aws-service-information.html) page in the documentation, search for the service name, and click the link to go to the page for that service. To view the service quotas for all AWS services in the documentation without switching pages, view the information in the [Service Endpoints and Quotas](https://docs.aws.amazon.com/general/latest/gr/aws-general.pdf#aws-service-information) page in the PDF instead.
- Open the [Service Quotas console](https://console.aws.amazon.com/servicequotas/home). In the navigation pane, choose **AWS services** and select a service.
- Use the [list-service-quotas](https://docs.aws.amazon.com/cli/latest/reference/service-quotas/list-service-quotas.html) and [list-aws-default-service-quotas](https://docs.aws.amazon.com/cli/latest/reference/service-quotas/list-aws-default-service-quotas.html) AWS CLI commands.

**To request a quota increase**

You can request a quota increase using Service Quotas and AWS Support Center. If a service is not yet available in Service Quotas, use AWS Support Center instead. Increases are not granted immediately. It might take a couple of days for your increase to become effective.

- **(Recommended)** Open the [Service Quotas console](https://console.aws.amazon.com/servicequotas/home). In the navigation pane, choose **AWS services**. Select a service, select a quota, and follow the directions to request a quota increase. For more information, see [Requesting a Quota Increase](https://docs.aws.amazon.com/servicequotas/latest/userguide/request-quota-increase.html) in the *Service Quotas User Guide*.
- Use the [request-service-quota-increase](https://docs.aws.amazon.com/cli/latest/reference/service-quotas/request-service-quota-increase.html) AWS CLI command.
- Open the [AWS Support Center](https://console.aws.amazon.com/support/home#/) page, sign in if necessary, and choose **Create case**. Choose **Service limit increase**. Complete and submit the form.

# Monitoring and Alerting

## Getting Started with Monitoring

As we called out in an earlier video, once we have our service running in the Cloud, we want to make sure that our service keeps running, and not just that, we want to make sure it keeps behaving as expected, returning the right results quickly and reliably. The key to ensuring all of this, is to set up good monitoring and alerting rules. In the next few videos, we'll do a rundown of monitoring and alerting concepts and techniques, followed by a practical demonstration. Let's dive in. To understand how our service is performing, we need to monitor it. Monitoring lets us look into the history and current status of a system. How can we know what the status is? We'll check out a bunch of different metrics. These metrics tell us if the service is behaving as expected or not. Well, some metrics are generic, like how much memory an instance is using. Other metrics are specific to the service we want to monitor. Say your company is running a website and you want to check if it's working correctly. When a web server responds to an HTTP request, it starts by sending a response code, followed by the content of the response. You might know, for example, that a 404 code means that the page wasn't found, or that a 500 response means that there was an internal server error. In general, response codes in the 500 range, like 501 or 503, tells us that something bad happened on the server while generating a response. Well, response codes in the 400 range means there was a client-side problem in the request. When monitoring your web service, you want to check both the count of response codes and their types to know if everything's okay. If you're running an e-commerce site, you'll care about how many purchases were made successfully and how many failed to complete. If you're running a mail server, you want to know how many emails were sent and how many got stuck and so on. You'll need to think about the service you want to monitor and figure out the metrics you'll need. Now, once we've decided what metrics we care about, what do we do with them? We'll typically store them in the monitoring system. There's a bunch of different monitoring systems out there. Some systems like AWS Cloudwatch, Google Stack Driver, or Azure Metrics are offered directly by the Cloud providers. Other systems like Prometheus, Datadog, or Nagios can be used across vendors. There's two ways of getting our metrics into the monitoring system. Some systems use a pull model, which means that the monitoring infrastructure periodically queries our service to get the metrics. Other monitoring systems use a push model, which means that our service needs to periodically connect to the system to send the metrics. No matter how we get the metrics into the system, we can create dashboards based on the collected data. This dashboard show the progression of the metrics over time. We can look at the history of one specific metric to compare the current state to how it was last week or last month. Or we can look at the progression of two or more metrics together to check out how the change in one metrics effects another. Imagine it's Monday morning and you notice that your service is receiving a lot less traffic than usual. You can look at the data from past weeks and see if you always get less traffic on Monday mornings or if there's something broken causing your service to be unresponsive. Or if you see that in the past couple days, the memory used by your instances has been going up, you can check if this growth follows a similar increase in another metric, like the amount of requests received or the amount of data being transmitted. This can help you decide if there's been a memory leak that needs to be fixed or if it's just an expected consequences of a growth in popularity. Pro tip, you only want to store the metrics that you care about, since storing all of these metrics in the system takes space, and storage space costs money. When we collect metrics from inside a system, like how much storage space the service is currently using or how long it takes to process a request, this is called whitebox monitoring. Whitebox monitoring checks the behavior of the system from the inside. We know the information we want to track, and we're in charge of making it possible to track. For example, if we want to track how many queries we're making to the database, we might need to add a variable to count this. On the flip side, blackbox monitoring checks the behavior of the system from the outside. This is typically done by making a request to the service and then checking that the actual response matches the expected response. We can use this to do a very simple check to know if the service is up and to verify if the service is responding from outside your network. Or we could use it to see how long it takes for a client in a different part of the world to get a response from the system. Okay, monitoring is really cool, but who wants to stare at dashboards all day trying to figure out if something's wrong? Fortunately, we don't have to. Instead, we can set up alerting rules to let us know if something's wrong. This is a critical part of ensuring a reliable system, and we're going to learn how to do it in the next video.

## Getting Alerts When Things Go Wrong

We expect a lot from our modern IT services. We expect them to be up and running 24-7. We want to be able to get our work done whenever and wherever. For that, we need our services to respond day or night, workday or holiday. But even if the services are running 24-7, System Administrators can't constantly be in front of their systems. Instead, we set up our services so that they work unattended and deal with problems when they happen. Now to do this, we need to detect those problems so that we can deal with them as quickly as possible. If you have no automated way of raising an alert, you might only find out about the issue when you get a call from a frustrated user telling you that your service is down. That's not ideal. It's much better to create automation that checks the health of your system and notifies you when things don't behave as expected. This can give you advance warning that something's wrong, sometimes even before users notice a problem at all. So how do we do that? The most basic approach is to run a job periodically that checks the health of the system and sends out an email if the system isn't healthy. On a Linux system, we could do this using cron, which is the tool to schedule periodic jobs. We'd pair this with a simple Python script that checks the service and sends any necessary emails. This is an extremely simplified version of an alerting system, but it shares the same principles. Is all alerting systems, no matter how complex and advanced. We want to periodically check the state of the service and raise alerts if there's a problem. When you use a monitoring system like the ones we described in our last video, the metrics you collect represent the state of your service. Instead of periodically running a script that connects to the service and checks if it's responding, you can configure the system to periodically evaluate the metrics; and based on some conditions, decide if an alert should be raised. Raising an alert signals that something is broken and a human needs to respond. For example, you can set up your system to raise alerts if the application is using more than 10 gigabytes of RAM, or if it's responding with too many 500 errors, or if the queue of requests waiting to get processed gets too long. Of course, not all alerts are equally urgent. We typically divide useful alerts into two groups, those that need immediate attention and those that need attention in the near future. If an alert doesn't need attention, then it shouldn't have been sent at all. It's just noise. If your web service is responding with errors to 50 percent of the requests, you should look at what's going on right away. Even if this means waking up in the middle of the night to address whatever is wrong, you'll definitely want to fix this kind of critical problem ASAP. On the other hand, if the issue is that the attached storage is 80 percent full, you need to figure out whether to increase the disk size or maybe clean up some of the stored data. But this isn't super urgent, so don't let it get in the way of a good night's sleep. Since these two types of alerts are different, we typically configure our systems to raise alerts in two different ways. Those that need immediate attention are called pages, which comes from a device called a pager. Before mobile phones became popular, pagers were the device of choice for receiving urgent messages, and they're still used in some places around the world. Nowadays, most people receive their pages in other forms like SMS, automated phone calls, emails, or through a mobile app, but we still call them pages. On the flip side, the non-urgent alerts are usually configured to create bugs or tickets for an IT specialist to take care of during their workday. They can also be configured to send email to specific mailing lists or send a message to a chat channel that will be seen by the people maintaining the service. One thing to highlight is that all alerts should be actionable. If you get a bug or a page and there's nothing for you to do, then the alert isn't actionable and it should be changed or it shouldn't be there at all. Otherwise, it's just noise. Say you're trying to check if your services database back-end is responsive. If you do this by creating a query that returns all rows in a large table, your request might sometimes timeout and raise an alert. That would be a noisy alert, not really actionable. You'd need to tweak the query to make the check useful. Say you run a cron job that copies files from one location to another every 10 minutes, you want to check that this job runs successfully. So you configure your system to alert you if the job fails. After putting this in production, you realize there's a bunch of unimportant reasons that can cause this job to temporarily fail. Maybe the destination storage is too busy and so sometimes the job times out. Maybe the origin was being rebooted right when the job started, so the job couldn't connect to it. No matter why, whenever you go to check out what caused a job to fail, you discover that the following run had succeeded and there's nothing for you to do. You need to rethink the problem and tweak your alert. Since the task is running frequently, you don't care if it fails once or twice, you can change the system to only raise the alert if the job fails three times in a row. That way when you get a bug, it means that it's failing consistently and you'll actually need to take action to fix it. All of this configuring and tweaking can seem like a lot of work. You need to think about which metrics you care about. Configure your monitoring system to store them, then configure your alerting system to raise alerts when things don't behave as expected. The flip side is that once you've set your systems to raise actionable alerts when needed, you're going to have peace of mind. If no alerts are firing, you know the service is working fine. This lets you concentrate on other tasks without having to worry. To set up good alerts, we need to figure out which situations should page, which ones should create bugs, and which ones we just don't care about. These decisions aren't always easy and might need some discussion with the rest of your team. But it can help make sure that you spend time only on things that actually matter. Up next, we'll talk about criteria that we can use to decide which situation should raise alerts and what to do about them.

## Service-Level Objectives

We all know that some IT systems are more critical than others. Let's be real, if you try to play a computer game that you haven't opened in a year and it doesn't work, you probably won't care as much as if you're trying to make a bank transfer and your bank's website is down. Sometimes a piece of infrastructure can be down and the overall system still works with degraded performance. For example, if the caching server that makes your web application go faster is down, the app can still function, even if it's running slower. No system is ever available 100% of the time, it's just not possible. But depending on how critical the service is, it can have different service level objectives, or SLOs. SLOs are pre-established performance goals for a specific service. Setting these objectives helps manage the expectations of the service users, and the targets also guide the work of those responsible for keeping the service running. SLOs need to be measurable, which means that there should be metrics that track how the service is performing and let you check if it's meeting the objectives or not.

Many SLOs are expressed as how much time a service will behave as expected. For example, a service might promise to be available 99% of the time.

Heads up, when dealing with metrics and availability, we need to do a little math to understand what those numbers mean in practice, but don't worry, it's all pretty straightforward. If our service has an SLO of 99% availability, it means it can be down up to 1 % of the time. If we measure this over a year, the service can be down for a total of 3.65 during the year and still have 99% availability. Availability targets like this one are commonly named by their number of nines. Our 99% example would be a two 9 service, 99.9% availability is a three 9 service, 99.999% availability is a five 9 service. Five nine services promised a total down time of up to five minutes in a year. Five nines is super high availability, reserved only for the most critical systems. A three nine service, aiming for a maximum of eight hours of downtime per year, is fine for a lot of IT systems. Now, you might be wondering, why not just make everything a five nine service? It's a good question. The answer is, because it's really expensive and usually not necessary. If your service isn't super critical and it's okay for it to be down briefly once in a while having two or three nines of availability might be enough. You can keep the service running with a small team.

Five nine services usually require a much larger team of engineers to maintain it. Any service can have a bunch of different service level objectives like these, they tell its users what to expect from it. Some services, like those that we pay for, also have more strict promises in the form of service level agreements, or SLAs. A service level agreement is a commitment between a provider and a client.

Breaking these promises might have serious consequences. Service level objectives though are more like a soft target, it's what the maintaining team aims for, but the target might be missed in some situations. As we called out, having explicit SLOs or SLAs is useful for both the users of that service and the team that keeps the service running. If you're using a cloud service, you can decide how much you're going to entrust your infrastructure to it, based on the SLAs that the provider publishes. If on the other hand you're part of the team that maintains the service, you can use the SLOs and SLAs of your service to decide which alerts to create and how urgent they should be. Say you have a service with an SLO that says that at least 90% of the requests should return within 5 seconds. To know if your service is behaving correctly, you need to measure how many of the total requests are returning within those 5 seconds, and you want that number to always be above 90%. So you might set up a non-paging alert to notify you if less than 95% return within 5 seconds, and a paging alert if less than 90% return promptly. If you're in charge of a website, you'll typically measure the rate of responses with 500 return codes to check if your service is behaving correctly. If your SLO is 99% of successful requests, you can set up a non-paging alert if the rate of errors is above 0.5%, and a paging alert if it reaches 1%. In an earlier video, we called out that services usually break because something changed. That's also often the case when looking at what makes services go out of SLO. If your service was working fine and meeting all of its SLOs and then started misbehaving, it's likely this was caused by a recent change. That's why some teams use the concepts of error budgets to handle their services.

Say you're running a service that has three nines of availability. This means the service can be down 43 minutes per month, this is your error budget. You can tolerate up to 43 minutes of downtime, so you keep track of the total time the service was down during the month. If it starts to get close to those 43 minutes, you might decide to stop pushing any new features and focus on resolving the problems that keep causing the downtime. Now, all this talk of nines, availability and downtime can have your head spinning if you've never done this before, and that's totally normal. If it's your first time setting objectives for your service, start by setting achievable goals that you can measure.

Track how the service behaves for a while and see what causes the service to deviate from the targets. Once you have a better idea of the whole service's behavior, you can set more aggressive goals. Up next, we'll go back to our VMS running in the cloud and demonstrate how we can monitor them using the tools offered by the provider.

## Basic Monitoring in GCP

So far, we've seen how to create virtual machines in the Google Cloud Console. We've kept these virtual machines running and now we want to see how we can use the tools provided by the cloud vendor to monitor them and create alerts based on them. For this demonstration, we'll use the monitoring tool called Stackdriver, which is part of the overall offering. When you first activate this system, it takes a while until it starts collecting on the metrics from all the machines, so we've activated in advance.

When we first opened the monitoring console, we see an overview of the system. At the moment, this is looking pretty empty, but we could configure this dashboard to show the charts that we consider the most useful. Let's go into the instances dashboard, we see here the list of our instances and we can click on each of them to see that monitoring information that Stackdriver has collected about them. The monitoring system gives us a very simple overview of each of the instances with three basic metrics, CPU usage, Disk I/O, and network traffic. Depending on what surface we want to run on a VM, we can customize these dashboards to show different metrics. If the metrics that come baked in aren't enough, you can create your own metrics and also add them here. Now we want to check out how to set up an alert to notify us if something isn't behaving correctly. To do this, we'll create a new alerting policy. To set up a new alert, we have to configure the condition that triggers the alert. After we've done that, we can also configure how we want to be notified of the issue and add any documentation that we want the notification to include. Let's start by configuring the condition. As we called out, alerting conditions are related to specific metrics. We want to be notified when the metric indicates that there's a problem with an instance. For this example, we're going to configure an alert that triggers if an instance in CPU utilization is more than 90 percent. We'll start by selecting that we want to monitor GCE, VM instances, which are the instances that we currently have running and then select the CPU utilization metric.

After selecting the metric, we see the graph of the collected values for all of the current running instances. We can optionally add extra filters and groups for the data for this condition. For example, we could choose to only look at some of the instances, selecting by their zone, region, or name. This can be useful if you want to have separate alerts for instances used for production, and those used for testing or development. On top of that, we can also choose an aggregator for the data, these aggregators are useful when the metrics that you're collecting are about the overall system and not just one instance. For example, if you're checking the number of error responses that your system generated, you want to sum all the errors across instances. Depending on how we filter group and aggregate the data, we'll end up with a bunch of different time series, we'll use these values to decide if we should trigger the alert or not. The next step is selecting how many of the different time series need to violate the condition for the alert to trigger. We can trigger the alert when one, some, or all of the different time series violate the condition. For this example, we'll configure our alert to trigger if any instance is using more than 90 percent of the CPU. So, let's select any time series violates. Now, we'll say that we want our alert to trigger if the value is above 90 percent for one minute. All right. We've set the condition. Now, we can select how we want to get the notification and when the alert triggers. Currently, the only type of notification that we can use is e-mail. To use the other channel types available, we need to configure them in our profile. For this example, e-mail will do. Using e-mails can be just fine when you're getting started with alerting, but eventually you'll want to configure additional methods. All right. We've configured our alert to send e-mails. Now, we can add extra documentation to our alert. This documentation is intended to help the person that's responding to the alert understand what they need to do to fix the problem. Including good documentation here, it can be super-important when you've got a bunch of different people working together in a team and not everyone knows everything. Alerts that include good documentation are much easier to tend to and help get the service back to a healthy state faster. For our example, we'll add a message saying that whoever is taking care of this alert, should check the instance with top. Finally, we'll need to give a name to our alerting policy, we'll call it CPU and then save it.

Now, we've set up our alert. Now, we can sit back and relax knowing that if anything goes wrong, we'll be the first to know. For the final part of this demo, we want to show what happens when the alert triggers. To do that, we'll start a process in one of our instances that uses all of the available CPU, by creating an infinite loop. So we'll go back to the main console, SSH into the VM, called Linux- instance and then create a wire loop that never ends.

Now, our loop is running and using all of the available CPU, we can check this by running the top command that shows us the CPU usage. We see that there's a bash command that's using almost 100 percent of the available CPU, our experiment is working. Now, remember that we said that we wanted the condition to be true for a minute before the alert triggers, it won't trigger just yet. It's common practice to use time windows of one, five, or even 10 minutes when dealing with the alerting. We don't want to get an alert for a small spike that lasted only a few seconds and then went away. We want to get alerted when there's an actual problem that requires our attention. The size of the time window we choose depends on the metric we're checking, the length of the expected spikes and a bunch of other factors. It's pretty normal to have to tweak how long we want the condition to be true as we try our alert out. If you're getting notified too often about conditions that go away on their own without you having to do anything, you might choose to make the time window larger. On the flip side, if you're getting notified too late about conditions that needed attention, you might choose to make the time window smaller. All right. We've let enough time pass, let's check out what's up with our alert.

We see that there's an open incident, which is a way of grouping problems. The alerts summary gives us a bunch of info about what's going on. We can click on the CPU link to get more information. This page shows us the metric that triggered the alert for the incident, it shows the threshold for triggering the alert and the current value of the metric. It also shows us the documentation that we entered and lets us create annotations. We can use these annotations to track the work that we do during an incident. All right. Let's stop the process that's using all of our instances CPU. It's still running the top process from before. Let's exit with Q. Now, the infinite loop is currently running in the background of our console. We can make it run in the foreground by typing fg, and then cancel it by pressing CTRL+C. Now, we've stopped the process. Let's check with top that it's no longer using all of our CPU. Great, the bash process isn't taking all of the CPU time anymore. In another minute, the alert that we'd saw earlier will stop triggering, nice. With that, we've demonstrated how we can monitor a bunch of instances running in the Cloud. We've created an alert based on metrics and verify that the alert triggers. Of course, there's a lot more that we can do with these tools, we'll give you pointers to more information in the reading coming up. After that, there's another quick quiz to check that everything is making sense.

# Metrics, Monitoring and Alerting

*This post is part of a series on effective monitoring. Be sure to check out the rest of the series: [Alerting on what matters](https://www.datadoghq.com/blog/monitoring-101-alerting/) and [Investigating performance issues](https://www.datadoghq.com/blog/monitoring-101-investigation/).*

Monitoring data comes in a variety of forms—some systems pour out data continuously and others only produce data when rare events occur. Some data is most useful for *identifying* problems; some is primarily valuable for *investigating* problems. More broadly, having monitoring data is a necessary condition for [*observability*](https://en.wikipedia.org/wiki/Observability) into the inner workings of your systems.

This post covers which data to collect, and how to classify that data so that you can:

1. Receive meaningful, automated alerts for potential problems
2. Quickly investigate and get to the bottom of performance issues

Whatever form your monitoring data takes, the unifying theme is this:

> Collecting data is cheap, but not having it when you need it can be expensive, so you should instrument everything, and collect all the useful data you reasonably can.

This series of articles comes out of our experience monitoring large-scale infrastructure for [our customers](https://www.datadoghq.com/customers/). It also draws on the work of [Brendan Gregg](https://dtdg.co/use-method), [Rob Ewaschuk](https://dtdg.co/philosophy-alerting), and [Baron Schwartz](https://dtdg.co/metrics-attention).

![alerting101-band-1.png](https://imgix.datadoghq.com/img/blog/monitoring-101-collecting-data/alerting101-band-1.png?auto=format&fit=max&w=847)

## [Metrics](https://www.datadoghq.com/blog/monitoring-101-collecting-data/#metrics)

Metrics capture a value pertaining to your systems *at a specific point in time* — for example, the number of users currently logged in to a web application. Therefore, metrics are usually collected once per second, one per minute, or at another regular interval to monitor a system over time.

There are two important categories of metrics in our framework: work metrics and resource metrics. For each system that is part of your software infrastructure, consider which work metrics and resource metrics are reasonably available, and collect them all.

![alerting101-chart-1.png](https://imgix.datadoghq.com/img/blog/monitoring-101-collecting-data/alerting101-chart-1.png?auto=format&fit=max&w=847)

### [Work metrics](https://www.datadoghq.com/blog/monitoring-101-collecting-data/#work-metrics)

Work metrics indicate the top-level health of your system by measuring its useful output. When considering your work metrics, it’s often helpful to break them down into four subtypes:

- **throughput** is the amount of work the system is doing per unit time. Throughput is usually recorded as an absolute number.
- **success** metrics represent the percentage of work that was executed successfully.
- **error** metrics capture the number of erroneous results, usually expressed as a rate of errors per unit time or normalized by the throughput to yield errors per unit of work. Error metrics are often captured separately from success metrics when there are several potential sources of error, some of which are more serious or actionable than others.
- **performance** metrics quantify how efficiently a component is doing its work. The most common performance metric is latency, which represents the time required to complete a unit of work. Latency can be expressed as an average or as a percentile, such as “99% of requests returned within 0.1s”.

These metrics are incredibly important for observability. They are the big, broad-stroke measures that can help you quickly answer the most pressing questions about a system’s internal health and performance: is the system available and actively doing what it was built to do? How fast is it producing work? What is the quality of that work?

Below are example work metrics of all four subtypes for two common kinds of systems: a web server and a data store.

**Example work metrics: Web server (at time 2015-04-24 08:13:01 UTC)**

| **Subtype** | **Description**                                             | **Value** |
| ----------- | ----------------------------------------------------------- | --------- |
| throughput  | requests per second                                         | 312       |
| success     | percentage of responses that are 2xx since last measurement | 99.1      |
| error       | percentage of responses that are 5xx since last measurement | 0.1       |
| performance | 90th percentile response time in seconds                    | 0.4       |

**Example work metrics: Data store (at time 2015-04-24 08:13:01 UTC)**

| **Subtype** | **Description**                                              | **Value** |
| ----------- | ------------------------------------------------------------ | --------- |
| throughput  | queries per second                                           | 949       |
| success     | percentage of queries successfully executed since last measurement | 100       |
| error       | percentage of queries yielding exceptions since last measurement | 0         |
| error       | percentage of queries returning stale data since last measurement | 4.2       |
| performance | 90th percentile query time in seconds                        | 0.02      |

### [Resource metrics](https://www.datadoghq.com/blog/monitoring-101-collecting-data/#resource-metrics)

Most components of your software infrastructure serve as a resource to other systems. Some resources are low-level—for instance, a server’s resources include such physical components as CPU, memory, disks, and network interfaces. But a higher-level component, such as a database or a geolocation microservice, can also be considered a resource if another system requires that component to produce work.

Resource metrics can help you reconstruct a detailed picture of a system’s state, making them especially valuable for investigation and diagnosis of problems. For each resource in your system, try to collect metrics that cover four key areas:

1. **utilization** is the percentage of time that the resource is busy, or the percentage of the resource’s capacity that is in use.
2. **saturation** is a measure of the amount of requested work that the resource cannot yet service, often queued.
3. **errors** represent internal errors that may not be observable in the work the resource produces.
4. **availability** represents the percentage of time that the resource responded to requests. This metric is only well-defined for resources that can be actively and regularly checked for availability.

Here are example metrics for a handful of common resource types:

| **Resource** | **Utilization**                                       | **Saturation**      | **Errors**                                  | **Availability**             |
| ------------ | ----------------------------------------------------- | ------------------- | ------------------------------------------- | ---------------------------- |
| Disk IO      | % time that device was busy                           | wait queue length   | # device errors                             | % time writable              |
| Memory       | % of total memory capacity in use                     | swap usage          | N/A (not usually observable)                | N/A                          |
| Microservice | average % time each request-servicing thread was busy | # enqueued requests | # internal errors such as caught exceptions | % time service is reachable  |
| Database     | average % time each connection was busy               | # enqueued queries  | # internal errors, e.g. replication errors  | % time database is reachable |

### [Other metrics](https://www.datadoghq.com/blog/monitoring-101-collecting-data/#other-metrics)

There are a few other types of metrics that are neither work nor resource metrics, but that nonetheless may help making a complex system observable. Common examples include counts of cache hits or database locks. When in doubt, capture the data.

## [Events](https://www.datadoghq.com/blog/monitoring-101-collecting-data/#events)

In addition to metrics, which are collected more or less continuously, some monitoring systems can also capture events: discrete, infrequent occurrences that can provide crucial context for understanding what changed in your system’s behavior. Some examples:

- Changes: Internal code releases, builds, and build failures
- Alerts: Internally generated alerts or third-party notifications
- Scaling events: Adding or subtracting hosts

An event usually carries enough information that it can be interpreted on its own, unlike a single metric data point, which is generally only meaningful in context. Events capture *what happened*, at a point in *time*, with optional *additional information*. For example:

| **What happened**                     | **Time**                | **Additional information** |
| ------------------------------------- | ----------------------- | -------------------------- |
| Hotfix f464bfe released to production | 2015–05–15 04:13:25 UTC | Time elapsed: 1.2 seconds  |
| Pull request 1630 merged              | 2015–05–19 14:22:20 UTC | Commits: ea720d6           |
| Nightly data rollup failed            | 2015–05–27 00:03:18 UTC | Link to logs of failed job |

Events are sometimes used used to generate alerts—someone should be notified of events such as the third example in the table above, which indicates that critical work has failed. But more often they are used to investigate issues and correlate across systems. In general, think of events like metrics—they are valuable data to be collected wherever it is feasible.

![alerting101-band-3.png](https://imgix.datadoghq.com/img/blog/monitoring-101-collecting-data/alerting101-band-3.png?auto=format&fit=max&w=847)

## [What good data looks like](https://www.datadoghq.com/blog/monitoring-101-collecting-data/#what-good-data-looks-like)

The data you collect should have four characteristics:

- **Well-understood.** You should be able to quickly determine how each metric or event was captured and what it represents. During an outage you won’t want to spend time figuring out what your data means. Keep your metrics and events as simple as possible, use standard concepts described above, and name them clearly.
- **Granular.** If you collect metrics too infrequently or average values over long windows of time, you may lose the ability to accurately reconstruct a system’s behavior. For example, periods of 100% resource utilization will be obscured if they are averaged with periods of lower utilization. Collect metrics for each system at a frequency that will not conceal problems, without collecting so often that monitoring becomes perceptibly taxing on the system (the [observer effect](https://en.wikipedia.org/wiki/Observer_effect_(information_technology))) or creates noise in your monitoring data by sampling time intervals that are too short to contain meaningful data.
- **Tagged by scope.** Each of your hosts operates simultaneously in multiple scopes, and you may want to check on the aggregate health of any of these scopes, or their combinations. For example: how is production doing in aggregate? How about production in the Northeast U.S.? How about a particular role or service? It is important to retain the multiple scopes associated with your data so that you can alert on problems from any scope, and quickly investigate outages without being limited by a fixed hierarchy of hosts.
- **Long-lived.** If you discard data too soon, or if after a period of time your monitoring system aggregates your metrics to reduce storage costs, then you lose important information about what happened in the past. Retaining your raw data for a year or more makes it much easier to know what “normal” is, especially if your metrics have monthly, seasonal, or annual variations.

## [Data for alerts and diagnostics](https://www.datadoghq.com/blog/monitoring-101-collecting-data/#data-for-alerts-and-diagnostics)

The table below maps the different data types described in this article to different levels of alerting urgency outlined [in a companion post](https://www.datadoghq.com/blog/monitoring-101-alerting/). In short, a *record* is a low-urgency alert that does not notify anyone automatically but is recorded in a monitoring system in case it becomes useful for later analysis or investigation. A *notification* is a moderate-urgency alert that notifies someone who can fix the problem in a non-interrupting way such as email or chat. A *page* is an urgent alert that interrupts a recipient’s work, sleep, or personal time, whatever the hour. Note that depending on severity, a notification may be more appropriate than a page, or vice versa:

| **Data**                      | **Alert**    | **Trigger**                                                  |
| ----------------------------- | ------------ | ------------------------------------------------------------ |
| Work metric: Throughput       | Page         | value is much higher or lower than usual, or there is an anomalous rate of change |
| Work metric: Success          | Page         | the percentage of work that is successfully processed drops below a threshold |
| Work metric: Errors           | Page         | the error rate exceeds a threshold                           |
| Work metric: Performance      | Page         | work takes too long to complete (e.g., performance violates internal SLA) |
| Resource metric: Utilization  | Notification | approaching critical resource limit (e.g., free disk space drops below a threshold) |
| Resource metric: Saturation   | Record       | number of waiting processes exceeds a threshold              |
| Resource metric: Errors       | Record       | number of errors during a fixed period exceeds a threshold   |
| Resource metric: Availability | Record       | the resource is unavailable for a percentage of time that exceeds a threshold |
| Event: Work-related           | Page         | critical work that should have been completed is reported as incomplete or failed |

## [Conclusion: Collect ’em all](https://www.datadoghq.com/blog/monitoring-101-collecting-data/#conclusion-collect-em-all)

- Instrument everything and collect as many work metrics, resource metrics, and events as you reasonably can. Observability of complex systems demands comprehensive measurements.
- Collect metrics with sufficient granularity to make important spikes and dips visible. The specific granularity depends on the system you are measuring, the cost of measuring and a typical duration between changes in metrics—seconds for memory or CPU metrics, minutes for energy consumption, and so on.
- To maximize the value of your data, tag metrics and events with several scopes, and retain them at full granularity for at least 15 months.

Automated alerts are essential to monitoring. They allow you to spot problems anywhere in your infrastructure, so that you can rapidly identify their causes and minimize service degradation and disruption. To reference [a companion post](https://www.datadoghq.com/blog/monitoring-101-collecting-data/), if metrics and other measurements facilitate [observability](https://en.wikipedia.org/wiki/Observability), then alerts draw human attention to the particular systems that require observation, inspection, and intervention.

But alerts aren’t always as effective as they could be. In particular, real problems are often lost in a sea of noisy alarms. This article describes a simple approach to effective alerting, regardless of the scale of the systems involved. In short:

1. Alert liberally; page judiciously
2. Page on symptoms, rather than causes

This series of articles comes out of our experience monitoring large-scale infrastructure for [our customers](https://www.datadoghq.com/customers/). It also draws on the work of [Brendan Gregg](http://dtdg.co/use-method), [Rob Ewaschuk](http://dtdg.co/philosophy-alerting), and [Baron Schwartz](http://dtdg.co/metrics-attention).

## [When to alert someone (or no one)](https://www.datadoghq.com/blog/monitoring-101-alerting/#when-to-alert-someone-or-no-one)

![alerting101-2-chart.png](https://imgix.datadoghq.com/img/blog/monitoring-101-alerting/alerting101-2-chart.png?auto=format&fit=max&w=847)

An alert should communicate something specific about your systems in plain language: “Two Cassandra nodes are down” or “90% of all web requests are taking more than 0.5s to process and respond.” Automating alerts across as many of your systems as possible allows you to respond quickly to issues and provide better service, and it also saves time by freeing you from continual manual inspection of metrics.

### [Levels of alerting urgency](https://www.datadoghq.com/blog/monitoring-101-alerting/#levels-of-alerting-urgency)

Not all alerts carry the same degree of urgency. Some require immediate human intervention, some require eventual human intervention, and some point to areas where attention may be needed in the future. All alerts should, at a minimum, be logged to a central location for easy correlation with other metrics and events.

#### [Alerts as records (low severity)](https://www.datadoghq.com/blog/monitoring-101-alerting/#alerts-as-records-low-severity)

Many alerts will not be associated with a service problem, so a human may never even need to be aware of them. For instance, when a data store that supports a user-facing service starts serving queries much slower than usual, but not slow enough to make an appreciable difference in the overall service’s response time, that should generate a low-urgency alert that is recorded in your monitoring system for future reference or investigation but does not interrupt anyone’s work. After all, transient issues that could be to blame, such as network congestion, often go away on their own. But should the service start returning a large number of timeouts, that alert-based data will provide invaluable context for your investigation.

#### [Alerts as notifications (moderate severity)](https://www.datadoghq.com/blog/monitoring-101-alerting/#alerts-as-notifications-moderate-severity)

The next tier of alerting urgency is for issues that do require intervention, but not right away. Perhaps the data store is running low on disk space and should be scaled out in the next several days. Sending an email and/or posting a notification in the service owner’s chat room is a perfect way to deliver these alerts—both message types are highly visible, but they won’t wake anyone in the middle of the night or disrupt an engineer’s flow.

#### [Alerts as pages (high severity)](https://www.datadoghq.com/blog/monitoring-101-alerting/#alerts-as-pages-high-severity)

The most urgent alerts should receive special treatment and be escalated to a page (as in “[pager](https://en.wikipedia.org/wiki/Pager)”) to urgently request human attention. Response times for your web application, for instance, should have an internal SLA that is at least as aggressive as your strictest customer-facing SLA. Any instance of response times exceeding your internal SLA would warrant immediate attention, whatever the hour.

![alerting101-2-band-1.png](https://imgix.datadoghq.com/img/blog/monitoring-101-alerting/alerting101-2-band-1.png?auto=format&fit=max&w=847)

### [When to let a sleeping engineer lie](https://www.datadoghq.com/blog/monitoring-101-alerting/#when-to-let-a-sleeping-engineer-lie)

Whenever you consider setting an alert, ask yourself three questions to determine the alert’s level of urgency and how it should be handled:

1. 

```
**Is this issue real?** It may seem obvious, but if the issue is not  
real, it usually should not generate an alert. The examples below  
can trigger alerts but probably are not symptomatic of real  
problems. Alerting—or, worse, paging—on occurrences such as these  
contributes to alert fatigue and can cause more serious issues to be  
ignored:



-   Metrics in a test environment are out of bounds
-   A single server is doing its work very slowly, but it is part of  
    a cluster with fast-failover to other machines, and it reboots  
    periodically anyway
-   Planned upgrades are causing large numbers of machines to report as offline


If the issue is indeed **real**, it should generate an alert. Even  
if the alert is not linked to a notification, it should be recorded  
within your monitoring system for later analysis and correlation.
```

1. 

```
**Does this issue require attention?** If you can reasonably  
automate a response to an issue, you should consider doing so. There  
is a very real cost to calling someone away from work, sleep, or  
personal time. If the issue is **real *and* it requires attention**,  
it should generate an alert that notifies someone who can  
investigate and fix the problem. At minimum, the notification should  
be sent via email, chat or a ticketing system so that the recipients  
can prioritize their response.
```

1. 

```
**Is this issue urgent?** Not all issues are emergencies. For  
example, perhaps a moderately higher than normal percentage of  
system responses have been very slow, or perhaps a slightly elevated  
share of queries are returning stale data. Both issues may need to  
be addressed soon, but not at 4:00 A.M. If, on the other hand, a key  
system stops doing its work at an acceptable rate, an engineer  
should take a look immediately. If the symptom is <strong>real *and* it  
requires attention *and* it is urgent</strong>, it should generate a page.
```

![alerting101-2-band-2.png](https://imgix.datadoghq.com/img/blog/monitoring-101-alerting/alerting101-2-band-2.png?auto=format&fit=max&w=847)

### [Page on symptoms](https://www.datadoghq.com/blog/monitoring-101-alerting/#page-on-symptoms)

Pages deserve special mention: they are extremely effective for delivering information, but they can be quite disruptive if overused, or if they are linked to poorly designed alerts. In general, a page is the most appropriate kind of alert when the system you are responsible for stops doing useful work with acceptable throughput, latency, or error rates. Those are the sort of problems that you want to know about immediately.

The fact that your system stopped doing useful work is a *symptom* —that is, it is a manifestation of an issue that may have any number of different *causes*. For example: if your website has been responding very slowly for the last three minutes, that is a symptom. Possible causes include high database latency, failed application servers, Memcached being down, high load, and so on. Whenever possible, build your pages around symptoms rather than causes. See our [companion article on data collection](https://www.datadoghq.com/blog/monitoring-101-collecting-data/) for a metric framework that helps to separate symptoms from causes.

Paging on symptoms surfaces real, oftentimes user-facing problems, rather than hypothetical or internal problems. Contrast paging on a symptom, such as slow website responses, with paging on potential causes of the symptom, such as high load on your web servers. Your users will not know or care about server load if the website is still responding quickly, and your engineers will resent being bothered for something that is only internally noticeable and that may revert to normal levels without intervention.

#### [Durable alert definitions](https://www.datadoghq.com/blog/monitoring-101-alerting/#durable-alert-definitions)

Another good reason to page on symptoms is that symptom-triggered alerts tend to be durable. This means that regardless of how underlying system architectures may change, if the system stops doing work as well as it should, you will get an appropriate page even without updating your alert definitions.

![alerting101-2-band-3.png](https://imgix.datadoghq.com/img/blog/monitoring-101-alerting/alerting101-2-band-3.png?auto=format&fit=max&w=847)

#### [Exception to the rule: Early warning signs](https://www.datadoghq.com/blog/monitoring-101-alerting/#exception-to-the-rule-early-warning-signs)

It is sometimes necessary to call human attention to a small handful of metrics even when the system is performing adequately. Early warning metrics reflect an unacceptably high probability that serious symptoms will soon develop and require immediate intervention.

Disk space is a classic example. Unlike running out of free memory or CPU, when you run out of disk space, the system will not likely recover, and you probably will have only a few seconds before your system hard stops. Of course, if you can notify someone with plenty of lead time, then there is no need to wake anyone in the middle of the night. Better yet, you can anticipate some situations when disk space will run low and build automated remediation based on the data you can afford to erase, such as logs or data that exists somewhere else.

## [Conclusion: Get serious about symptoms](https://www.datadoghq.com/blog/monitoring-101-alerting/#conclusion-get-serious-about-symptoms)

- Send a page only when symptoms of urgent problems in your system’s
  work are detected, or if a critical and finite resource limit is
  about to be reached.
- Set up your monitoring system to record alerts whenever it detects
  real issues in your infrastructure, even if those issues have not
  yet affected overall performance.

The responsibilities of a monitoring system do not end with symptom detection. Once your monitoring system has notified you of a real symptom that requires attention, its next job is to help you diagnose the root cause by making your systems [observable](https://en.wikipedia.org/wiki/Observability) via the monitoring data you have collected. Often this is the least structured aspect of monitoring, driven largely by hunches and guess-and-check. This post describes a more directed approach that can help you to find and correct root causes more efficiently.

This series of articles comes out of our experience monitoring large-scale infrastructure for [our customers](https://www.datadoghq.com/customers/). It also draws on the work of [Brendan Gregg](http://dtdg.co/use-method), [Rob Ewaschuk](http://dtdg.co/philosophy-alerting), and [Baron Schwartz](http://dtdg.co/metrics-attention).

## [A word about data](https://www.datadoghq.com/blog/monitoring-101-investigation/#a-word-about-data)

![metric types](https://imgix.datadoghq.com/img/blog/monitoring-101-investigation/alerting101-chart-1.png?auto=format&fit=max&w=847)

There are three main types of monitoring data that can help you investigate the root causes of problems in your infrastructure. Data types and best practices for their collection are discussed in-depth [in a companion post](https://www.datadoghq.com/blog/monitoring-101-collecting-data/), but in short:

- **Work metrics** indicate the top-level health of your system by measuring its useful output
- **Resource metrics** quantify the utilization, saturation, errors, or availability of a resource that your system depends on
- **Events** describe discrete, infrequent occurrences in your system such as code changes, internal alerts, and scaling events

By and large, work metrics will surface the most serious symptoms and should therefore generate [the most serious alerts](https://www.datadoghq.com/blog/monitoring-101-alerting/#page-on-symptoms). But the other metric types are invaluable for investigating the *causes* of those symptoms. In order for your systems to be [observable](https://en.wikipedia.org/wiki/Observability), you need sufficiently comprehensive measurements to provide a full picture of each system’s health and function.

## [It’s resources all the way down](https://www.datadoghq.com/blog/monitoring-101-investigation/#its-resources-all-the-way-down)

![metric uses](https://imgix.datadoghq.com/img/blog/monitoring-101-investigation/alerting101-2-chart.png?auto=format&fit=max&w=847)

Most of the components of your infrastructure can be thought of as resources. At the highest levels, each of your systems that produces useful work likely relies on other systems. For instance, the Apache server in a LAMP stack relies on a MySQL database as a resource to support its work. One level down, within MySQL are database-specific resources that MySQL uses to do *its* work, such as the finite pool of client connections. At a lower level still are the physical resources of the server running MySQL, such as CPU, memory, and disks.

Thinking about which systems *produce* useful work, and which resources *support* that work, can help you to efficiently get to the root of any issues that surface. Understanding these hierarchies helps you build a mental model of how your systems interact, so you can quickly focus in on the key diagnostic metrics for any incident. When an alert notifies you of a possible problem, the following process will help you to approach your investigation systematically.

![recursive investigation](https://imgix.datadoghq.com/img/blog/monitoring-101-investigation/investigating-diagram-4.png?auto=format&fit=max&w=847)

### [1. Start at the top with work metrics](https://www.datadoghq.com/blog/monitoring-101-investigation/#1-start-at-the-top-with-work-metrics)

First ask yourself, “Is there a problem? How can I characterize it?” If you don’t describe the issue clearly at the outset, it’s easy to lose track as you dive deeper into your systems to diagnose the issue.

Next examine the work metrics for the highest-level system that is exhibiting problems. These metrics will often point to the source of the problem, or at least set the direction for your investigation. For example, if the percentage of work that is successfully processed drops below a set threshold, diving into error metrics, and especially the types of errors being returned, will often help narrow the focus of your investigation. Alternatively, if latency is high, and the throughput of work being requested by outside systems is also very high, perhaps the system is simply overburdened.

### [2. Dig into resources](https://www.datadoghq.com/blog/monitoring-101-investigation/#2-dig-into-resources)

If you haven’t found the cause of the problem by inspecting top-level work metrics, next examine the resources that the system uses—physical resources as well as software or external services that serve as resources to the system. If you’ve already set up dashboards for each system as outlined below, you should be able to quickly find and peruse metrics for the relevant resources. Are those resources unavailable? Are they highly utilized or saturated? If so, recurse into those resources and begin investigating each of them at step 1.

### [3. Did something change?](https://www.datadoghq.com/blog/monitoring-101-investigation/#3-did-something-change)

Next consider alerts and other events that may be correlated with your metrics. If a code release, [internal alert](https://www.datadoghq.com/blog/monitoring-101-alerting/#levels-of-urgency), or other event was registered slightly before problems started occurring, investigate whether they may be connected to the problem.

### [4. Fix it (and don’t forget it)](https://www.datadoghq.com/blog/monitoring-101-investigation/#4-fix-it-and-dont-forget-it)

Once you have determined what caused the issue, correct it. Your investigation is complete when symptoms disappear—you can now think about how to change the system to avoid similar problems in the future. If you did not have the data you needed to quickly diagnose the problem, add more instrumentation to your system to ensure that those metrics and events are available for future responders.

## [Build dashboards before you need them](https://www.datadoghq.com/blog/monitoring-101-investigation/#build-dashboards-before-you-need-them)

![dashboard](https://imgix.datadoghq.com/img/blog/monitoring-101-investigation/example-dashboard-2.png?auto=format&fit=max&w=847)

In an outage, every minute is crucial. To speed your investigation and keep your focus on the task at hand, set up dashboards in advance that help you observe the current and recent state of each system. You may want to set up one dashboard for your high-level application metrics, and one dashboard for each subsystem. Each system’s dashboard should render the work metrics of that system, along with resource metrics of the system itself and key metrics of the subsystems it depends on. If event data is available, overlay relevant events on the graphs for correlation analysis.

## [Conclusion: Follow the metrics](https://www.datadoghq.com/blog/monitoring-101-investigation/#conclusion-follow-the-metrics)

Adhering to a standardized monitoring framework allows you to investigate problems more systematically:

- For each system in your infrastructure, set up a dashboard ahead of time that displays all its key metrics, with relevant events overlaid.
- Investigate causes of problems by starting with the highest-level system that is showing symptoms, reviewing its [work and resource metrics](https://www.datadoghq.com/blog/monitoring-101-collecting-data/#metrics) and any associated events.
- If problematic resources are detected, apply the same investigation pattern to the resource (and its constituent resources) until your root problem is discovered and corrected.

# An Introduction to Metrics, Monitoring, and Alerting

## Introduction

Understanding the state of your infrastructure and systems is essential for ensuring the reliability and stability of your services. Information about the health and performance of your deployments not only helps your team react to issues, it also gives them the security to make changes with confidence. One of the best ways to gain this insight is with a robust monitoring system that gathers metrics, visualizes data, and alerts operators when things appear to be broken.

In this guide, we will discuss what metrics, monitoring, and alerting are. We will talk about why they are important, what types of opportunities they provide, and the type of data you may wish to track. We will be introducing some key terminology along the way and will end with a short glossary of some other terms you might come across while exploring this space.



## What Are Metrics, Monitoring and Alerting?

Metrics, monitoring, and alerting are all interrelated concepts that together form the basis of a monitoring system. They have the ability to provide visibility into the health of your systems, help you understand trends in usage or behavior, and to understand the impact of changes you make. If the metrics fall outside of your expected ranges, these systems can send notifications to prompt an operator to take a look, and can then assist in surfacing information to help identify the possible causes.

In this section, we’ll take a look at these individual concepts and how they fit together.

### What Are Metrics and Why Do We Collect Them?

Metrics represent the raw measurements of resource usage or behavior that can be observed and collected throughout your systems. These might be low-level usage summaries provided by the operating system, or they can be higher-level types of data tied to the specific functionality or work of a component, like requests served per second or membership in a pool of web servers. Some metrics are presented in relation to a total capacity, while others are represented as a rate that indicates the “busyness” of a component.

Often, the easiest metrics to begin with are those already exposed by your operating system to represent the usage of underlying physical resources. Data about disk space, CPU load, swap usage, etc. are already available, provide value immediately, and can be forwarded to a monitoring system without much additional work. Many web servers, database servers, and other software also provide their own metrics which can be passed forward as well.

For other components, especially your own applications, you may have to add code or interfaces to expose the metrics you care about. Collecting and exposing metrics is sometimes known as adding **instrumentation** to your services.

Metrics are useful because they provide insight into the behavior and health of your systems, especially when analyzed in aggregate. They represent the raw material used by your monitoring system to build a holistic view of your environment, automate responses to changes, and alert human beings when required. Metrics are the basic values used to understand historic trends, correlate diverse factors, and measure changes in your performance, consumption, or error rates.

### What is Monitoring?

While metrics represent the data in your system, monitoring is the process of collecting, aggregating, and analyzing those values to improve awareness of your components’ characteristics and behavior. The data from various parts of your environment are collected into a **monitoring system** that is responsible for storage, aggregation, visualization, and initiating automated responses when the values meet specific requirements.

In general, the difference between metrics and monitoring mirrors the difference between data and information. Data is composed of raw, unprocessed facts, while information is produced by analyzing and organizing data to build context that provides value. Monitoring takes metrics data, aggregates it, and presents it in various ways that allow humans to extract insights from the collection of individual pieces.

Monitoring systems fulfill many related functions. Their first responsibility is to accept and store incoming and historical data. While values representing the current point in time are useful, it is almost always more helpful to view those numbers in relation to past values to provide context around changes and trends. This means that a monitoring system should be capable of managing data over periods of time, which may involve sampling or aggregating older data.

Secondly, monitoring systems typically provide visualizations of data. While metrics can be displayed and understood as individual values or tables, humans are much better at recognizing trends and understanding how components fit together when information is organized in a visually meaningful way. Monitoring systems usually represent the components they measure with configurable graphs and dashboards. This makes it possible to understand the interaction of complex variables or changes within a system by glancing at a display.

An additional function that monitoring systems provide is organizing and correlating data from various inputs. For the metrics to be useful, administrators need to be able to recognize patterns between different resources and across groups of servers. For example, if an application experiences a spike in error rates, an administrator should be able to use the monitoring system to discover if that event coincides with the capacity exhaustion of a related resource.

Finally, monitoring systems are typically used as a platform for defining and activating alerts, which we will talk about next.

### What is Alerting?

Alerting is the responsive component of a monitoring system that performs actions based on changes in metric values. Alerts definitions are composed of two components: a metrics-based condition or threshold, and an action to perform when the values fall outside of the acceptable conditions.

While monitoring systems are incredibly useful for active interpretation and investigation, one of the primary benefits of a complete monitoring system is letting administrators disengage from the system. Alerts allow you to define situations that make sense to actively manage, while relying on the passive monitoring of the software to watch for changing conditions.

While notifying responsible parties is the most common action for alerting, some programmatic responses can be triggered based on threshold violations as well. For instance, an alert that indicates that you need more CPU to process the current load can be responded to with a script that auto-scales that layer of your application. While this isn’t strictly an alert since it doesn’t result in a notification, the same monitoring system mechanism can often be used to kick off these processes as well.

However, the main purpose of alerting is still to bring human attention to bear on the current status of your systems. Automating responses is an important mechanism for ensuring that notifications are only triggered for situations that require consideration from a knowledgeable human being. The alert itself should contain information about what is wrong and where to go to find additional information. The individual responding to the alert can then use the monitoring system and associated tooling like log files to investigate the cause of the problem and implementing a mitigation strategy.

Infrastructure of even moderate complexity requires distinctions in alert severity so that the responsible teams or individuals can be notified using methods appropriate to the scale of the problem. For instance, rising utilization of storage might warrant a work ticket or email, while an increase in client-facing error rates or unresponsiveness might require sending a page to on-call staff.



## What Type of Information Is Important to Track?

The types of values you monitor and the information you track will probably change as your infrastructure evolves. Since systems usually function hierarchically, with more complex layers building on top of more primitive infrastructure, it can be useful to think about the metrics available at these different levels when planning your monitoring strategy.

### Host-Based Metrics

Towards the bottom of the hierarchy of primitive metrics are host-based indicators. These would be anything involved in evaluating the health or performance of an individual machine, disregarding for the moment its application stacks and services. These are mainly comprised of usage or performance of the operating system or hardware, like:

- CPU
- Memory
- Disk space
- Processes

These can give you a sense of factors that may impact a single computer’s ability to remain stable or perform work.

### Application Metrics

The next category of metrics you may want to look at are application metrics. These are metrics concerned with units of processing or work that depend on the host-level resources, like services or applications. The specific types of metrics to look at depends on what the service is providing, what dependencies it has, and what other components it interacts with. Metrics at this level are indicators of the health, performance, or load of an application:

- Error and success rates
- Service failures and restarts
- Performance and latency of responses
- Resource usage

These indicators help determine whether an application is functioning correctly and with efficiency.

### Network and Connectivity Metrics

For most types of infrastructure, network and connectivity indicators will be another dataset worth exploring. These are important gauges of outward-facing availability, but are also essential in ensuring that services are accessible to other machines for any systems that span more than one machine. Like the other metrics we’ve discussed so far, networks should be checked for their overall functional correctness and their ability to deliver necessary performance by looking at:

- Connectivity
- Error rates and packet loss
- Latency
- Bandwidth utilization

Monitoring your networking layer can help you improve the availability and responsiveness of both your internal and external services.

### Server Pool Metrics

When dealing with horizontally scaled infrastructure, another layer of infrastructure you will need to add metrics for is pools of servers. While metrics about individual servers are useful, at scale a service is better represented as the ability of a collection of machines to perform work and respond adequately to requests. This type of metric is in many ways just a higher level extrapolation of application and server metrics, but the resources in this case are homogeneous servers instead of machine-level components. Some data you might want to track are:

- Pooled resource usage
- Scaling adjustment indicators
- Degraded instances

Collecting data that summarizes the health of collections of servers is important for understanding the actual capabilities of your system to handle load and respond to changes.

### External Dependency Metrics

Other metrics you may wish to add to your system are those related to external dependencies. Often, services provide status pages or an API to discover service outages, but tracking these within your own systems—as well as your actual interactions with the service—can help you identify problems with your providers that may affect your operations. Some items that might be applicable to track at this level are:

- Service status and availability
- Success and error rates
- Run rate and operational costs
- Resource exhaustion

There are many other types of metrics that can be helpful to collect. Conceptualizing the most important information at varying levels of focus can help you identify indicators that are most useful for predicting or identifying problems. Keep in mind that the most valuable metrics on higher levels are likely to be resources provided by lower layers.



## Factors That Affect What You Choose to Monitor

For peace of mind, in an ideal world you would track everything related to your systems from the beginning in case an item may one day be relevant to you. However, there are many reasons why this might not be possible or even desirable.

A few factors that can affect what you choose to collect and act on are:

- **Resources available for tracking**: Depending on your human resources, infrastructure, and budget, you will have to limit the scope of what you keep track of to what you can afford to implement and reasonably manage.
- **The complexity and purpose of your application**: The complexity of your application or systems can have a large impact on what you choose to track. Items that might be mission critical for some software might not be important at all in others.
- **The deployment environment**: While robust monitoring is most important for production systems, staging and testing systems also benefit from monitoring, though there may be differences in severity, granularity, and the overall metrics measured.
- **The likelihood of the metric being useful**: One of the most important factors affecting whether something is measured is its potential to help in the future. Each additional metric tracked increases the complexity of the system and takes up resources. The necessity of data can change over time as well, requiring reevaluation at regular intervals.
- **How essential stability is**: Simply put, stability and uptime might not be priorities for certain types of personal or early stage projects.

The factors that influence your decisions will depend on your available resources, the maturity of your project, and the level of service you require.



## Important Qualities of a Metrics, Monitoring, and Alerting System

While each monitoring application or service will have its strengths and weaknesses, the best options often share some important qualities. A few of the more important characteristics to look for when evaluating monitoring systems are below.

### Independent from Most Other Infrastructure

One of the most basic requirements of an adequate monitoring system is to be external to other services. While it’s sometimes useful to group services together, a monitoring system’s core responsibilities, its helpfulness in diagnosing problems, and its relationship to the watched systems means that it’s important for your monitoring system to be independently accessible. Your monitoring system will inevitably have some effect on the systems it monitors, but you should aim to keep this minimal to reduce the impact your tracking has on performance and to increase the reliability of your monitoring in the event of other system problems.

### Reliable and Trustworthy

Another basic requirement is reliability. As a monitoring system is responsible for gathering, storing, and providing access to high value information, it is important that you can trust it to operate correctly on a daily basis. Dropped metrics, service outages, and unreliable alerting can all have an immediate harmful impact on your ability to manage your infrastructure effectively. This applies not only to the core software reliability, but also to the configuration you enable, since mistakes like inaccurate alerting can lead to a loss of trust in the system.

### Easy to Use Summary and Detail Views

The ability to display high-level summaries and ask for greater detail on-demand is an important feature to ensure that the metrics data is useful and consumable to human operators. Designing dashboards that present the most commonly viewed data in an immediately intelligible manner can help users understand system state at a glance. Many different dashboard views can be created for different job functions or areas of interest.

Equally important is the ability to drill down from within summary displays to surface the information most pertinent to the current task. Dynamically adjusting the scale of graphs, toggling off unnecessary metrics, and overlaying information from multiple systems is essential to make the tool useful interactively for investigations or root cause analysis.

### Effective Strategy for Maintaining Historical Data

A monitoring system is most useful when it has a rich history of data that can help establish trends, patterns, and consistencies over long timelines. While ideally, all information would be retained indefinitely in its original granularity, cost and resource constraints can sometimes make it necessary to store older data at a reduced resolution. Monitoring systems with the flexibility to work with data both at full granularity and in a sampled format provide a wider range of options for how to handle an ever increasing amount of data.

A related feature that is helpful is the ability to easily import existing data sets. If reducing the information density of your historic metrics is not an attractive option, offloading older data to a long-term storage solution might be a better alternative. In this case, you don’t need to maintain older data within the system, but you need to be able to reload it in bulk when you wish to analyze or use it.

### Able to Correlate Factors from Different Sources

The monitoring system is responsible for providing a holistic view of your entire infrastructure, so it needs to be able to display related information, even if it comes from different systems or has different characteristics. Administrators should be able to glue together information from disparate parts of their systems at will to understand potential interactions and overall status across the entire infrastructure. Ensuring that time synchronization is configured across your systems is a prerequisite to being able to correlate data from different systems reliably.

### Easy to Start Tracking New Metrics or Infrastructure

In order for your monitoring system to be an accurate representation of your systems, you need to be able to make adjustments as the machines and infrastructure change. A minimal amount of friction when adding additional machines will help you do so. Equally important is the ability to easily remove decommissioned machines without destroying the collected data associated with them. The system should make these operations as simple as possible to encourage setting up monitoring as part of the instance provisioning or retirement process.

A related ability that is important is the ease in which the monitoring system can be set up to track entirely new metrics. This depends on the way that metrics are defined in the core monitoring configuration as well as the variety and quality of mechanisms available to send metric data to the system. Defining new metrics is usually more complex than adding additional machines, but reducing the complexity of adding or adjusting metrics will help your team respond to changing requirements in an appropriate time frame.

### Flexible and Powerful Alerting

One of the most important aspects of a monitoring system to evaluate is its alerting capabilities. Aside from very strict reliability requirements, the alerting system need to be flexible enough to notify operators through multiple mediums and powerful enough to be able to compose thoughtful, actionable notification triggers. Many systems defer the responsibility of actually delivering notifications to other parties by offering integrations with existing paging services or messenger applications. This minimizes the responsibility of the alerting functionality and usually provides more flexible options since the plugin just needs to consume an external API.

The part that the monitoring system cannot defer, however, is defining the alerting parameters. Alerts are defined based on values falling outside of acceptable ranges, but the definitions can require some nuance in order to avoid over alerting. For instance, momentary spikes are often not a concern, but sustained elevated load may require operator attention. Being able to clearly define the parameters for an alert is a requirement for composing a robust, trustworthy set of alert conditions.



## Additional Terminology

As you explore the monitoring ecosystem, you’ll start to encounter a set of shared terminology that is frequently used to discuss characteristics of monitoring systems, the data being handled, and different trade offs that require consideration. While in no way exhaustive, the list below can help introduce you to some of the terms you’re most likely to come across.

- **Observability**: Although not strictly defined, observability is a general term used to describe processes and techniques related to increasing awareness and visibility into systems. This can include monitoring, metrics, visualization, tracing, and log analysis.
- **Resource**: In the context of monitoring and software systems, a resource is any exhaustible or limited dependency. What is considered a resource can vary greatly based on part of the system being discussed.
- **Latency**: Latency is a measure of the time it takes to complete an action. Depending on the component, this can be a measure of processing, response, or travel time.
- **Throughput**: Throughput represents the maximum rate of processing or traversal that a system can handle. This can be dependent on software or hardware design. Often there is an important distinction between theoretical throughput and practical observed throughput.
- **Performance**: Performance is a general measure of how efficiently a system is completing work. Performance is an umbrella term that often encompasses work factors like throughput, latency, or resource consumption.
- **Saturation**: Saturation is a measure of the amount of capacity being used. Full saturation indicates that 100% of the capacity is currently in use.
- **Visualization**: Visualization is the process of presenting metrics data in a format that allows for quick, intuitive interpretation through graphs or charts.
- **Log aggregation**: Log aggregation is the act of compiling, organizing, and indexing log files to allow for easier management, searching, and analysis. While separate from monitoring, aggregated logs can be used in conjunction with the monitoring system to identify causes and investigate failures.
- **Data point**: A data point is a single measurement of a single metric.
- **Data set**: A data set is a collection of data points for a metric.
- **Units**: Units are the context for a measured value. A unit defines the magnitude, scope, or quantity of a measurement to understand extent and allow comparison.
- **Percentage Units**: Percentage units are measurements that are taken as a part of a finite whole. A percentage unit indicates how much a value is out of the total possible amount.
- **Rate Units**: Rate units indicate the magnitude of a metric over a constant period of time.
- **Time series**: Time series data is a series of data points that represent changes over time. Most metrics are best represented by a time series because single data points often represent a value at a specific time and the resulting series of points is used to show changes over time.
- **Sampling rate**: Sample rate is a measurement of how often a representative data point is collected in lieu of continuous collection. A higher sampling rate more accurately represents the measured behavior, but requires more resources to handle the extra data points.
- **Resolution**: Resolution refers to the density of data points that make up a data set. Collections with higher resolutions over the same time frame indicate a higher sample rate and a more granular view of the same behavior.
- **Instrumentation**: Instrumentation is the ability to track the behavior and performance of software. This is accomplished by adding code and configuration to software to output data that can then be consumed by a monitoring system.
- **The observer effect**: The observer effect is the impact of the monitoring system itself on the phenomena being observed. Since monitoring takes up resources, the act of measuring behavior and performance will alter the values produced. Monitoring systems seek to avoid adding unnecessary overhead to minimize this impact.
- **Over-monitoring**: Over-monitoring occurs when the quantity of metrics and alerts configured is inversely related to their usefulness. Over-monitoring can cause stress on the infrastructure, make it difficult to find relevant data, and cause teams to lose trust in their monitoring and alerting systems.
- **Alert fatigue**: Alert fatigue is the human response of desensitivity that results from frequent, unreliable, or improperly prioritized alerts. Alert fatigue can cause operators to ignore severe problems and is usually an indication that alert conditions need to be reevaluated.
- **Threshold**: When alerting, a threshold is the boundary between acceptable and unacceptable values which triggers an alert if exceeded. Often alerts are configured to trigger when a value exceeds the threshold for a certain period of time, in order to avoid sending an alert for temporary spikes.
- **Quantile**: A quantile is a dividing point used to separate a dataset into distinct groups based on their values. Quantiles are used to put values into “buckets” that represent segments of a population of data. Often, this is used to separate common values from outliers to better understand what constitutes representative and extreme cases.
- **Trend**: A trend is the general direction that a set of values is indicating. Trends are more reliable than single values in determining the general state of the component being tracked.
- **White-box monitoring**: White-box monitoring is a term used to describe monitoring that relies on access to internal state of the components being measured. White-box monitoring can provide a detailed understanding of system state and is helpful for identifying causes of problems.
- **Black-box monitoring**: Black-box monitoring is monitoring that observes the external state of a system or component by looking only at its inputs, outputs, and behavior. This type of monitoring can closely align with a user’s experience of a system, but is less useful for finding the cause of problems.

## Conclusion

Gathering metrics, monitoring components, and configuring alerts is an essential part of setting up and managing production infrastructure. Being able to tell what is happening within your systems, what resources need attention, and what is causing a slowdown or outage is invaluable. While designing and implementing your monitoring setup can be a challenge, it is an investment that can help your team to prioritize their work, delegate the responsibility of oversight to an automated system, and understand the impact of your infrastructure and software on your stability and performance.

# Troubleshooting and Debugging

## What to Do When You Can't Be Physically There

If you're used to troubleshooting problems on physical computers. It can take a bit of a mindset shift to get used to fixing problems with virtual machines running in the cloud. There's a bunch of things that you can't do, you can't walk up to a server and check out what's wrong with it. But there's also other things that are a lot simpler when troubleshooting VMs in the cloud. Like adding more memory or moving the machine to a different data center. Let's say that after the latest upgrade, a bunch of your cloud VMs have stopped booting. Something went wrong, but you don't know exactly what. You can't connect to the instances or boot them in rescue mode, so what can you do? There's a bunch of options, if you're following the infrastructure as code practices that we've talked about. You could deploy new VMs with the previous version of the system, this would help us get back to a healthy state as quickly as possible. On top of this, you want to understand the problem and how to fix it. To do that, you can create a snapshot of the disk image for one of the failing VMs. And then mount that disk image on a healthy machine. That way you can analyze the contents of the image and figure out what's causing the failures. And it's not always easy to know which piece of the system is causing a failure. Especially if the system is complex with many different services interacting with each other. If you're trying to figure out what's causing your complex servers to respond with a ton of 500s. You need to look at different pieces individually until you find the culprit. Does the problem happen if you run the service and a test VM? Without any load balancers or caching servers in between? Does it happen if you run the service locally on your workstation? The more you can isolate the faulty behavior, the easier it is to fix it. You should remember that problems will happen, it makes sense to spend some time getting ready for them. Setting up a testing environment might take time and effort. So it's a good idea to do this in advance before any problem actually happens. That way you don't need to do it under pressure when your users are complaining that the system's down. Say you're using a database service that's only reachable from inside your cloud network. This means you can't interact with it directly from the outside, only from instances within your cloud infrastructure. If your service starts acting up, you might want to check the responses from the database directly. Rather than going through any of the other back-end servers. To do this, you'll need to have a debugging machine in the network and you'll need to use tools to interact with the database directly. Again, setting the machine up, and learning how to use the tools takes time. So get ahead of the game and do it in advance before any problems come up. You might remember from the troubleshooting and debugging course, that understanding logs is super important for being able to solve problems in IT.

When you run your service in the cloud, you need to learn where to find the logs. That the provider keeps and what info is available in which logs. Some cloud providers offer centralized log solutions to collect all your logs in one place. You can have all your notes, send info, warning and error messages to the log collection point. Then, when you're trying to debug a problem, you can easily see everything that was going on when the error occurred. Up next, we'll check out more strategies that you can use to get to the root cause of your cloudy problems.

## Identifying Where the Failure Is Coming From

As we've called out a few times, when we host our services in the cloud, we need to give up part of the control over the infrastructure that we're using. This might be especially noticeable when we're trying to find the root cause of a problem in our service and we don't know if the failure is caused by an error on our side or on the provider side. So what can we do in that case? Problems on the provider side tend to be isolated to geographical regions. If you're seeing weird problems and you have no idea what could be going on, you can try bringing up your service in a different region and checking if the failure happens there too. If it works fine there, it's likely that there's an issue with the cloud infrastructure and you should bring it up with your provider. If it fails in the other regions too, it's likely that it's a problem with your system. Similarly, if you're seeing problems related to resource usage, you can try running the same system in a different machine type and checking how it behaves there. This could help out, for example, if your service takes too much time to process incoming requests. By changing your service to more powerful machines, you might improve the overall performance. Another option that we've mentioned a bunch is doing rollbacks for the pieces that have recently changed. Having all your infrastructure stored as code in a version control system will let you access the history of the changes to each component in the system. When setting up your service, you should make sure that you can deploy and roll back each individual piece. Imagine you get an alert saying that the web servers in your application are using a lot more memory than they used to you. You don't know why but you know that a new version was deployed a couple of days ago. By rolling back to the previous version, you can verify if that change was at fault or not. If the server's work fine after the rollback, you can investigate the specific changes and try to figure out why they're using so much more memory. If the server's are still using a lot of memory after the rollback, it means something else is up. In an earlier video, we touched briefly upon one popular option when running things on the cloud called containers. Containers are packaged applications that are shipped together with their libraries and dependencies. Each application is executed in a separate container, completely independent of any other applications running on the same machine. Now, one of the neat characteristics of containerized applications is that you can deploy the same container to your local workstation to a server running on-premise or to cloud infrastructure provided by different vendors. This can be really helpful when trying to understand if the failure is in the code or the infrastructure. You simply deploy the container somewhere else and check if it behaves the same way. When using containers, the typical architecture is to have a lot of small containers that take care of different parts of the service. This means that the overall system can get really complex and when something breaks, it can be hard to identify where the problem is coming from. The key to solving problems in the container world is to make sure you have good logs coming in from all of the parts of the system. And, that you can bring up test instances of each of the applications to try things out when necessary. Up next, we'll talk about some of the tools that we can use in the cloud to recover from outages.

## Recovering from Failure

When dealing with a complex system, there's a lot of ways it can fail. If we want our service to be reliable, we need to make sure that we can get it up and running as quickly as possible when bad things happen. We'll need to have good backups and a well-documented recovery plan. Backups here doesn't mean just copies of your data. It also means backups for the different pieces of your infrastructure, including the instances that are running the service and the network that's used to connect to the service. Backups of the data your service handles are extremely important. If you operate a service that stores any kind of data, it's critical that you implement automatic backups and that you periodically check that those backups are working correctly by performing restores. This helps make sure that you're backing up the right data and that you have well-documented processes for recovering it when things fail. What about the rest of the infrastructure? If you store all your Infrastructure as code, you already have a backup of what your infrastructure should look like. But if your service goes down for some reason, deploying all that infrastructure from scratch might take awhile. That's why many teams keep backup or a secondary instances of their services already up and running. That way, if there's a problem with the primary instance, they can simply point the load balancer or the DNS entries to the secondary instance with minimal disruption to the service. Alternatively, it's common practice to have enough servers running at any time so that if one of them goes down, the others can still handle the traffic, or on a larger scale, have the service running on different data centers around the world, so that if one of the data centers has a problem, the service can still be provided by the instances running in the other data centers. If you're running a service on-premise, you might want to have two different connections to the Internet. This way, if the connection offered by one of your ISPs goes down, you can still connect to the Internet through the other one. When you're running on Cloud, you can mostly rely on your Cloud provider having enough network redundancy. But if you really care about your service staying up no matter what, you might want to run your service on two different Cloud vendors so that if one of the providers has a large outage, you can still rely on the other. Now, imagine you're running your service in one data center. Unfortunately, that data center has just suffered a natural disaster, and all of your instances are down. What do you do? First step, deep breath, don't panic. You need to recover your service from scratch, deploying it in a different data center and getting all your data from backups. As long as the backups are available in other data centers and your Infrastructure is fully stored in a version control system, this should be possible. But figuring out how to successfully bring up the whole system from scratch can take awhile. So you don't want to have to scramble to do it when disaster hits. Instead, you should have a documented procedure that explains all of the steps that you need to take. Since systems evolve over time, you need to make sure that this documentation stays up-to-date. One way to do that is to once in a while pretend that you need to recover your service, follow the documented steps, and check if anything is missing or outdated. Systems will fail. A hundred percent availability is simply not an achievable targets, but being prepared for a failure will let you recover your service quickly and keep your users happy. Up next, we've gathered some resources to give you more info on how to debug problems on the Cloud and to be ready for when things fail. After that, the last quiz of the course awaits you.

# Module Review

## Module 4 Wrap Up: Managing Cloud Instances at Scale

Wow. Look at all that we've covered. In the past videos, we've discussed a lot of different topics related to deploying software in the Cloud. We've learned a bunch of concepts and techniques that we need to take into account when building applications that will run on Cloud, how to keep them running, and how to figure out what's wrong when things don't go according to plan. We started by discussing some of the different options for storing data in the Cloud. We learned how we can use Cloud's flexibility to get the right type of storage and increase it when needed. We then learned about the different approaches to load balancing, which we can use to ensure that our services can be distributed across a number of servers. We also learned how we can get the load balancer to check the health of the back ends to only send request to the servers that are working fine. We looked into how we can build safety into our code changes. We checked out how we can make sure that changes we pushed to production are well-tested, and how we can use development and test environments to let us experiment with changes until we know they'll give a good experience to our users. We then learned about some of the limitations that we can come across when running our services in the Cloud, which are different from the problems we have when running services on physical machines. We also learned some best practices for how to monitor our service, when and how to generate alerts, and we even saw an alert triggering an action. We wrapped up by looking into some of the problems specific to running our instances in the Cloud and how to deal with those. That was a lot of interesting stuff in a short amount of time. Don't you think? Well, we're not done yet. Up next we've got the last graded assessment of the course. In this assessment, you'll put into practice all of the knowledge that you've built up so far. You'll need to figure out what's going on with the deployment that's not behaving as expected and find a way to fix it. But you've got this.