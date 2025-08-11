🛠️ Jenkins Pipeline for .NET 7 SDK & Docker Engine Setup

This project contains a Jenkins declarative pipeline that automates the setup of

1) .NET 7 SDK

2) Docker Engine Community Edition (CE)

3) Docker daemon handling (manual start if not running)

4) User permission setup for Jenkins to access Docker

📜 Pipeline Overview

The pipeline executes the following stages:

1️⃣ Install .NET 7 SDK

Uses the official Microsoft script to install the latest .NET 7 SDK.

curl -sSL https://dot.net/v1/dotnet-install.sh | bash /dev/stdin --channel 7.0

2️⃣ Install Docker Engine CE

Installs Docker Engine Community Edition using Docker's recommended installation script.

curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh
docker --version

3️⃣ Start Docker Daemon (If Not Running)

Checks whether the Docker daemon is active. If not, it manually starts dockerd in the background.

dockerd & sleep 10

4️⃣ Add Jenkins User to Docker Group

Adds the Jenkins user to the docker group to allow Docker access without requiring sudo.

apt-get update
usermod -aG docker jenkins

⚠️ Note
systemctl commands are intentionally excluded to support environments where systemd is not used (e.g., Docker-in-Docker, some Jenkins agents).

This pipeline assumes that:

You have root or sudo access in your Jenkins environment.

The Jenkins agent is running on a Debian-based Linux system.

After adding Jenkins to the Docker group, you may need to restart the Jenkins agent for group changes to apply (not done within the pipeline).

This helped me to learn basics of Jenkins Pipeline and how to automate things using the devops principles.

Jenkins helps us to reduce the time of project upto 40%.

Modern tool used for automation.
🧪 Use Case
Ideal for CI/CD workflows that require:

Building and publishing .NET 7 applications

Running Docker containers as part of the build/test/deploy pipeline
