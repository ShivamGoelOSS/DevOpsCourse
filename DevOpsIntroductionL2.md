# DevOps Introduction
# Concept
- **Definition**: DevOps is a set of practices, cultural philosophies and tools that combine software development (Dev) and IT operations (Ops) to deliver applications and services fast and more reliably.
- **Key Ideas:**
	- Break Silos between development and operations team.
	- Automate repetitive tasks.
	- Ensure continuous delivery of high quality software.
- **Characteristics:** 
	- Collaboration between developers and operations.
	- Continuous integration, testing and deployment.
	- Focus on automation, monitoring and feedback loops.
- **Example:** 
	- **Without DevOps:** Developers finish code -> throw it to operations -> deployment fails -> long bug-fix cycles.
	- **With DevOps:** Developers push code -> automated CI/CD pipelines tests and deploys -> faster and more reliable releases.
# Why Do You Need DevOps?
Organizations need DevOps to:
- **Accelerate Delivery:** Reduce release cycle from months to days or hours. Example: deploying new features weekly instead of quarterly.
- **Improve Collaboration:** Developers and operations share responsibilities. Example: Both teams maintain infrastructure as code.
- **Increase Reliability:** Automated testing and monitoring reduces production errors. Example: CI pipelines catch bugs before deployment.
- **Automate Repetitive Tasks:** Builds, deployments, and environment setup are automated. Example: Using Jenkins or GitHub Actions to deploy code automatically.
- **Enhance Scalability and Flexibility:** Cloud native practices allow applications to scale dynamically. Example: Kubernetes manages containerized app scaling automatically.
- **Foster Continuous Improvement:** Monitoring feedback leads to better performance, security and user experience.
# Role of Operations Team in DevOps
- It is responsible for keeping applications running smoothly, securely and reliably after deployment. Their work ensures that the software built by developers performs well in real world environments.
- Their responsibilities include:
	- **Infrastructure Management:** Set up, configure and maintain servers (on-premises or cloud based). Use **Infrastructure as Code (IaC)** tools like Terraform or Ansible to automate provisioning. Manage networking, load balancing and storage systems.
	- **Deployment & Configuration:** Handle deployment of new releases to staging or production environments. Maintain version control of configurations using tools like Helm, Docker, or Kubernetes.
	- **Monitoring & Logging:** Continuously monitor system health, performance and uptime. Set up monitoring dashboards and alerts using tools like Prometheus, Grafana or Datadog. Use logging systems like ELK (Elasticsearch, Logstash, Kibana) to analyze logs and debug issues.
	- **Security & Compliance:** Implement system level security (firewalls, access control, encryption). Manage secrets, credentials, and permissions.
	- **Incident & Outage Management:** Respond to system outages and performance issues quickly. Create post-incident reports to improve system reliability.
	- **Performance Optimization:** Analyze performance metrics to find bottlenecks. Scale systems up/down based on demand (especially in cloud environments). Tune resource usage to reduce cost and improve speed.
	- **Collaboration with Developers:** Work closely with developers to understand application needs. Share feedback from production to improve development practices. Help automate deployment, testing and rollback processes.
- Hence, they focus on stability, scalability, security and performance of the deployed applications while also collaborating with developers to make deployment and monitoring as automated and seamless as possible.
# DevOps Lifecycle
- **SDLC (Software/System Development Lifecycle):** Requirement Analysis -> Design -> Implementation -> Testing -> Evolution
- **DevOps Lifecycle:** 
	- DevOps is not linear - it is a continuous and iterative process. Feedback from monitoring loops back into planning and coding. It represents the continuous process from development to production. The main stages are: 
		- **Plan:** Requirement Gathering, Task Planning. **Tools:** Jira, Trello, Confluence
		- **Code:** Writing application code, unit test etc. **Tools:** Git, GitHub, GitLab
		- **Build:** Compile code and create deployable artifacts. **Tools:** Maven, Gradle, npm, Dockerfile
		- **Test:** Automated testing for quality assurance. **Tools:** Selenium, JUnit, pytest
		- **Release:** Package and release code. **Tools:** Jenkins, GitLab CI/CD, CircleCI
		- **Deploy:** Deploy to staging/production. **Tools:** Kubernetes, Docker, Ansible, Helm, Kustomize
		- **Operate:** Manage infrastructure and monitor apps. **Tools:** AWS CloudWatch, Prometheus, ELK
		- **Monitor:** Track performance and collect feedback. **Tools:** Grafana, Nagios, Datadog.
