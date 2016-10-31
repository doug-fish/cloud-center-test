# cloud-center-test
A service that logs a 2 part message. The idea is that one
part should come from the service and the other from the app
to demonstrate that service parameters are getting stored
in the app

Here’s a scenario that you can try out that I hope illustrates the problem I am having.

1. Create a new service
Admin->Services->Add Service

    - Choose External Service, 
    - Choose a logo,
    - Name: test-service,
    - Service ID:testservice

    - Under External Lifecycle Actions/Start choose URL and paste in
https://raw.githubusercontent.com/doug-fish/cloud-center-test/master/start.sh

    - Click "add a parameter",
    - Parameter Name: FROM_SERVICE,
    - Default Value: ServiceValue1

    - Click "add a parameter",
    - Parameter Name: FROM_APP,
    - Default Value: AppValue1,
    - Check "Should this parameter be visible to the user?" and "Should this parameter be editable by the user?"

    - Click Save

2. Create a new test application
    - Click Applications
    - Click Model
    - Click Custom Profiles
    - Click n tier execution app profile
    - Drag the test-service to the topology modeller (it's under frontend cache)
    - Click Basic information
    - Set name = test-app and version = 1
    - Click Save as app

3. Deploy the app and check result
    - Wait for it to succeed (should't take long)
    - Look in the log
    - The top item in the log should be something like

    START TaskRunning 10/31/16 14:10:00 ServiceValue1:AppValue1

4. Update the app and service values and check result.

You can see different values of AppValue1 by editing the parameter in the application and re-deploying, but you can't edit the value of ServiceValue1 to ServiceValue2 and see the updated value without removing the test service from the test-app and re-adding.
