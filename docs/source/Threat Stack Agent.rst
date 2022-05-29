Threat Stack Agent
=====================================

Deploying Threat Stack 
----------------------
Before you install the Threat Stack host-based Agent, you must prepare your Linux distribution to work with the Agent. 

The Threat Stack host-based Agent uses the Linux Audit Framework to collect files, network, and process data.  

 

Check for other Agents
----------------------

.. note::
   
  Conflict can occur between the Threat Stack host-based Agent and other tools leveraging these kernels. Before deploying the Agent, ensure no other tools
  use these kernels. **This is the result of a known Linux limitation where only one process can bind to the AuditD socket. 
  https://man7.org/linux/man-pages/man5/auditd.conf.5.html


Code Block to Check for The Threat Stack Agent on the machine

.. code-block:: 
   
   hello world!


Install the Threat Stack Agent
------------------------------
*Prerequisites*

* Access to the Threat Stack Console 
* Access to host either via CLI or RDP 

*Linux/Windows Distributions*


The Threat Stack application walks customers through an Agent install on the Servers page.

Log into Threat Stack > Click Servers. The Servers page displays. 

Select Agent 3.x. The + Add New Server dialog displays. Proceed to the set of instructions below, specific to your Linux or Windows distribution. 
