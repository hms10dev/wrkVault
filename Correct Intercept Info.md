╰ rubikon intercept --cluster mtpfio01 --workload com-manh-cp-ai-forecast --gcloud default --http-match mascptnt02 --verbose debug

DEBU[0001] Path Complement: /ai-forecast                
DEBU[0001] Path for bootstrap.yml file: /Users/hsylla/Desktop/Desktop_April2024/components/component-ai-forecast/ai-forecast/src/main/resources/bootstrap.yml 
DEBU[0001] Path for .gradle file: /Users/hsylla/Desktop/Desktop_April2024/components/component-ai-forecast/ai-forecast/ai-forecast.gradle 
DEBU[0001] Struct - interceptConfig (before merge): 
GCloudConfiguration: default
ClusterName: mtpfio01WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW 
WorkloadName: com-manh-cp-ai-forecast
ComponentName: ai-forecast
Port: 17401
DebugPort: 17406
HttpMatch: x-telepresence-intercept-id=mascptnt02::.*
ComponentSrcCodePath: /Users/hsylla/Desktop/Desktop_April2024/components/component-ai-forecast 
DEBU[0001] ***************                              
DEBU[0001] Struct - interceptConfig (after merge): 
GCloudConfiguration: default
ClusterName: mtpfio01
WorkloadName: com-manh-cp-ai-forecast
ComponentName: ai-forecast
Port: 17401
DebugPort: 17406
HttpMatch: x-telepresence-intercept-id=mascptnt02::.*
ComponentSrcCodePath: /Users/hsylla/Desktop/Desktop_April2024/components/component-ai-forecast 
DEBU[0001] ***************                              
Validating and configuring gcloud and kubectl for GCloud Configuration: default and Cluster: mtpfio01
DEBU[0003] rubikon/pkg.connect2Tele Connecting - [telepresence connect] WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW 
DEBU[0003] Struct - interceptConfig (after merge): WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW 
GCloudConfiguration: defaultWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW 
ClusterName: mtpfio01
WorkloadName: com-manh-cp-ai-forecast
ComponentName: ai-forecast
Port: 17401

Using Deployment com-manh-cp-ai-forecastW 
   Intercept name         : com-manh-cp-ai-forecast
   State                  : ACTIVEWWWWWWW 
   Workload kind          : DeploymentWWW 
   Destination            : 127.0.0.1:17401
   Service Port Identifier: eighty-eighty 
   Volume Mount Error     : sshfs is not installed on your local machine
   Intercepting           : HTTP requests with headers
         'x-telepresence-intercept-id =~ mascptnt02::.*'


DEBU[0000] Path Complement: /ai-forecast                WW 
DEBU[0000] Path for bootstrap.yml file: /Users/hsylla/Desktop/Desktop_April2024/components/component-ai-forecast/ai-forecast/src/main/resources/bootstrap.yml 
DEBU[0000] Path for .gradle file: /Users/hsylla/Desktop/Desktop_April2024/components/component-ai-forecast/ai-forecast/ai-forecast.gradle 
DEBU[0000] Struct - interceptConfig (before merge): 
GCloudConfiguration: ""W 
ClusterName: mtpfio01WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WorkloadName: com-manh-cp-ai-forecast
ComponentName: ai-forecast
Port: 17401
DebugPort: 17406
HttpMatch: x-telepresence-intercept-id=mascptnt02::.*
ComponentSrcCodePath: /Users/hsylla/Desktop/Desktop_April2024/components/component-ai-forecast 
DEBU[0000] ***************                              
DEBU[0000] Struct - interceptConfig (after merge): 
GCloudConfiguration: default
ClusterName: mtpfio01
WorkloadName: com-manh-cp-ai-forecast
ComponentName: ai-forecast
Port: 17401
DebugPort: 17406
HttpMatch: x-telepresence-intercept-id=mascptnt02::.*
ComponentSrcCodePath: /Users/hsylla/Desktop/Desktop_April2024/components/component-ai-forecast 
DEBU[0000] ***************                              
Intercept file: '/Users/hsylla/rubikon/mtpfio01/com-manh-cp-ai-forecast/intercept.yml' loaded
