# Jenkins + React CI Demo

This repository demonstrates how to set up a Jenkins CI pipeline for a basic React application. It covers installation, configuration, and testing a build process.

---

## 🚀 Project Setup

This app was created using Create React App:

```bash
npx create-react-app jenkins-demo-app
cd jenkins-demo-app
git init
git remote add origin https://github.com/<your-username>/jenkins-demo-app.git
git add .
git commit -m "Initial commit"
git push -u origin main

🛠️ Jenkins Setup Instructions
1. Create a New Job in Jenkins
Click New Item

Enter job name (e.g., react-build-demo)

Choose Freestyle project

Click OK

2. Configure the Job
✅ Source Code Management
Select Git

Repository URL: https://github.com/<your-username>/jenkins-demo-app.git

✅ Build Triggers
Choose one of:

⏱️ Poll SCM: H/5 * * * * (checks every 5 minutes)

🪝 GitHub Webhook: Enable “GitHub hook trigger for GITScm polling” and set up webhook at:

arduino
Copy
Edit
http://<your-jenkins-ip>:8080/github-webhook/
✅ Build Environment
After installing the NodeJS Plugin (Manage Jenkins → Manage Plugins):

Go to Manage Jenkins → Global Tool Configuration

Under NodeJS, add:

Name: node18

✅ Check “Install automatically”

Choose version: 18.x

In the job config, under Build Environment, enable:

✅ “Provide Node & npm bin/ folder to PATH”

Select node18

✅ Build Step
Add a shell step:

bash
Copy
Edit
npm install
npm run build
✅ Example: Intentionally Failing the Build
To test a failed build, you can:

🔧 Syntax Error (in src/App.js)
js
Copy
Edit
function Broken() {
  return <div>Missing tag
}
🔧 Invalid Import
js
Copy
Edit
import Missing from './not-there';
🔧 Force Exit
Add to shell script:

bash
Copy
Edit
exit 1
📦 Deployment Artifacts
After a successful build, the static files will be generated in build/.

Optional: add a post-build step to archive the build folder if needed.

🤖 Optional Improvements
Convert to Pipeline project using Jenkinsfile

Add ESLint or tests for stricter CI

Set up Slack or email notifications for failed builds

📎 Resources
Jenkins: https://www.jenkins.io/

Node.js: https://nodejs.org/

Create React App: https://create-react-app.dev/

NodeJS Plugin for Jenkins: https://plugins.jenkins.io/nodejs/
