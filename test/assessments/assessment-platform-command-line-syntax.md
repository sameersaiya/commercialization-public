---
title: Assessment Platform Command-Line Syntax
description: Assessment Platform Command-Line Syntax
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: 34286b79-1867-4d0d-8b65-6a0c6a7e5df8
ms.mktglfcycl: plan
ms.sitesec: msdn
ms.author: sapaetsc
ms.date: 05/05/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-oem
---

# Assessment Platform Command-Line Syntax


AXE.exe is a command-line tool that you can use to automate jobs from a script and minimize resource usage. 

A *job* is one or more assessments run simultaneously on a computer. You should create, modify, and save a job by using the [Windows Assessment Console](windows-assessment-console.md). By default, jobs are saved to %UserProfile%\\Documents\\Windows Assessment Console\\Jobs\\. You can't use the command-line options to compose a job. 

AXE.exe is installed with the Windows Assessment Toolkit and, by default to the following location:

<p style="margin: 1em 0 0 1.5em;">%programfiles(x86)%\\Windows Kits\\10\\Assessment and Deployment Kit\\Windows Assessment Toolkit\\*architecture*\\</p>

where *architecture* is either **x86** or **amd64**.

## Command-Line Options


The base syntax for using the Assessment Platform from the command line is:

<p style="margin: 1em 0 0 1.5em;"><strong>axe</strong>&nbsp;<em>job_file</em>&nbsp;[&nbsp;<em>AXE_options</em>&nbsp;]</p>


