<properties 
	pageTitle="Add Mobile Services to an existing app (iOS) | Mobile Dev Center" 
	description="Learn how to get started using Mobile Services to leverage data in your iOS app." 
	services="mobile-services" 
	documentationCenter="ios" 
	authors="krisragh" 
	manager="dwrede" 
	editor=""/>

<tags 
	ms.service="mobile-services" 
	ms.workload="mobile" 
	ms.tgt_pltfrm="" 
	ms.devlang="objective-c" 
	ms.topic="article" 
	ms.date="10/10/2014" 
	ms.author="krisragh"/>

# Add Mobile Services to an existing app

[AZURE.INCLUDE [mobile-services-selector-get-started-data](../includes/mobile-services-selector-get-started-data.md)]

This topic shows you how to use a Azure Mobile Services to leverage data in an iOS app. In this tutorial, you will download an app that stores data in memory, create a new mobile service, integrate the mobile service with the app, and view the changes to data made when running the app.

The mobile service that you create in this tutorial supports the .NET runtime in the Mobile Service. This allows you to use .NET languages and Visual Studio for server-side business logic in the mobile service. To create a mobile service that lets you write your server-side business logic in JavaScript, see the [JavaScript backend version] of this topic.

>[AZURE.NOTE]This tutorial is intended to help you better understand how Mobile Services enables you to use Azure to store and retrieve data from an iOS app. As such, this topic walks you through many of the steps that are completed for you in the Mobile Services quickstart. If this is your first experience with Mobile Services, consider first completing the tutorial [Get started with Mobile Services].
</div>

This tutorial walks you through these basic steps:

1. [Download the iOS app project]
2. [Create the mobile service]
3. [Download the service locally]
4. [Test the mobile service]
5. [Publish the mobile service to Azure]
7. [Update the app to use Mobile Services]
8. [Test the app against Mobile Services]

This tutorial requires the following:

