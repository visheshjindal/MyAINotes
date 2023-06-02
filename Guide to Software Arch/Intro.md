# Guide to Solution Architect

## Type of Architects

* Infrastruture Architects: Design Servers, VMs, Storage, Network, etc.
* Software Architects: Design Software, Applications, etc.
* Enterprise Architects: Works with Top Level Management, CTO, CIO, etc.

## Responsibilities of an Architect

Developers knows what can be done. Architects knows what should be done.

* Fast
* Reliable
* Secure
* Easy to Maintain
* Scalable

## Architect Mindset

* Understand the Business
  * Understand their Problem
  * Understand the way they wanna grow
* Define the System's Goals
  * Effect of the system on the Organization
* Figure out who your Client is
* Always keep in Mind what is the thing that really matters to the person you are talking to

## Architecture Process

* Understand the System's Requirements
* Understand the NFR's
* Map the components
* Select the technology stack
* Design the System
* Write the Architecture Document
* Support the Development Team

## Requirement

* What system should do is : Functional Requirement
* What system should deal with: Non Functional Requirement
  * Performance
  * Load
  * Data Volume
  * Concurrent Users
  * SLA
Non functional requirement are important and should be considered.

## Performance

* Always talk in numbers: Talk to client and help them figure out the time
* Latency and throughput: How many task can be done in a given time unit
    e.g. Saving User Data

|  Latency  |   Throughput                 |
|---     |---                         |
|  1 second |   Well designed app > 1000 |
| --        |   Badly designed app < 60  |

## Load

Quantity of work can be done without crashing
|  Throughput          |   Load                         |
|---                 |---                             |
|  100 request/sec      |   500 request without crashing |
*_Always plan for extreme cases_

## Data Volume

* How much data will be accoumlated overtime
* This will help in deciding
  * Database Type
  * Designing Queries

* Two major aspects
  * Day One requirenment
  * Data Growth
* Concurrent Users vs Load

|  Concurrent Users          |   Load                         |
|---                         |---                             |
|  Including "DeadTimes"        |   Actual Requests                 |
*_Rule of 👍🏻 Concurrent = Load X 10_

## Service Level Agreement (SLA)

* Manage client expectations
* 99.99% is not realistic goal

**_NFR Never start working before setting them_**

## Who should define NFR's??

## Architect's Role in NFR

* Framing requirement bounderies
* Discuss numbers

## Application Types

### Web Apps

* User Interface
* User Initiated Actions
* Large Scale
* Short, Focused Actions
* Request and Response Based

### Web API

* Similar Web Apps
* Client is Web servers
* REST based
* Returns Data and not HTMl
* Very Accessible
* Data retrivel and store
* Client initiated actions
* Large scale
* Short, Focused Actions

### Mobile

### Console

### Service

### Desktop

## Selecting the Tech Stack

* Can perform a Task
* Community (Stack Overflow)
* Popularity (Google Trends)

## Backend Technology Stack

* .Net (OOP, Statically typed)
* .Net Core
* Java (OOP, Statically typed)
* node.js
* PHP
* Python

## Frontend Technology Stack

* HTML, JS and CSS
  * Angular & React
* Mobile Native or Cross

## DataStore Tech

* SQL
* NoSQL

## Introduction to *-ilities

* Non functional Requirements are mapped to Quality Attributes(-ilities)
  * Scalability
  * Managebility
  * Modularity
  * Extensibility
  * Testability

### Scalability: Adding computing resource without any interruption

* Scale Up
* Scale Out

### Managebility: Knows whats going on and take action accordingly e.g. Systems to report the problem

### Modularity: A system that is built from building blocks, that can be changed or replaced without affecting the whole system

### Extensibility: A system that its functionality can be extended witout modifying the existing code

### Testability: How easy is to test

## Software Component Architecture

Two levels of Architecture

* Component Architecture
* System Architecture (Bigger Picture)

### Layers

* Represent Horizontal Functionality
  * UI/SI
  * Business Logic
  * Data Access Layer
* Tier vs Layers

### Interfaces

### DI

### SOLID

### Naming Conventions

### Exception Handling

### Logging

## System Architecture

* The Big Picture
* Answer the question?
  * Heavy load handling
  * What will happen if crash?
  * How complicated can this update process is?
  * And many more...

It includes the following:

* Defining Software Components (Services)
* The communicating b/w components
* Designing System Capabilities

### Losse Coupling

Making sure the services are strongly tied with each other

### Stateless (Always)

The Application state is stored in only two places: Data Store and User Interface. State is Application Data.

* Scalibilty
* Redundancy

### Caching

Bring data closer to its consumer so that its retriveal is faster.
What to cache? Cache should hold the data which is frequently accessed and rarely modified.

Cache types: In-memory/In-process and Distributed.

### Messaging

Means of communication between different services.\
Messaging Criteria:

* Performance
* Messaging Size
* Execution Model
* Feedback and Realiability
* Complexity

Types of Messaging:

* REST API (get is 8KB)
* HTTP Push Notification (Pub/Sub) e.g. WebSockets
* Queue e.g. RabbitMQ
* File Based Type or Database based

### Logging & Monitoring

* Central Logging Service
* Correlation ID

## External Considerations

* Deadlines
* Existing Dev Team Skills
* IT Support
* Cost

## Architecture Document

* Goal of the Document
  * What and How
  * Function and NFR
* Audience
  * Project Manager
  * CTO
  * QA
  * Developers
* As simple as possible
* Document Structure
  * Background
  * Requirement
  * Executive Summary
  * Architectural Overview
  * Components Drill-Down

### Background

Describe the system from a Business POV

* System's Role
* Reason for replace
* Expected Business Impact

### Requirements

* Functional
* Non-Functional

### Executive Summary

Explain in the non-technical way for the Non-technical audience:

* Use charts and Diagrams
* Use well known technical terms - sparsely
* Easy to read

### Architectural Overview

* General Description
* High-Level Diagram
* Diagram walk through

### Components Drill Down

* Component Role
* Technology Stack
* Component's Architecture
* Development Instructions

### Advance Architecture Topics

* Microservices
* Event Sourcing
* CQRS