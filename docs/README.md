# Software architecture brief
# Table of contents
* [1 — Requirements](#requirements)
    * [1.1 — Functional requirements](#functional-requirements)
    * [1.2 — Non-functional requirements](#non-functional-requirements)
    * [1.3 — Constraints](#constraints)
* [2 — API Design](#api-design)
* [3 — Software architecture diagram](#software-architecture-diagram)

# Requirements
## Functional requirements
### Use cases
1. User registration
2. User login
3. User accessing a dashboard
4. User creating a target vocal profile
5. User starting a session
6. User uploading a voice recording
8. User getting feedback (delayed and real-time)
9. User extracting speech features — voice, speed, pitch and pause pattern features
10. User establishing a their baseline

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

---

## Non-functional requirements
### Performance

* Low response time
* High throughput

---

### Scalability

* Vertical scalability required
* Horizontal scalability not required
* Team scalability not required

---

### Availability

* High uptime is required
* Low mean time between failures (MTBF) is required
* Low mean time to recovery (MTTR) is required 

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

# API Design
## Public
### REST
#### Entities
* Users
* Analytics
* Vocal-profiles 
* Sessions


#### URIs
* Users/
    * {user-id}
* Vocal-profiles/
    * baseline
    * target
        * {target-vocal-profile-id}
* Analytics/
    * {Analytics-id}
* Sessions/
    * {target-vocal-profile-id} 
        * real-time
            * volume
            * speed
            * pitch
            * pauses  
        * {target-vocal-profile-id}/upload
            * volume
            * speed
            * pitch
            * pauses

#### Resource representation
GET /users/
{
  "firstName": "Bob",
  "lastName": "Spalding"
}

POST /users/
{
    "firstname" : "Anna",
    "lastname" : "Egger",
    "age" : "27",
    "gender" : "female",
    "ethnicity" : "Austrian",
    "educationLevel" : "Phd",
    "employmentStatus" : "Employed",
    "annualIncome" : "100,000",
    "location" : {
        "city" : "Vienna",
        "country" : "Austria",
        "regionType" : "Urban"
    },
    "maritialStatus" : "single",
    "heathAndDisability" : [
        "none"
    ]
}


PUT /users/
{
    "firstname" : "Anna",
    "lastname" : "Egger",
    "age" : "27",
    "gender" : "female",
    "ethnicity" : "Austrian",
    "educationLevel" : "Phd",
    "employmentStatus" : "Employed",
    "annualIncome" : "100,000",
    "location" : {
        "city" : "Vienna",
        "country" : "Austria",
        "regionType" : "Urban"
    },
    "maritialStatus" : "single",
    "heathAndDisability" : [
        "none"
    ]
}

POST /vocal-profiles/baseline-profiles
{
    "datetime" : "18/10/2026,10:30:46",
    "rootMeanSquare" : ,
    "soundPressureLevel" : ,
    "energyEntropy" : "",
    "intensityContour" : "",
    "fundamentalFrequency" : "",
    "fundamentalFrequencyVariability" : "",
    "pitchRange" : "",
    "pitchContours" : "",
    "speechRate" : "", 
    "articulationRate" : "",
    "pauseDuration" : "",
    "pauseFrequency" : "",
    "vowelToConsonantRatio" : "",
    "syllableDurationVariability" : ""
}

POST /vocal-profiles/target-profiles
{
    "datetime" : "18/10/2026,10:30:46",
    "rootMeanSquare" : ,
    "soundPressureLevel" : ,
    "energyEntropy" : "",
    "intensityContour" : "",
    "fundamentalFrequency" : "",
    "fundamentalFrequencyVariability" : "",
    "pitchRange" : "",
    "pitchContours" : "",
    "speechRate" : "", 
    "articulationRate" : "",
    "pauseDuration" : "",
    "pauseFrequency" : "",
    "vowelToConsonantRatio" : "",
    "syllableDurationVariability" : ""
}

GET /vocal-profiles/baseline-profiles
{
    "datetime" : "18/10/2026,10:30:46",
    "rootMeanSquare" : ,
    "soundPressureLevel" : ,
    "energyEntropy" : "",
    "intensityContour" : "",
    "fundamentalFrequency" : "",
    "fundamentalFrequencyVariability" : "",
    "pitchRange" : "",
    "pitchContours" : "",
    "speechRate" : "", 
    "articulationRate" : "",
    "pauseDuration" : "",
    "pauseFrequency" : "",
    "vowelToConsonantRatio" : "",
    "syllableDurationVariability" : ""
}

GET /vocal-profiles/target-profiles
{
    "datetime" : "18/10/2026,10:30:46",
    "rootMeanSquare" : ,
    "soundPressureLevel" : ,
    "energyEntropy" : "",
    "intensityContour" : "",
    "fundamentalFrequency" : "",
    "fundamentalFrequencyVariability" : "",
    "pitchRange" : "",
    "pitchContours" : "",
    "speechRate" : "", 
    "articulationRate" : "",
    "pauseDuration" : "",
    "pauseFrequency" : "",
    "vowelToConsonantRatio" : "",
    "syllableDurationVariability" : ""
}

GET /vocal-profiles/baseline-profiles/{baseline-profile-id}
{
    "datetime" : "18/10/2026,10:30:46",
    "rootMeanSquare" : ,
    "soundPressureLevel" : ,
    "energyEntropy" : "",
    "intensityContour" : "",
    "fundamentalFrequency" : "",
    "fundamentalFrequencyVariability" : "",
    "pitchRange" : "",
    "pitchContours" : "",
    "speechRate" : "", 
    "articulationRate" : "",
    "pauseDuration" : "",
    "pauseFrequency" : "",
    "vowelToConsonantRatio" : "",
    "syllableDurationVariability" : ""
}


GET /vocal-profiles/target-profiles/{target-profile-id}
{
    "datetime" : "18/10/2026,10:30:46",
    "rootMeanSquare" : ,
    "soundPressureLevel" : ,
    "energyEntropy" : "",
    "intensityContour" : "",
    "fundamentalFrequency" : "",
    "fundamentalFrequencyVariability" : "",
    "pitchRange" : "",
    "pitchContours" : "",
    "speechRate" : "", 
    "articulationRate" : "",
    "pauseDuration" : "",
    "pauseFrequency" : "",
    "vowelToConsonantRatio" : "",
    "syllableDurationVariability" : ""
}

PUT /vocal-profiles/target-profiles/{target-profile-id}
{
    "rootMeanSquare" : ,
    "soundPressureLevel" : ,
    "energyEntropy" : "",
    "intensityContour" : "",
    "fundamentalFrequency" : "",
    "fundamentalFrequencyVariability" : "",
    "pitchRange" : "",
    "pitchContours" : "",
    "speechRate" : "", 
    "articulationRate" : "",
    "pauseDuration" : "",
    "pauseFrequency" : "",
    "vowelToConsonantRatio" : "",
    "syllableDurationVariability" : ""
}

DELETE /vocal-profiles/target-profiles/{target-profile-id}
DELETE /vocal-profiles/baseline-profiles/{baseline-profile-id}

POST /sessions/real-time
POST /sessions/upload/

GET /analytics/
{
    "rootMeanSquare" : ,
    "soundPressureLevel" : ,
    "energyEntropy" : "",
    "intensityContour" : "",
    "fundamentalFrequency" : "",
    "fundamentalFrequencyVariability" : "",
    "pitchRange" : "",
    "pitchContours" : "",
    "speechRate" : "", 
    "articulationRate" : "",
    "pauseDuration" : "",
    "pauseFrequency" : "",
    "vowelToConsonantRatio" : "",
    "syllableDurationVariability" : ""
}

GET /analytics/{session-id}
{
    "rootMeanSquare" : ,
    "soundPressureLevel" : ,
    "energyEntropy" : "",
    "intensityContour" : "",
    "fundamentalFrequency" : "",
    "fundamentalFrequencyVariability" : "",
    "pitchRange" : "",
    "pitchContours" : "",
    "speechRate" : "", 
    "articulationRate" : "",
    "pauseDuration" : "",
    "pauseFrequency" : "",
    "vowelToConsonantRatio" : "",
    "syllableDurationVariability" : ""
}

#### HTTP methods for operations on resource
POST /users/
GET /users/
PUT /users/
DELETE /users/

POST /vocal-profiles/baseline-profiles
POST /vocal-profiles/target-profiles
GET /vocal-profiles/baseline-profiles
GET /vocal-profiles/baseline-profiles/{baseline-profile-id}
GET /vocal-profiles/target-profiles
GET /vocal-profiles/target-profiles/{target-profile-id}
PUT /vocal-profiles/target-profiles/{target-profile-id}
DELETE /vocal-profiles/target-profiles/{target-profile-id}
DELETE /vocal-profiles/baseline-profiles/{baseline-profile-id}

POST /sessions/real-time
POST /sessions/upload/
GET /sessions/{session-id}

GET /analytics/
GET /analytics/{session-id}

### Websocket

## Private
### gRPC

# Software architecture diagram