+ [Mobile Services iOS SDK] and [XCode 4.5][Install Xcode] and iOS 5.0 or later versions.
+ Visual Studio 2013 (you can get [Visual Studio Express for Web](http://go.microsoft.com/p/?linkid=9832232) for free).
+ A Microsoft Azure account. If you don't have an account, you can create a free trial account in just a couple of minutes. For details, see <a href="http://www.windowsazure.com/en-us/pricing/free-trial/?WT.mc_id=A756A2826&amp;returnurl=http%3A%2F%2Fwww.windowsazure.com%2Fen-us%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started-with-data-ios%2F" target="_blank">Azure Free Trial</a>.

##<a name="download-app"></a>Download the GetStartedWithData project

This tutorial is built on the [GetStartedWithData app][GitHub], which is an iOS app. The UI for this app is identical to the app generated by the Mobile Services iOS quickstart, except that added items are stored locally in memory.

1. Download the GetStartedWithData [sample app][GitHub].

2. In Xcode, open the downloaded project and examine the TodoService.m file.

   	Notice that there are eight **// TODO** comments that specify the steps you must take to make this app work with your mobile service.

3. Press the **Run** button (or the Command+R key) to rebuild the project and start the app.

4. In the app, type some text in the text box, then click the **+** button.

   	![][0]  

   	Notice that the saved text is displayed in the list below.

##<a name="create-service"></a>Create a new mobile service in the Management Portal

[AZURE.INCLUDE [mobile-services-dotnet-backend-create-new-service](../includes/mobile-services-dotnet-backend-create-new-service.md)]

##<a name="download-the-service-locally"></a>Download the service to your local computer

[AZURE.INCLUDE [mobile-services-ios-download-service-locally](../includes/mobile-services-ios-download-service-locally.md)]

##<a name="test-the-service"></a>Test the mobile service

[AZURE.INCLUDE [mobile-services-dotnet-backend-test-local-service](../includes/mobile-services-dotnet-backend-test-local-service.md)]

##<a name="publish-mobile-service"></a>Publish the mobile service to Azure

[AZURE.INCLUDE [mobile-services-dotnet-backend-publish-service](../includes/mobile-services-dotnet-backend-publish-service.md)]

##<a name="update-app"></a>Update the app to use the mobile service for data access

[AZURE.INCLUDE [mobile-services-ios-enable-mobile-service-access](../includes/mobile-services-ios-enable-mobile-service-access.md)]

##<a name="test-app"></a>Test the app against your new mobile service

1. In Xcode, select an emulator to deploy to (either iPhone or iPad), press the **Run** button (or the Command+R key) to rebuild the project and start the app.

   	This executes your Azure Mobile Services client, built with the iOS SDK, that queries items from your mobile service.

2. As before, type text in the textbox, and then click the **+** button..

   	This sends a new item as an insert to the mobile service. Each new todoItem is stored and updated in the SQL database you previously configured for your mobile service in the Azure Management Portal.

3. Stop and restart the app to see that the changes were persisted to the database in Azure.

	You can also examine the database using the Azure Management portal or Visual Studio's SQL Server Object Explorer. The next two steps use the [Azure Management portal] to view the changes in your database.

4. In the Azure Management Portal, click manage for the database associated with your mobile service.

    ![][17]

5. In the Management portal execute a query to view the changes made by the app. Your query will be similar to the following query but use your database name instead of `todolist`.

        SELECT * FROM [todolist].[todoitems]

    ![][18]

This concludes the **Get started with data** tutorial.

##<a name="next-steps"></a>Next steps

This tutorial demonstrated the basics of enabling an iOS app to work with data in Mobile Services.

Next, consider completing one of the following tutorials that is based on the GetStartedWithData app that you created in this tutorial:

* [Validate and modify data with scripts]
  <br/>Learn more about using server scripts in Mobile Services to validate and change data sent from your app.

* [Refine queries with paging]
  <br/>Learn how to use paging in queries to control the amount of data handled in a single request.

Once you have completed the data series, try these other iOS tutorials:

* [Get started with authentication]
	<br/>Learn how to authenticate users of your app.

* [Get started with push notifications]
  <br/>Learn how to send a very basic push notification to your app with Mobile Services.

<!-- Anchors. -->
[Download the iOS app project]: #download-app
[Create the mobile service]: #create-service
[Add a data table for storage]: #add-table
[Update the app to use Mobile Services]: #update-app
[Test the app against Mobile Services]: #test-app
[Next Steps]:#next-steps
[Download the service locally]: #download-the-service-locally
[Test the mobile service]: #test-the-service
[Publish the mobile service to Azure]: #publish-mobile-service


<!-- Images. -->
[0]: ./media/mobile-services-dotnet-backend-ios-get-started-data/mobile-quickstart-startup-ios.png
[8]: ./media/mobile-services-dotnet-backend-ios-get-started-data/mobile-dashboard-tab.png
[9]: ./media/mobile-services-dotnet-backend-ios-get-started-data/mobile-todoitem-data-browse.png
[17]: ./media/mobile-services-dotnet-backend-ios-get-started-data/manage-sql-azure-database.png
[18]: ./media/mobile-services-dotnet-backend-ios-get-started-data/sql-azure-query.png


<!-- URLs. -->
[Validate and modify data with scripts]: /en-us/develop/mobile/tutorials/validate-modify-and-augment-data-dotnet
[Refine queries with paging]: /en-us/develop/mobile/tutorials/add-paging-to-data-ios
[Get started with Mobile Services]: /en-us/develop/mobile/tutorials/get-started-ios
[Get started with data]: /en-us/develop/mobile/tutorials/get-started-with-data-ios
[Get started with authentication]: /en-us/develop/mobile/tutorials/get-started-with-users-ios
[Get started with push notifications]: /en-us/develop/mobile/tutorials/get-started-with-push-ios
[JavaScript backend version]: /en-us/develop/mobile/tutorials/get-started-with-data-ios

[Azure Management Portal]: https://manage.windowsazure.com/
[Management Portal]: https://manage.windowsazure.com/
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Mobile Services iOS SDK]: https://go.microsoft.com/fwLink/p/?LinkID=266533
[GitHub]:  http://go.microsoft.com/fwlink/p/?LinkId=268622
[GitHub repo]: http://go.microsoft.com/fwlink/p/?LinkId=268784
