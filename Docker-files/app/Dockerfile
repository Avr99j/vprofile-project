# Multistage docker file


# Build Stage 1
# Build an image from the openjdk base image
FROM openjdk:11 AS BUILD_IMAGE

# Install maven
RUN apt update && apt install maven -y

RUN git clone https://github.com/devopshydclub/vprofile-project.git

# Run mvn install command to install the artifacts in the vprofile-project/targets folder
RUN cd vprofile-project && git checkout docker && mvn install

#*********************************************************************************************
# Build stage 2
# Build a docker image from the base tomcat image
FROM tomcat:9-jre11

LABEL "Project" = "Vprofile"
LABEL "Author" = "Avraaj"

# Delete the default artifacts present in the home folder of the tomcat base image to replace with our project artifacts
RUN rm -rf /usr/local/tomcat/webapps/*

# Copy the artifacts (.war file) generated from Build stage 1 to the tomcat home folder and name the artifact as ROOT.war
COPY --from=BUILD_IMAGE vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080

# Command to run the tomcat server
CMD ["catalina.sh", "run"]