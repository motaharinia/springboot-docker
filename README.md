## Spring Boot with Docker

### Docker
Developing apps today requires so much more than writing code. Multiple languages, frameworks, architectures, and discontinuous interfaces between tools for each lifecycle stage creates enormous complexity. Docker simplifies and accelerates your workflow, while giving developers the freedom to innovate with their choice of tools, application stacks, and deployment environments for each project.

### Docker Images:
https://hub.docker.com/search?q=&type=image

further references:     
- https://spring.io/guides/gs/spring-boot-docker/ 
- https://www.docker.com/why-docker
- https://www.youtube.com/watch?v=FlSup_eelYE
- https://virgool.io/Software/%D8%A2%D9%85%D9%88%D8%B2%D8%B4-%D9%86%D8%B5%D8%A8-%D8%AF%D8%A7%DA%A9%D8%B1-%D8%A8%D8%B1-%D8%B1%D9%88%DB%8C-%D9%88%DB%8C%D9%86%D8%AF%D9%88%D8%B2-%D8%A8%D8%AF%D9%88%D9%86-%D8%AF%D8%B1%D8%AF%D8%B3%D8%B1-bpfdxbknabpc
- https://dockerme.ir/
- http://docker.ir/


### Project Descriptions :
please see application.properties files in resources folder and select a active profile "dev" or "com" to run project. you can check test methods too.  
docker configuration steps:
1. install docker desktop for windows from "https://hub.docker.com/editions/community/docker-ce-desktop-windows"
    - login with docker id and password
    - click on docker tray icon and uncheck the "setting/general/start docker desktop when you log in" (because of vpn should be run before)
    - click on docker tray icon and uncheck the "setting/general/automatically check for update" (because of vpn should be run before)
    - click on docker tray icon and check the "setting/general/expose daemon on tcp://localhost:2375 without tls" and restart docker (to use in intellij docker window)
    - click on docker tray icon and goto "setting/resources/advanced/disc image location" you can change image location
2. current project is created as below:
    - Java: 13
    - Artifact: dockertest
    - Packaging: jar
    - Dependencies: "Spring web"
    - in application.properties added: 
        - ```server.port=8080```
    - in pom.xml inside <build> tag added below tag: 
        - ```<finalName>dockertest</finalName>```
3. added "Dockerfile" file beside "pom.xml" with these lines:   
    ```FROM openjdk:13```   
    ```ADD target/dockertest.jar dockertest.jar```  
    ```EXPOSE 8080```   
    ```ENTRYPOINT ["java", "-jar", "dockertest.jar"]``` 

4. in IntelliJ IDEA , select lifecycle/clean and lifecycle/install and run in maven box to create jar file in target:

5. in IntelliJ IDEA terminal in project folder 
    - check current terminal path:  
    ```cd```

    - check docker version:     
    ```docker -v```

    - build docker image file from "Dockerfile" properties in project beside pom.xml with tag "dockertest" (it will download openjdk image file for the first time):    
    ```docker build -f Dockerfile -t dockertest .```

    - check docker images after build:      
    ```docker images```

    - push and run docker image for test spring application with same port 8080 in spring(we can change docker port as we wish):    
    ```docker run -p 8080:8080 dockertest```

    - check terminal commands history:  
    ```history```

    - clear terminal:   
    ```cls```

7. test spring boot application on windows Browser:
    ```http://localhost:8080```

8. in IntelliJ IDEA in the Settings/Preferences dialog Ctrl+Alt+S, select Build, Execution, Deployment | Docker.
Click The Add button to add a Docker configuration and specify how to connect to the Docker daemon.
    - Name: MyDocker
    - Connect to Docker daemon with: select TCP socket on "tcp://localhost:2375"  (Path Mapping: For Windows and macOS: Specify the mappings for folders that can be shared between the host and the container volumes)

9. be carefull of huge log file in c:\users\MyUser\.intellijidea2019.3\system\log\docker.log after apply this setting for IntelliJ IDEA

10. in IntelliJ IDEA "view menu/tool window/services" we can see docker and connect to it

11. stop container by id: "docker exec <containerId> stop". copy docker image from "docker images" command. for example:    
    ```docker exec db79a8e5fdae stop```

### IntellliJ IDEA Configurations :
- IntelijIDEA: Help -> Edit Custom Vm Options -> add these two line:
    - -Dfile.encoding=UTF-8
    - -Dconsole.encoding=UTF-8
- IntelijIDEA: File -> Settings -> Editor -> File Encodings-> Project Encoding: form "System default" to UTF-8. May be it affected somehow.
- IntelijIDEA: File -> Settings -> Editor -> General -> Code Completion -> check "show the documentation popup in 500 ms"
- IntelijIDEA: File -> Settings -> Editor -> General -> Auto Import -> check "Optimize imports on the fly (for current project)"
- IntelijIDEA: File -> Settings -> Editor -> Color Scheme -> Color Scheme Font -> Scheme: Default -> uncheck "Show only monospaced fonts" and set font to "Tahoma"
- IntelijIDEA: Run -> Edit Configuration -> Spring Boot -> XXXApplication -> Environment -> VM Options: -Dspring.profiles.active=dev

<hr/>
<a href="mailto:eng.motahari@gmail.com?"><img src="https://img.shields.io/badge/gmail-%23DD0031.svg?&style=for-the-badge&logo=gmail&logoColor=white"/></a>



