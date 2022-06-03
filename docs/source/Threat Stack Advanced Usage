Threat Stack Advanced Usage Guide
==================================

Lifecycle of an Alert
----------------------

Threat Stack Collects telemetry from a variety of sensors in the environment, outlined below.

*Linux/Containers*

* FIM changes via inotify/FAnotify
* Agent collection of auditd socket
* Docker/Container Telemetry through the use of tscontainerd which utilizes docker APIs to augment existing audit messages referencing the original docker container

*Windows*

* FIM Changes by monitoring a file system driver loaded via the Win32 API HRESULT FilterLoad(LPCWSTR 1pFilterName). FilterLoad is the name of the filter driver, 'ThreatStackFIM'
* Windows events from windows native logging capabilities
* Sysmon Events should sysmon be configured(which is advised)


*Kubernetes*

* Kubernetes API telemetry
* Cloudtrail data supporting managed kubernetes (EKS Cloudtrail data) if applicable

*AWS Control Plane*

* AWS Cloudtrail Logs

Section 2
---------

Fill in here
