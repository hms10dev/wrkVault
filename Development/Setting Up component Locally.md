# Local Component Setup steps:

| clone git repository                       | (on terminal window) git clone git@bitbucket.org:manhattanassociates /component-carrier.git                                                              |
|--------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                            | cd component-carrier                                                                                                                                     |
|                                            |                                                                                                                                                          |
| Import gradle project in intellij          | https://www.jetbrains.com/idea/guide/tutorials/working-with-gradle/opening-a-gradle-project/                                                             |
|                                            |                                                                                                                                                          |
| Bring Up dependent components and Mysql DB | **(on terminal window) :**  chmod 777 ~/ipsetup.sh                                                                                                       |
|                                            | sudo ~/ipsetup.sh                                                                                                                                        |
|                                            | **configure docker hub using:**  docker login -u="manhrd+rdverde" -p=" 75V0R0GTYLDBPMT9TL82APK2WKL5CXZPKCA6GTD9B0J9P2GXOELZ U4NIB5GM5BVK" quay.io/manhrd |
|                                            | ./launch-deps.sh                                                                                                                                         |
|                                            |                                                                                                                                                          |
| Eureka                                     | confirm all dependent components are up and running by                                                                                                   |
|                                            | localdocker:[PORT NUMBER]                                                                                                                                |
|                                            |                                                                                                                                                          |
| Start the component                        | ./gradlew clean build                                                                                                                                    |
|                                            | export BUILD_NUMBER=`date` && ./gradlew asciidoctor && unset BUILD_NUMBER                                                                                |
|                                            | ./gradlew bootrun                                                                                                                                        |
|                                            |                                                                                                                                                          |
| Generate Auth Token                        | In seperate terminal window execute these for token generation:  chmod 777 ~/auth_token_generator_local.sh  ./auth_token_generator_local.sh              |
|                                            |                                                                                                                                                          |
| Connecting to Mysql DB                     |                                                                                                                                                          |
|                                            |                                                                                                                                                          |
|                                            |                                                                                                                                                          |
|                                            |                                                                                                                                                          |
|                                            |                                                                                                                                                          |
|                                            |                                                                                                                                                          |
|                                            |                                                                                                                                                          |
|                                            |                                                                                                                                                          |
|                                            |                                                                                                                                                          |
|                                            |                                                                                                                                                          |
|                                            |                                                                                                                                                          |
|                                            |                                                                                                                                                          |
|                                            |                                                                                                                                                          |
|                                            |                                                                                                                                                          |
