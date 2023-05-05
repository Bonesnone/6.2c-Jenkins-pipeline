This was created by Jye Floreani for the SIT223 6.2c github/jenkins pipeline integration and emailing project

### Requirements
Requires Docker and JMeter installed on both developer and Jenkins machines

### Setting up your own Jenkins server
Once you have a Jenkins build server running, install the following plugins:<br />
(Build tools) Maven<br />
(Unit and integration test) Performance plugin (to interface with JMeter)<br />
(Code analysis) Fortify<br />
(Security analysis) SNYK<br />
(Deployment) Docker<br />

With all of these installed, enable and restart. Copy this git repository SCM to replicate the Jenkinsfile, and ensure JMeter is located within the Jenkins working folder. By default, this directory is:<br />
`/usr/share/jenkins/` and `/usr/lib/jenkins/` on Linux<br />
`C:\Users\Jenkins\AppData\Local\Jenkins` on Windows<br />
Now you're ready to start development!

### Project Structure
Below is the current high-level structure of the project.

`public` – Public web documents including the index.html and other base html documents.<br />
`src` – Java(script) objects that need to be referenced internally.<br />
`src/resources` – Images, videos, audio, and other things used to build the page content.<br />