# DevOps Principles
DevOps is guided by several principles.
- **Culture of Collaboration:** Dev and Ops work together throughout the lifecycle.
- **Automation:** Automate builds, tests, deployments and infrastructure provisioning.
- **Continuous Integration and Continuous Delivery (CI/CD):** Integrate code frequently and deploy continuously.
- **Measurement:** Track performance metrics, deployment frequency, error rates, and system health.
- **Sharing Knowledge:** Encourage team learning and transparency.
- **Infrastructure as Code (IaC):** Manage infrastructure declaratively using code (Terraform, Ansible).
- **Monitoring and Feedback:** Continuous feedback helps improve processes and application reliability.
# DevOps Practices
DevOps is implemented using a set of best practices:
- **Continuous Integration (CI):** Merge code frequently; automated builds and tests for early bug detection.
- **Continuous Delivery (CD):** Automate release process to staging for faster releases.
- **Continuous Deployment (CD):** Automate deployment to production for immediate user access.
- **Version Control:** Track changes in code and config for easy rollback, and collaboration.
- **Automated Testing:** Unit, Integration, and UI testing for higher software quality.
- **Infrastructure as Code (IaC):** **Manage servers and configs as code.** Benefits: Repeatable, auditable environments.
- **Configuration Management:** Standardize environment setup to reduce manual errors.
- **Monitoring & Logging:** Track application & infrastructure health to detect and fix issues quickly.
- **Collaboration & Communication:** Shared responsibilities, chatOps for improved team efficiency.
# Tools in DevOps
DevOps relies on a **toolchain** across different lifecycle stages:
- **Version Control:** Git, GitHub, BitBucket, GitLab for tracking source code.
- **CI/CD:** Jenkins, GitLab CI, CircleCI, GitHub Actions to automate build, test and deploy.
- **Configuration Management:** Ansible, Chef, Puppet to automate server setup.
- **Containerization:** Docker to package apps into portable containers.
- **Orchestration:** Kubernetes, OpenShift to **deploy and manage containers at scale.**
- **Infrastructure as Code (IaC):** Terraform, CloudFormation to provision and manage cloud resources.
- **Monitoring & Logging:** Prometheus, Grafana, ELK Stack, Datadog to observe system health.
- **Collaboration & ChatOps:** Slack, Microsoft Teams, Mattermost for team communication, alerting. 
- **Security:** SonarQube, Trivy, Snyk to **integrate security in DevOps pipelines.**
# Developer & Operations Flow in DevOps
- In a DevOps environment, developers are expected to commit code regularly. Each commit is automatically tested and built through CI/CD pipelines maintained by the operations team. After successful verification, the operations team ensures deployment, scaling, and monitoring of the application.
- **Regular Code Commits:**
	- Code changes are committed frequently in small, logical units.
	- Each commit is pushed to a version control system such as Git.
	- Automated pipelines are triggered upon commit or merge events.
	- Frequent commits ensure quick feedback, easier debugging, and safer rollbacks.
- **Pipeline Execution:**
	- Once a commit is pushed, the Continuous Integration (CI) pipeline is triggered.
	- The pipeline automatically performs linting, building, and unit testing.
	- **On merging into the main branch**, a Continuous Delivery (CD) pipeline is executed to build deployable artifacts.
	- The same artifact is later promoted through environments like staging and production.
- **Deployment Workflow:**
	- Code is committed to the repository.
	- The CI pipeline is executed and all tests are run.
	- If successful, an artifact or Docker image is built and stored.
	- The CD pipeline deploys the artifact to a staging environment.
	- Automated smoke tests and validation scripts are executed.
	- Upon approval, deployment to production is triggered.
	- The system is monitored for performance, errors, and stability.
	- In case of failure, rollback or hotfix deployment is performed.
- **Scaling and Monitoring:**
	- Applications are scaled automatically based on metrics such as CPU usage or request rate.
	- Load balancers distribute traffic efficiently across instances.
	- Monitoring dashboards are created for visibility into system health.
	- Alerts are configured to notify the operations team about performance issues or outages.
- **In a DevOps lifecycle:**
	- Code is committed frequently.
	- Pipelines are triggered automatically.
	- Applications are built, tested, deployed, and monitored continuously.
	- The operations team ensures systems are scaled, secured, and maintained efficiently.
	- Collaboration between development and operations is promoted to achieve faster, more reliable releases.

![[Pasted image 20251030184907.png]]
# Conclusion 
- DevOps bridges development and operations for faster, reliable software delivery. 
- **Why DevOps:** Faster delivery, collaboration, automation, monitoring, continuous improvement.
- **Lifecycle:** Plan → Code → Build → Test → Release → Deploy → Operate → Monitor (iterative).
- **Principles:** Collaboration, automation, CI/CD, measurement, sharing, IaC, monitoring. 
- **Practices**: CI/CD, automated testing, IaC, monitoring, configuration management. 
- **Tools:** Git, Jenkins, Docker, Kubernetes, Terraform, Prometheus, Grafana, Ansible. DevOps is a mindset, methodology, and tool ecosystem — mastering it improves software quality, delivery speed, and team collaboration.
