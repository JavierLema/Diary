---
tags: [Dev Training]
title: Dev Training Documentation. Job Server.
created: '2022-09-30T11:54:29.026Z'
modified: '2024-11-05T08:51:34.430Z'
---

# Dev Training Documentation. Job Server.

https://docs.google.com/document/d/15OltMX0r1VXtbq1-e95G7EIuGe8YsS6JSHOG4VBkyqs/edit

*****************************
## About
###The Job Server is one of the most critical and essential parts in all RFE environments ###
Job Server it's a modulable application. In actuality contains this module:
* Jobs
* Order Process
* Notification - send notifications
* Print Process - print documents (for example, invoices)
* File Watch - check some folders on FTP and use found PDFs to fulfill orders
* Communication Server
* ProcessMail - check some mailboxes and create orders based on the received emails
* Indexing - indexing of new (imported) content
* ProcessTask - cleanup and update
* Purge - removing
* Maintenance
* TaskMaster - a new feature that allows spreading the load between servers
* Converting - converting of documents

***Important***
* To start VLJobServer project, you need to comment AtalaUtils.Init() line on Service.cs or check "Prefer 32-bit" on the Build tab in project properties.
* To visualize all JobServers status, you must launch a VLServicesConsole project.
    * In this project, the user can see all JobServers instances on CCC for different envionments. The user can examine all server properties, configurations, ....
    * The user can start and stop all server instances.

## Involved classes

* VLJobServer -> Main.cs. This project runs a Service with a Singleton pattern and loading all components
* VLServerComponents -> Components to loading
    * VLServerJobComponent class contains a ***PRINCIPAL*** method ThreadWorkProc():
        - JobProcessor. This class manages all threads into JobServer.
            * static public JobProcessor Get(Job p_oJob) -> This method returns a Job type to execute. JobType it's an enum defined into JobEnums.cs.
            * public virtual bool BeginExecution(Job p_oJob, short serverId, JobCompleteCB p_oCB).
            * Create a private DbCommand variable to update progress on DB -> In a thread?

* VLServicesConsole -> Is an application to monitor the status of the different Job Server applications running in different environments.
    - You can start/stop components from this application.
    - If you want to ***debug JobServer***, you only need to put a breakpoint into a ***ThreadWorkProc() method and stop/start the component***.

## Proposed challenges and Key points
Investigate two very important components:
* VLServerOrderComponent > All the orders processing engine.
* VLServerJobComponent > For the Import/Export RFE ecosystem.
