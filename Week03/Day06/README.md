# Questions and Answers Omar Elbanna

## What is the packages is a prerequisite for installing Jenkins ?
- Java Package JDK
---------------------------------------------------------------------------------------
## Run this command and tell me the ssh port: curl -Lv http://localhost:8085/login 2>&1 | grep -i 'x-ssh-endpoint'
- noting happened 
---------------------------------------------------------------------------------------
## What are jenkins plugins?

	A. Plugins are used to configure the security settings in Jenkins.
	B. Plugins are the primary means of enhancing the functionality of a Jenkins environment to suit organization or user specific needs.
	C. Plugins are used to create jobs in Jenkins.
	D. Plugins are the tools to setup CI/CD pipelines in Jenkins.

- B. Plugins are the primary means of enhancing the functionality of a Jenkins environment to suit organization or user specific needs.
---------------------------------------------------------------------------------------
## Can we install the .hpi plugin file from Jenkins web UI?
- Yes
---------------------------------------------------------------------------------------
## Make sure that Git and Github plugins are installed if it's not kindly install them
```markdown
>"Git client plugin
>Version5.0.0
>Utility plugin for Git support in Jenkins
>Report an issue with this plugin
>Git plugin
>Version5.4.1
>This plugin integrates Git with Jenkins.
>Report an issue with this plugin
>GitHub API Plugin
>Version1.321-468.v6a_9f5f2d5a_7e
>This plugin provides GitHub API for other plugins.
>Report an issue with this plugin
>GitHub Branch Source Plugin
>Version1797.v86fdb_4d57d43
>Multibranch projects and organization folders from GitHub. Maintained by CloudBees, Inc.
>Report an issue with this plugin
>GitHub plugin
>Version1.40.0
>This plugin integrates GitHub to Jenkins.
>Report an issue with this plugin
>Pipeline: GitHub Groovy Libraries
>Version61.v629f2cc41d83
>Allows Pipeline Groovy libraries to be loaded on the fly from GitHub.
>Report an issue with this plugin"
```
- Yes, all the plugins are installed
---------------------------------------------------------------------------------------
## Install Jenkins as normal service or as docker container (bouns install it using ansible)
```markdown
> omarelbanna@Omars-MacBook-Air Day06 % brew install jenkins-lts       
> omarelbanna@Omars-MacBook-Air Day06 % brew services start jenkins-lts
> localhost:9090 # note that i have changed the port 
```
---------------------------------------------------------------------------------------
# Under what location Jenkins store its data primarily?
- /var/lib/jenkins
---------------------------------------------------------------------------------------
# Install and configure thinbackup plugin and make sure that the default dir for backup is: /var/lib/jenkins/jenkins_backup
- ThinBackup
- Settings are now integrated in global configuration.
---------------------------------------------------------------------------------------
# Create a Jenkins user as per the details provided below.

	A. Username: jenkins
	B. Password: jenk!n$
	C. Full Name: Orange DevOps
```
User ID         Name
   ↓              ↓
jenkins 	Orange DevOps
```
---------------------------------------------------------------------------------------
# Install the Role-based Authorization Strategy plugin and enable the Role-Based Strategy authorization in Jenkins security settings.
---------------------------------------------------------------------------------------
# Create a role named developers and make sure it has overall Read permissions alone. Also assign role called developers to the user called jenkins.
---------------------------------------------------------------------------------------
# First, install the Matrix Authorization Strategy plugin and using the Project-based Matrix Authorization Strategy assign some permissions that would allow jenkins to build the mytest job.
# Install Pipeline Jenkins plugin?
# Create a pipeline job named hello-world, it should just echo the Hello World string.

	Once this is done, build this job through user jenkins.
	Note: You should use jenkins's credentials from the previous question.
	
		Username: jenkins
		Password: jenk!n$
