MyProjects
==========

My Projects


sudo rpm --import https://adoptopenjdk.jfrog.io/adoptopenjdk/api/gpg/key/public
sudo sh -c 'echo -n "deb https://adoptopenjdk.jfrog.io/adoptopenjdk/rpm/centos/7/x86_64/adoptopenjdk-17.repo " > /etc/yum.repos.d/adoptopenjdk-17.repo'




Yes, if the JAR file you are deploying is a Micronaut application, you will need to modify the shell script accordingly. Here are the changes you need to make:

Add the --features=graal option to the mn command to build the GraalVM native image. This option is required for Micronaut applications to work properly when compiled to native image.

Update the command to start the Java process with the new JAR file to use the Micronaut command to start the application instead. This is because a Micronaut application can be started either as a traditional JVM application or as a native image.

Here's the updated shell script:





#!/bin/bash

# Variables
ARTIFACTORY_URL="https://your.artifactory.url"
REPO_KEY="your-repo-key"
GROUP_ID="your-group-id"
ARTIFACT_ID="your-artifact-id"
VERSION="$1"
PACKAGING="jar"
JAR_NAME="$ARTIFACT_ID-$VERSION.$PACKAGING"
JAR_URL="$ARTIFACTORY_URL/artifactory/$REPO_KEY/$GROUP_ID/$ARTIFACT_ID/$VERSION/$JAR_NAME"

# Check if the version number is provided
if [ -z "$VERSION" ]; then
  echo "Usage: $0 [version]"
  exit 1
fi

# Download JAR file from Artifactory
echo "Downloading JAR file from Artifactory..."
curl -u your-username:your-password -O $JAR_URL

# Stop the running Java process (if any)
echo "Stopping the running Java process (if any)..."
sudo systemctl stop your-java-service

# Build native image with GraalVM
echo "Building native image with GraalVM..."
mn package --features=graal

# Replace the old JAR file with the new one
echo "Replacing the old JAR file with the new one..."
sudo mv build/$JAR_NAME /path/to/your/java/service/directory/


In this script, the mn package --features=graal command is used to build the GraalVM native image. This command assumes that you have the Micronaut CLI installed on your VMaaS server. If you don't have the Micronaut CLI installed, you can download the GraalVM distribution from the GraalVM website and use the native-image command to build the native image instead.

The command to start the Micronaut application with the new JAR file is now ./$JAR_NAME. This assumes that the JAR file is in the same directory as the shell script. If the JAR file is in a different directory, you will need to update the path accordingly.

Note that deploying a Micronaut application as a native image requires additional setup and configuration, such as configuring the classpath and native image properties. For more information, please refer to the Micronaut documentation.

# Start the Micronaut application with the new JAR file
echo "Starting the Micronaut application with the new JAR file..."
cd /path/to/your/java/service/directory/
./$JAR_NAME
`
