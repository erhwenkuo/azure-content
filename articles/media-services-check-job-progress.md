<properties 
	pageTitle="How to Check Job Progress using .NET" 
	description="Learn how to use event handler code to track job progress and send status updates. Code samples are written in C# and use the Media Services SDK for .NET." 
	services="media-services" 
	documentationCenter="" 
	authors="juliako" 
	manager="dwrede" 
	editor=""/>

<tags 
	ms.service="media-services" 
	ms.workload="media" 
	ms.tgt_pltfrm="na" 
	ms.devlang="dotnet" 
	ms.topic="article" 
	ms.date="02/10/2015" 
	ms.author="juliako"/>

#How to: Check Job Progress
This article is one in a series introducing Azure Media Services programming. The previous topic was [How to: Encode an Asset](http://go.microsoft.com/fwlink/?LinkID=301753&clcid=0x409).

When you run jobs, you often require a way to track job progress. The following code example defines the StateChanged event handler. This event handler tracks job progress and provides updated status, depending on the state. The code also defines the LogJobStop method. This helper method logs error details.

	private static void StateChanged(object sender, JobStateChangedEventArgs e)
	{
	    Console.WriteLine("Job state changed event:");
	    Console.WriteLine("  Previous state: " + e.PreviousState);
	    Console.WriteLine("  Current state: " + e.CurrentState);
	
	    switch (e.CurrentState)
	    {
	        case JobState.Finished:
	            Console.WriteLine();
	            Console.WriteLine("********************");
	            Console.WriteLine("Job is finished.");
	            Console.WriteLine("Please wait while local tasks or downloads complete...");
	            Console.WriteLine("********************");
	            Console.WriteLine();
	            Console.WriteLine();
	            break;
	        case JobState.Canceling:
	        case JobState.Queued:
	        case JobState.Scheduled:
	        case JobState.Processing:
	            Console.WriteLine("Please wait...\n");
	            break;
	        case JobState.Canceled:
	        case JobState.Error:
	            // Cast sender as a job.
	            IJob job = (IJob)sender;
	            // Display or log error details as needed.
	            LogJobStop(job.Id);
	            break;
	        default:
	            break;
	    }
	}
	
	private static void LogJobStop(string jobId)
	{
	    StringBuilder builder = new StringBuilder();
	    IJob job = GetJob(jobId);
	
	    builder.AppendLine("\nThe job stopped due to cancellation or an error.");
	    builder.AppendLine("***************************");
	    builder.AppendLine("Job ID: " + job.Id);
	    builder.AppendLine("Job Name: " + job.Name);
	    builder.AppendLine("Job State: " + job.State.ToString());
	    builder.AppendLine("Job started (server UTC time): " + job.StartTime.ToString());
	    builder.AppendLine("Media Services account name: " + _accountName);
	    builder.AppendLine("Media Services account location: " + _accountLocation);
	    // Log job errors if they exist.  
	    if (job.State == JobState.Error)
	    {
	        builder.Append("Error Details: \n");
	        foreach (ITask task in job.Tasks)
	        {
	            foreach (ErrorDetail detail in task.ErrorDetails)
	            {
	                builder.AppendLine("  Task Id: " + task.Id);
	                builder.AppendLine("    Error Code: " + detail.Code);
	                builder.AppendLine("    Error Message: " + detail.Message + "\n");
	            }
	        }
	    }
	    builder.AppendLine("***************************\n");
	    // Write the output to a local file and to the console. The template 
	    // for an error output file is:  JobStop-{JobId}.txt
	    string outputFile = _outputFilesFolder + @"\JobStop-" + JobIdAsFileName(job.Id) + ".txt";
	    WriteToFile(outputFile, builder.ToString());
	    Console.Write(builder.ToString());
	}
	
	private static string JobIdAsFileName(string jobID)
	{
	    return jobID.Replace(":", "_");
	}
