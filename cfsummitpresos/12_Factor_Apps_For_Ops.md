^ Open this presentation with [Deckset](http://www.decksetapp.com/)


![fit] (cfsummit_ppt1/Slide1.jpg) 

---

![fit] (cfsummit_ppt1/Slide2.jpg)

---
# The 12 factor App for Operations


---

### The Basics

> much of this source: http://www.clearlytech.com/2014/01/04/12-factor-apps-plain-english/

---

# \#1: Codebase

* One codebase tracked in revision control, many deploys
* Put all your code in a source control system. Heck, just put it up on GitHub from the start.

Importance: Non-negotiable. Everyone does this, and developers will laugh at you if you aren’t.

---

# \#2: Dependencies

* Dependencies must be explicitly declared
* They should be declared with the rest of the code, and tracked the same way
* Dependencies tracking should contain version numbers of dependencies

Importance: High. Without this, your team will have a constant slow time-suck of confusion and frustration, multiplied by their size and number of applications. Spare yourself.

---

# \#3: Config

* Config belongs in the environment if possible - it varies between deploys, but the code doesn't
* Includes access credentials, logging config, etc.
* Should be read at runtime, not preprocessed into code.

Importance: Medium. You can get away without it, but its sloppy.

---

# \#4: Backing Services

* Anything your application uses as a resource (database, queueing system, email, cache) should be referenced with 'bindings' to these services.
* All applications deployed with explicit references to data services in manifest.yml (mechanism for User Provided Services)
* Possibly discovered via:
  * Spring Cloud (pay attention to configuration files)
  * Discovery mechanism (Zookeeper, etcd, Consul etc )
  * Environment

Importance: High. Its easy to do, and follows with the Config rules above

^Rags

---

# \#5: Build Release Run

* Build, Release and Run are separate stages for the application life cycle.
* Use profiles (ala Spring Boot) for running in different environments. Profiles should be easily grepable.

> The process of turning the code into a bundle of scripts, assets and binaries that run the code is the build. The release sends that code to a server in a fresh package together with the nicely-separated config files for that environment (see Config again). Then the code is run so the application is available on those servers.

^Rags

---

# \#6: Processes

* As a rule, you want each of those instances of running code to be stateless.
* Seperation of concerns - each microservice is a single process
* This makes your app more resilient, and easier to recover

Importances: High. Makes tools like CF even possible

^Rags

---

# \#7: Port Binding

* Your app should not assume its the only thing running on the same port
* Bind an internal port/IP to external URL using load balancer

Importances: Moderate. Most tools like Heroku, CF do this for you, and enforce it

^Rags

---

# \#8: Concurrency

* An extension of 6 above.
* Not necessarily required for certain aspects (single process workers, etc)

Importances: Low. But it helps scale certain parts.

^Rags

---

# \#9: Disposability

* Losing a process should be a non event
* No loss of state for user if we lose a process
* Startup times should be low

Importances: Moderate. Makes it easy to release quickly

^Rags

---

# \#10: Dev / Prod Parity

* Dev MUST == Production in config, but not performance
* Following the above helps do this

Importances: Critical. You can't do continuous push (or push at all) safely without it.

---

# \#11: Logs

* Log *everything*
  * Storage is cheap
  * Searching is cheap
* Logs help fix problems *after* they happen
* Use tokens for specific flows

Importances: High. Can't debug without logs.

---


# \#12: Admin Processes

* Use your app/framework for these... build in the tools as needed.
* Don’t run updates directly against a database
* Don’t run them from a local terminal window
* ChatOps can help here

Importances: Moderate. Helps prevent mistakes

---

# More Resources

* [Pivotal Podcasts: Episode 23 (Operational transformation) ](http://blog.pivotal.io/podcasts-pivotal) 
* [You Build it, you run it - an interview with Werner Vogels] (https://queue.acm.org/detail.cfm?id=1142065)

---

# 6 Laws of Systems that never stop

* Isolation
* Concurrency
* Failure Detection
* Fault Identification
* Live Code Upgrade
* Stable Storage

[http://www.infoq.com/presentations/Systems-that-Never-Stop-Joe-Armstrong] (http://www.infoq.com/presentations/Systems-that-Never-Stop-Joe-Armstrong)