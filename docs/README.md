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
    "narticulationRate" : "",
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
#### Decisions
* wss://deencore.com/sessions/real-time
* Authentication and authorisation done thorugh JWT sessions on webapp beforehand
* Client browser has to send a Ping frame every 10 seconds and server has to respond within 5 seconds with a Pong frame or connection is severed by the server after 2nd attempt. 
* We will not use STOM because it is a text-based protocol with unnecessary header overheads or WOMP because it adds unnecessary latency and complexity. 
* Transportation protocol will be plain websocket
* Serialisation protocol will be a unified binary protobuf schema
* Due to limited bandwidth but good processing power we will use Opus audio codec
* Interval sizing will be a balanced mid-range of 40-60ms
* No WebM or Ogg container to keep overhead low
* HTTP handshake-level auth 
* Initialisation state to get stream between client browser and server up as well as server and C++ analysis backend
* Ending state to get the stream closed and cleaned up
* Include a sequence number to help the server or C++ backend detect dropped buffers
* Dedicate CPU cores to decoding incoming audio chunks, returning data to webapp from server and main CPU cores to ingest incoming streams 

#### Client to server
* session-id
* user credentials in webapp auth and session cookie
* Sample rate, channel count, encoding format, sequence/timestamp data
* If heartbeat is alive then pause otherwise the server can count it as a dropped connection and we can add an automatic timeout limit to avoid an accidental open session or some form of server attack that spins-up multiple sessions and leaves them running with no audio

#### Server to client
* Depends on the active session before starting it you toggle the specific aspects you are practicing (volume, speed, pitch, pauses) - this does not affect client to server because we want to capture all data but server to client we only need to display chosen features.
* We need to return difference between current and target performance and display it visually on frontend
* I am not sure
* I am not sure
* No exercise reccomendation only live in delayed feedback and I might not include them to keep research around feedback frequency and not introduce complexity by adding feedback type

## Private
### gRPC

# Software architecture diagram

