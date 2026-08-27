# Table of content
* [1 — Software architecture](#software-architecture)
    * [1.1 — Functional requirements](#functional-requirements)
    * [1.2 — Non-functional requirements](#non-functional-requirements)
    * [1.3 — Constraints](#constraints)
    * [1.4 — API Design](#api-design)
* [2 — Decisions](#decisions)
    * [2.1 — Functional requirement decisions](#functional-requirements-1)
    * [2.1 — Non-functional requirement decisions](#non-functional-requirements-1)
    * [2.1 — Constraint decisions](#constraints-1)
    * [2.3 — API design decisions](#api-design-1)

 

# Software architecture

## Functional requirements
### Use cases
1. User registration
2. User login
3. User accessing a dashboard
4. User creating a target vocal profile
5. User starting a session
6. User uploading a voice recording
7. User getting real-time feedback
8. User getting delayed feedback 
9. User wants to extract speech voice, speed, pitch and pause pattern features

---

### Importance VS Feasability

*Include or die*
1. User goal vocal profiles
2. User uploading a voice recording
3. User dashboard
4. User wants to extract speech voice, speed, pitch and pause pattern features

*Strongly consider*
1. User starting a session
2. User getting delayed feedback
3. User getting real-time feedback
4. User login
5. User registration

*Remove*
* N/A

---

### Userflows

*Registration*
![Registration Userflow](imgs/Registration.png)

*Login*
![Login Userflow](imgs/Login.png)

*Voice recording upload*
![Voice recording upload Userflow](imgs/Voice%20recording%20upload.png)

*Starting session*
![Starting session Userflow](imgs/Starting%20session.png)

## Non-functional requirements

### Performance

* Response time
* Throughput

---

### Scalability

* Vertical 
* Horizontal 
* Team 

---

### Availability

* Uptime
* Downtime
* Mean time between failures (MTBF)
* Mean time to recovery (MTTR)

---

### Fault tolerance

* Failure prevention
    * Spatial replication and redundancy
    * Time replication and redundancy
* Failure detection and isolation
    * Monitoring service
* Recovery
    * Automatic alerts
    * Failover 
    * Rollback
    * Restart
    * Auto-scaling
    * Stop
    * SOPs

---

### SLA, SLO, SLI

* Service-level-agreement
* Service-level-objectives
* Service-level-indicators

---

### Non-functional trade-off decisions

* Increase availability by sacrificing scalability
* Increase performance by sacrificing scalability
* Trade some performance for higher security (if necessary get some more performance by trading some availability)

---

## Constraints 

### Technical constraints

*Workstation*
* Dell T7910

*CPU*
* Intel Xeon E5-2640 v4

*RAM*
* 32Gb DDR4 ECC 24000Hz (4x8Gb)

*HDD*
* 3TB

*SSD*
* 128Gb

*GPU*
* NVIDIA GeForce GT 1030

*Tech stack*
* Java
* Springboot
* C++
* Python
* HTML
* CSS
* JS
* MySQL

*Platform*
* Web

---

### Business constraints

*Time*
* 6-Month

*Budget*
* £0

---

### Regulatory constraints

*GDPR and ethics*
* Privacy
* Transparency
* Consent
* Security
* Accountability
* Retention

---

## API design
### Public APIs
- REST
- websocket

### Private APIs
- gRPC

---
## Large scale systems
### Load balancer 
**HAProxy**
* Both level 4 and level 7 routing levels required
* Performance over flexibility

### Message brokers
**Kafka or redpanda**
* Stream message pattern required
* Data delivery guarantee not required 
* Standard web protocols required nothing specific 


### API Gateway
**KrakenD**
* Changing settings via code is fine

# Decisions
## Functional requirements
### Importance VS Feasability 
An importance VS feasability graph was used to plot use cases and categorise them into "include or die", "strongly consider" and "Remove"

## Non-Functional requirements
### Context
* Single-user application
* Locally-hosted application
* Internal-use only
* Every-day use application

---

### Availability VS Scalability
*Judgement* 
* Scalability should be de-prioritised because it is a single-user, locally-hosted, internal-use only application
* Availability should be prioritised because it is an every-day use type of application

*Decision*
* Trade scalability for availability in architecture and implementation 

---

### Performance VS Scalability
*Judgement* 
* Scalability should be de-prioritised because it is a single-user, locally-hosted, internal-use only application
* Performance should be prioritised because it is a real-time signal processing, speech feature extraction, every-day use type of application

*Decision*
* Trade scalability for performance in architecture and implementation 

---

### Security VS Performance
*Judgement* 
* Security should be prioritised because this application will be used in research so some performance can be traded(this is a decision between 2 important aspects where 1 is being prioritised) to comfortably meet GDPR and ethics 

*Decision*
* Trade some performance for security in architecture and implementation (You can re-gain performance by trading some availability if necessary)

## Constraints

## API Design
1. User registration (REST)
2. User login (REST)
3. User accessing a dashboard (REST)
4. User creating a target vocal profile (REST)
5. User starting a real-time recording session (websocket)
6. User uploading a voice recording (REST)
7. User getting real-time feedback (websocket)
8. User getting delayed feedback (REST) 
9. User wants to extract speech voice, speed, pitch and pause pattern features (backend sends data to webapp through gRPC)

Python audio signal processing and analysis service communication with springboot web application (gRPC)

## Large scale system
### Load balancer
* Load balancing not required because there is only 1 instance of each service and only one server

### Message broker
* Event based message broker required because there will be multiple asynch and synch communications between services happening

### API Gateway
* API gateway required because altough this is a single-user application an element of my dissertation is about conducting research with multiple users (10 or below) and making sure that this is safe so API gateway will be a good security addition

### CDN
* CDN not required as this is serving the same user locally and during research within the same city