```
Started by user Orange DevOps
[Pipeline] Start of Pipeline
[Pipeline] node
Running on Jenkins in /Users/omarelbanna/.jenkins/workspace/mytest
[Pipeline] {
[Pipeline] stage
[Pipeline] { (Hello)
[Pipeline] echo
Hello World
[Pipeline] }
[Pipeline] // stage
[Pipeline] }
[Pipeline] // node
[Pipeline] End of Pipeline
Finished: SUCCESS
```
---------------------------------------------------------------------------------------
# Install SSH Build Agents Jenkins plugin.
# Create a simple Jenkins job that prints "Hello, World!" in the console output.
#	Set up a basic Freestyle job with a shell command to print a message.
```
Started by user Omar Hussein Mohamed Amen
Running as SYSTEM
Building in workspace /Users/omarelbanna/.jenkins/workspace/HelloWorldJob
[HelloWorldJob] $ /bin/sh -xe /var/folders/7g/pmh5cj016vz2gr_ysg6pdtt40000gn/T/jenkins8461859380047222010.sh
+ echo 'Hello, World!'
Hello, World!
Finished: SUCCESS
```
---------------------------------------------------------------------------------------
# Configure a Jenkins job to pull code from a public GitHub repository.
#	Use the Git plugin to connect to the repository and check out the latest code.
```
Started by user Omar Hussein Mohamed Amen
Running as SYSTEM
Building in workspace /Users/omarelbanna/.jenkins/workspace/GitHubCodePull
The recommended git tool is: NONE
No credentials specified
 > git rev-parse --resolve-git-dir /Users/omarelbanna/.jenkins/workspace/GitHubCodePull/.git # timeout=10
Fetching changes from the remote Git repository
 > git config remote.origin.url https://github.com/zscbana/EduTrack # timeout=10
Fetching upstream changes from https://github.com/zscbana/EduTrack
 > git --version # timeout=10
 > git --version # 'git version 2.39.3 (Apple Git-146)'
 > git fetch --tags --force --progress -- https://github.com/zscbana/EduTrack +refs/heads/*:refs/remotes/origin/* # timeout=10
 > git rev-parse refs/remotes/origin/main^{commit} # timeout=10
Checking out Revision b57b0fc5abd7e47f9b8275f92b6f14c38290929c (refs/remotes/origin/main)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f b57b0fc5abd7e47f9b8275f92b6f14c38290929c # timeout=10
Commit message: "ci: add Azure Static Web Apps workflow file on-behalf-of: @Azure opensource@microsoft.com"
First time build. Skipping changelog.
[GitHubCodePull] $ /bin/sh -xe /var/folders/7g/pmh5cj016vz2gr_ysg6pdtt40000gn/T/jenkins7631460546571838225.sh
+ ls -l
total 40
-rw-r--r--  1 omarelbanna  staff   259 Sep 18 16:45 AUTHORS
drwxr-xr-x  3 omarelbanna  staff    96 Sep 18 16:45 Contact
-rw-r--r--  1 omarelbanna  staff  1454 Sep 18 16:45 README.md
drwxr-xr-x  3 omarelbanna  staff    96 Sep 18 16:45 Roadmaps
-rw-r--r--  1 omarelbanna  staff  2420 Sep 18 16:45 Styels.css
drwxr-xr-x  3 omarelbanna  staff    96 Sep 18 16:45 Tracks
drwxr-xr-x  3 omarelbanna  staff    96 Sep 18 16:45 images
-rw-r--r--  1 omarelbanna  staff  3636 Sep 18 16:45 index.html
-rw-r--r--  1 omarelbanna  staff   791 Sep 18 16:45 main.js
Finished: SUCCESS
```
---------------------------------------------------------------------------------------
# Set up a Jenkins job that triggers every 5 minutes using the "Build periodically" option.
	Use the cron syntax to configure the trigger.
```
Build periodically
Schedule
*/5 * * * *
```
---------------------------------------------------------------------------------------
# Install a Jenkins plugin from the Plugin Manager.
	Pick any plugin (Docker) and verify that it's successfully installed.
