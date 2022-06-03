Threat Stack Advanced Usage Guide
==================================


Types of Events
---------------

Threat Stack Collects telemetry from a variety of sensors in the environment, outlined below. They are all stored in JSON format.

*Linux/Containers*

* FIM changes via inotify/FAnotify
* Agent collection of auditd socket
* Docker/Container Telemetry through the use of tscontainerd which utilizes docker APIs to augment existing audit messages referencing the original docker container

Sample Linux Host Event

Sample Linux Raw Event JSON

Sample Container Host Event

Sample Container Raw Event JSON

*Windows*

* FIM Changes by monitoring a file system driver loaded via the Win32 API HRESULT FilterLoad(LPCWSTR 1pFilterName). FilterLoad is the name of the filter driver, 'ThreatStackFIM'
* Windows events from windows native logging capabilities
* Sysmon Events should sysmon be configured(which is advised)

Sample Windows Host Event

Sample Windows Raw JSON




*Kubernetes*

* Kubernetes API telemetry
* Cloudtrail data supporting managed kubernetes (EKS Cloudtrail data) if applicable

Sample Kubernetes Event

Sample Kubernetes Raw JSON



*AWS Control Plane*

* AWS Cloudtrail Logs


All the above telemetry are referred to collectively as *events*. You can see all the raw events in an organization by navigating to the Threat Stack Console, and navigating to the 'events' section of the platform.


Lifecycle of an event and alert
-------------------------------

All the above telemetry is captured, and evaluated against our rules engine on our backend. The Logic is as follows.


1. Collect the event data from the sensor(s) in the organization environment.
2. Evaluate the filters against a rule logic.
3. If the event data matches parameters for a rule, while also not be suppressed against the alert will fire.

events are retained for 72 hours/3 days from collection, if the activity is collected as an alert, it will be retained for 1 calendar year. There is no way to delete an alert from the platform. If you dismiss it, it will move to the 'dismissed' tab 

Lets look at an example in my personal organization.

Investigating Root Cause of activity (linux)
--------------------------------------------


Investigating Root Cause of activity (windows)
----------------------------------------------

Investigating Root Cause of activity (cloudtrail)
-------------------------------------------------