<p>The following table describes each option. The names of these options are not case-sensitive.</p>
<br/>
<table>
<thead>
<tr class="header">
<th bgcolor="EEEEEE"><p style="text-align: center; margin: 0 0 0 0">Option</p></th>
<th bgcolor="EEEEEE"><p style="text-align: center; margin: 0 0 0 0">Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Help</strong> or <strong>/?</strong></p></td>
<td><p>Displays information about available AXE.exe command-line options.</p></td>
</tr>
<tr class="even">
<td><p><em>job_file</em></p></td>
<td><p>Specifies the job file that you want to run, and <em>job_file</em> can specify a relative path. If the job is in the directory that you're running AXE.exe from, no path is required.</p>
<p>By default, when you create a job in the Windows Assessment Console, it's saved in to %USERPROFILE%\Documents\Windows Assessment Console\Jobs\.</p>
<p style="margin: 1em 1.5em 0 1.5em;"><strong>Note</strong>&nbsp;&nbsp;&nbsp;This option is required if no other parameter that performs an action is specified.</p>
<p>Example:</p>
<code>axe&nbsp;C:\Assessments\MyJobs\Job1.jobx</code></td>
</tr>
<tr class="odd">
<td><p><strong>/Analyze</strong> <em>path_and_file_name</em></p></td>
<td><p>Reanalyzes the results from a job file specified by <em>path_and_file_name</em>. This option requires a job from a package or assessment manifest directly to locate the assessments to reanalyze.</p></td>
</tr>
<tr class="even">
<td><p><strong>/Assessment</strong> <em>assessment_file</em></p></td>
<td><p>Specifies the path and file name of an assessment manifest, <em>assessment_file</em>, to reanalyze in the results file specified.</p>
</td>
</tr>
<tr class="odd">
<td><p><strong>/Timeout</strong>&nbsp;<em>seconds</em></p></td>
<td><p>Specifies the amount of time in <em>seconds</em> that the job will wait for another job to finish before it exits with an error. When <em>seconds</em> is zero, the default, the job will exit immediately if another job is already running.</p>
<p>Example:</p>
<code>axe&nbsp;C:\Assessments\myJobs\Job1.jobx /Timeout 30</code></td>
</tr>
<tr class="even">
<td><p><strong>/NoPublish</strong></p></td>
<td><p>Specifies not to publish the results file to the location that's specified in the job file. When you use this option, the results are saved to the default location, %LOCALAPPDATA%\Microsoft\Axe\Results\.</p>
<p>Example:</p>
<code>axe&nbsp;C:\Assessments\myJobs\Job1.jobx /NoPublish</code></td>
</tr>
<tr class="even">
<td><p><strong>/PublishToSource</strong></p></td>
<td><p>Specifies that AXE.exe update the original results folder when running <strong>/Analyze</strong>. Using <strong>/PublishToSource</strong> is optional, and it is ignored when running a job.</p>
<p><strong>/PublishToSource</strong> may be combined with the publish path, but the publish path will only be used if AXE.exe cannot publish to the original results folder.</p>
<p>Example:</p>
<code>axe&nbsp;C:\Assessments\myJobs\Job1.jobx /NoPublish</code></td>
</tr>
<tr class="odd">
<td><p><strong>/PublishPath</strong>&nbsp;<em>folder_path</em></p></td>
<td><p>Specifies a <em>folder_path</em> to publish the results file to. The path specified by <em>folder_path</em> overrides the publication path, <strong>ResultsPublishPath</strong>, that's specified in the job file. This option is ignored if it's combined with <strong>/NoPublish</strong>.</p>
<p>Example:</p>
<code>axe&nbsp;C:\Assessments\myJobs\Job1.jobx /PublishPath C:\Assessments\myResults</code></td>
</tr>
<tr class="even">
<td><p><strong>/RemoveRestart</strong></p></td>
<td><p>Specifies that any existing, pending job-restart task should be removed.</p>
<p style="margin: 1em 1.5em 0 1.5em;"><strong>Note</strong>&nbsp;&nbsp;&nbsp;The <strong>/JobFile</strong> option isn't needed when you use this option.</p>
<p>When you run a job, the assessment creates a task to restart the job if there's a system failure, like a loss of power. When you use this option, the task is removed from the Task Scheduler. If no job-restart task is pending, the assessment will return an error to inform you that the task doesn't exist.</p>
<p>Example:</p>
<code>axe&nbsp;/RemoveRestart</code></td>
</tr>
<tr class="odd">
<td><p><strong>/NoWarnings</strong></p></td>
<td><p>Suppresses warning messages. This is an optional parameter.</p>
<p>Example:</p>
<code>axe&nbsp;C:\Assessments\myJobs\Job1.jobx /NoWarnings</code></td>
</tr>
<tr class="even">
<td><p><strong>/Pause</strong></p></td>
<td><p>Pauses AXE.exe after the job finishes. You can then see any errors or other information in the console before AXE.exe exits and the console closes. Exiting continues when you press a key.</p>
<p>Example:</p>
<code>axe&nbsp;C:\Assessments\myJobs\Job1.jobx /Pause</code></td>
</tr>
<tr class="odd">
<td><p><strong>/JobParameter</strong> <em>parameter</em><strong>=</strong><em>value</em></p></td>
<td><p>Specifies a <em>value</em> to override a job <em>parameter</em> that may exist in the job manifest. You can use <strong>/JobParameter</strong> up to 100 times to specify multiple job parameters. If duplicate parameter names appear, the assessment uses the last value supplied for that name. Using <strong>/JobParameter</strong> is optional.</p>
<p>The <strong>/PublishPath</strong> option takes precedence over setting the <strong>ResultsPublishPath</strong> job parameter with this option.</p>
<p>Example:</p>
<code>axe&nbsp;C:\Assessments\myJobs\Job1.jobx /JobParameter iterations=1</code></td>
</tr>
<tr class="even">
<td><p><strong>/DisplayLog</strong>&nbsp;<em>path_and_file_name</em></p></td>
<td><p>Displays the content of an Event Trace Log (ETL) file specified by <em>path_and_file_name</em>, which can contain wildcard characters. AXE.exe writes an ETL file when running a job and displays its location in the console.</p>
<p>The default location of the log file is %LOCALAPPDATA%\\Microsoft\\Axe\\Logs\\<em>GUID</em>, where <em>GUID</em> is a GUID that is generated randomly for each new job. The job results file in the <strong>SessionLogFiles</strong> node also contains the full location. This node specifies all of the log files.</p>
<p style="margin: 1em 1.5em 0 1.5em;"><strong>Note</strong>&nbsp;&nbsp;&nbsp;All of the ETL files are automatically converted into a single AxeLog.txt file that is saved in the results directory. You can open this file by using Notepad.</p>
<p>Example:</p>
<code>axe&nbsp;/DisplayLog %LOCALAPPDATA%\Microsoft\Axe\Logs\E5A6CB43-C!CE-4FC1-8170-13B002E250B36\AxeLog-000.etl</code></td>
</tr>
</tbody>
</table>

 

**Benefits:**

-   Running a job at the command prompt uses fewer resources and has less impact on performance metrics.

-   You can use command-line options to automate a job.

-   Command-line options provide additional parameters that aren't available in the Windows Assessment Console.

**Limitations:**

-   The job that you run can't be one of the preconfigured jobs or one of the single assessments that the Windows Assessment Toolkit provides.

-   You can't create or modify a job by using AXE.exe. You must use the Windows Assessment Console.

## Related topics


[Windows Assessment Console Overview](windows-assessment-console-overview.md)

 

 







