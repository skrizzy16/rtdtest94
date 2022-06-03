Threat Stack Advanced Usage Guide
==================================


Types of Events
---------------

Threat Stack Collects telemetry from a variety of sensors in the environment, outlined below. They are all stored in JSON format

*Linux/Containers*

* FIM changes via inotify/FAnotify
* Agent collection of auditd socket
* Docker/Container Telemetry through the use of tscontainerd which utilizes docker APIs to augment existing audit messages referencing the original docker container

Sample Linux Host Event


.. image:: _static/SampleLinux.png

Sample Linux Raw Event JSON


Sample Container Host Event

.. image:: _static/SampleContainer.png


Sample Container Raw Event JSON
   
   
*Windows*

* FIM Changes by monitoring a file system driver loaded via the Win32 API HRESULT FilterLoad(LPCWSTR 1pFilterName). FilterLoad is the name of the filter driver, 'ThreatStackFIM'
* Windows events from windows native logging capabilities
* Sysmon Events should sysmon be configured(which is advised)

Sample Windows Host Event

.. image:: _static/SampleWinsec.png

Sample Windows Raw JSON

*Kubernetes*

* Kubernetes API telemetry
* Cloudtrail data supporting managed kubernetes (EKS Cloudtrail data) if applicable

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

.. note::
   
   It can take 10-15 minutes for a suppression update, as well as 10-15 minutes for new rules to kick in for our backend to update. In addition, while      alerts are retained for 1 year, there is a 60k Alert UI cap. As a result, if you were to hypothetically aggregate 20k of alerts per day, you would      only have 3 days of visibility at a time.


Suppression Best Practices
--------------------------
When drafting suppressions, there is an inherent risk in overtly suppressing out bad activity. For example, suppressing all root user activity.

*Good Suppression Example*

.. codeblock::
  
   user = 'root' AND tty = null AND cwd = '/usr/bin' AND session = '4294967295' AND auid = '4294967295' AND 
   arguments = 'ps -e -o pid,ppid,state,command' AND exe = '/usr/sbin/chronyd'

  

*Bad Suppression Example that will not work, due the event_time, agent_id will only apply to that agent_id and PID being recycled*

.. codeblock::

  pid = '3081' AND user = 'root' AND agent_id = "abcdef-1234-4va1-ad42-555bd87fa32a" AND command = 'ps' AND event_time = '1654270691800'
  

*Bad Suppression Example that will work, but is too broad*

.. codeblock::

  user = 'root' AND command = 'ps' 
  


EventSearch
============

When leveraging event Search I advise leveraging the supported key words and operators use case here:

https://threatstack.zendesk.com/hc/en-us/articles/200194909-Supported-Keys-and-Operators