- done
---------------------------------------------------------------------------------------
# Configure a Jenkins job to send email notifications when a build fails.
#	Set up the Email Extension Plugin and define an email recipient list.
- done
---------------------------------------------------------------------------------------
# Create a Jenkins pipeline with two stages:
#	Stage 1: Pull code from GitHub(repo from your choise)
#	Stage 2: Run a simple shell script that lists all files in the workspace.
```
Started by user Omar Hussein Mohamed Amen
Running as SYSTEM
Building in workspace /Users/omarelbanna/.jenkins/workspace/GitHubCodePull
The recommended git tool is: NONE
No credentials specified
 > git rev-parse --resolve-git-dir /Users/omarelbanna/.jenkins/workspace/GitHubCodePull/.git # timeout=10
Fetching changes from the remote Git repository
 > git config remote.origin.url https://github.com/zscbana/EduTrack # timeout=10
Fetching upstream changes from https://github.com/zscbana/EduTrack
 > git --version # timeout=10
 > git --version # 'git version 2.39.3 (Apple Git-146)'
 > git fetch --tags --force --progress -- https://github.com/zscbana/EduTrack +refs/heads/*:refs/remotes/origin/* # timeout=10
 > git rev-parse refs/remotes/origin/main^{commit} # timeout=10
Checking out Revision b57b0fc5abd7e47f9b8275f92b6f14c38290929c (refs/remotes/origin/main)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f b57b0fc5abd7e47f9b8275f92b6f14c38290929c # timeout=10
Commit message: "ci: add Azure Static Web Apps workflow file on-behalf-of: @Azure opensource@microsoft.com"
First time build. Skipping changelog.
[GitHubCodePull] $ /bin/sh -xe /var/folders/7g/pmh5cj016vz2gr_ysg6pdtt40000gn/T/jenkins7631460546571838225.sh
+ ls -l
total 40
-rw-r--r--  1 omarelbanna  staff   259 Sep 18 16:45 AUTHORS
drwxr-xr-x  3 omarelbanna  staff    96 Sep 18 16:45 Contact
-rw-r--r--  1 omarelbanna  staff  1454 Sep 18 16:45 README.md
drwxr-xr-x  3 omarelbanna  staff    96 Sep 18 16:45 Roadmaps
-rw-r--r--  1 omarelbanna  staff  2420 Sep 18 16:45 Styels.css
drwxr-xr-x  3 omarelbanna  staff    96 Sep 18 16:45 Tracks
drwxr-xr-x  3 omarelbanna  staff    96 Sep 18 16:45 images
-rw-r--r--  1 omarelbanna  staff  3636 Sep 18 16:45 index.html
-rw-r--r--  1 omarelbanna  staff   791 Sep 18 16:45 main.js
Finished: SUCCESS
```
---------------------------------------------------------------------------------------
# Set up a Jenkins job to archive log files generated by the build.
#	Use the "Archive the artifacts" post-build action to store the logs.

- Set up a Jenkins job to clean up old builds (e.g., only keep the last 5 builds).
	Configure the job to discard old builds using the "Discard Old Builds" option.

- Create a Jenkins job that takes user input for a name and prints a greeting message in the console output (e.g., "Hello, [Name]!" ).
	Use the "This build is parameterized" option and add a string parameter.

- Set up a Jenkins job to build a Java project using the javac command.
	Ensure the job compiles a basic Java file and outputs the result.

- Create a Jenkins job that runs a script to check for disk space usage on the Jenkins server.
	Use a simple shell script in the build step to check the disk space (df -h on Linux).

- Create a Jenkins job that executes a Python script from the repository search for a repo or create one.
	Ensure the job pulls the script from GitHub and runs it.

- Configure a Jenkins job that runs on an agent (slave) node with specific labels ("linux").
	Set up a node with a label and configure the job to run only on that node.