---
tags: [Dev Training]
title: Dev Training Documentation. Process Tasks
created: '2022-10-10T08:47:48.287Z'
modified: '2024-11-05T08:51:34.474Z'
---

# Dev Training Documentation. Process Tasks
https://docs.google.com/document/d/1bnpmk603Zau8XTuIxKVGM74EXOdwbPpDOtbQHmFno58/edit#heading=h.4zpzkx9au4vp
___

## About
Are a lot of process simple task running in background. These task are not much complexy.
An samples of these task are in: ..\rightfind-enterprise\Build\AWSConfigs\AWSRFEDev2016\ in a ProcessTask.config file.
This configuracion it already in a database:
SELECT top 50 * FROM LibraryFieldSetTrigger WHERE TriggerType = 0 *Scheduled = 0, RealTime = 1*

## General Classes
Principal projects implicated: VLServerComponents, VLShared, VLServicesConsole.
- JobProcessor
- ProcessTaskJP : **JobProcessor**
    * Principal method to run this task is Run()
    * ProcessTaskJob (ProcessTaskJob)Job. Using reflection to running task on a Run() method:
        - Type oTargetType = Type.GetType(strTypeName, true, true);
        - object oTarget = oTargetType.Assembly.CreateInstance(ProcessTaskJob.Class, true);
- Job >> "SELECT * FROM JobsPending WITH (NOLOCK) WHERE (Status=JobStatus.Idle OR Status=JobStatus.Approved) AND ServerId={3} AND NextOccurrence <= {4} ORDER BY Priority DESC, NextOccurrence ASC";
    * JobProcessor.Get(Job)
    * JobProcessor.BeginExecution(Job)
- ProcessTaskJob : **Job**. This classes implements a Populate and Save methods.
- Classes which implement the **IProcessTask** interface
- LibraryTriggerProcessTask.Execute()

In a Service.cs class on VLJobServer project load and execute jobs and processTask
Method **Service.Start()**:

+ **`AddComponent(new VLServerJobComponent())`**;
    + Load Jobs defined into JobsPending table on Database.
        - `Job[] aJobs = Job.GetTopJobsSql(VLServerJobSettings.MaxRunning, serverId);`        
    + Create a Job:
        - `oJob = Job.Create((JobType)oReader.["Type"]`);`
    + Execute Job:
        - `JobProcessor.Get(oJob).BeginExecution(oJob, serverId, funcCB)`
    

+ **`AddComponent(new VLServerProcessTaskComponent());`**
    + Load process defined into `<REPO>\Build\AWSConfigs\AWSRFEDev2016\rdev1proc1\ProcessTask.config` file. First step needs parse all process settings, parameters,...
        - `oData = VLServerProcessTaskDataList` 
    + Create a task to run a process defined into processTask.config file.
        - `ScheduledItem oItem = new ProcessTaskScheduledItem(oData);`
    + Execute this process task
        - `oItem.ExecuteAsync();`

All proccess task defined into ProcessTask.config needs a IProcessTask implementation in a class into VLShared or VLServerComponents.
This inteface define a Execute method that it's necessary implemented in a derived class.


    



##
