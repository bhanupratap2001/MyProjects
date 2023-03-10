MyProjects
==========

My Projects


sudo rpm --import https://adoptopenjdk.jfrog.io/adoptopenjdk/api/gpg/key/public
sudo sh -c 'echo -n "deb https://adoptopenjdk.jfrog.io/adoptopenjdk/rpm/centos/7/x86_64/adoptopenjdk-17.repo " > /etc/yum.repos.d/adoptopenjdk-17.repo'





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

# Start the Micronaut application with the new JAR file
echo "Starting the Micronaut application with the new JAR file..."
cd /path/to/your/java/service/directory/
./$JAR_NAME
`
