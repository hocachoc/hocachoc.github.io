# Questions

<div class="grid" markdown>
??? question "🌶️🌶️🌶️ How would you migrate an existing application to a containerized environment?"
    ??? success "Recall for longterm memory"
        To migrate an existing application to a containerized environment, I will need to do 2 parts:

        1. **Development on local**
            1. Figure out **any external dependency**, such as database, do I need to containerize it?
            2. Figure out **what parts of the application need to be containerized together**. For example, if I have frontend, backend. I will need to see which part I need to containerize, both frontend and backend, or seperated frontend with backend?
            3. **Create the Dockerfile** and define the entire architecture in that configuration, including the interservice dependencies.
            4. **Build** the actual **Docker image**.
            5. Make sure it **runs locally**.
        2. **Deploy to production**
            1. Configure the **orchestration tool** (such as Kubernestes) to **manage the containers**.
            2. If I have dev or staging environment, I could make a **test before moving to prod**.
            3. Once all testings have been passed, I am ready to deploy to production, however, make sure the **monitoring and alerting** on any problem shortly after the deployment **in case I need to roll back**.
??? question "🌶️🌶️🌶️ Describle your approach to implementing security in a DevOps pipeline (DevSecOps)"
    ??? success "Recall for longterm memory"
        To implement security in a DevOps pipeline (DevSecOps), I will integrate security practices throughout the development and deployment process, not only about securing the app once it's in production but also about securing the entire app creation process. There are 7 techniques:

        1. **Shift Left Security**: I perform SAST includes static code analysis, dependency scanning and secret detection during the build phase.
        2. **Automated Testing**: I perform DAST, vulnerability scans to identify potential security issues before they reach production.
        3. **Continuous Monitoring**: after the app reach production, I continue to monitor the pipeline and applications for security incidents using tools like Prometheus, Grafrana, ELK, Datalog and specialized security monitoring tools.
        4. **Infrastructure as Code - Security**: I perform security scans for IaC templates/configuration for any misconfigurations and vulnerabilities (like hardcorded passwords)
        5. **Access Control**: I implement RBAC or ABAC and enforcing the principle of least privilege across the pipeline.
        6. **Compliance Checks**: figure out the compliance requirements and regulations of client industry and integrate those checks to ensure the pipeline adheres to industry standards and regulatory requirements.
        7. **Incidient Response**: figure out a clear incident response plan and integrate security alerts into the pipeline to quickly address potential security breaches.
??? question "🌶️🌶️🌶️ What are the advantages and disadvantages of using Kubernetes Operators?"
    ??? success "Recall for longterm memory"
        1. **Advantages**:
            1. **Automation of Complex Tasks**: automate the management of complex stateful applications (like databases) reducing the need for manual intervention.
            2. **Consistency**: reduce human error and increase reliability by ensuring consistent deployments, scaling, and management of applications across environments.
            3. **Custom Resource Management**: allow I to manage custom resources in Kubernetes, extending its capabilities to support more complex applications and services.
            4. **Simplified Day-2 Operations**: streamline tasks like backup, upgrades, and failure recovery, making it easier to manage applications over time.
        2. **Disadvantages**:
            1. **Complexity**: developing and maintaining Operators can be complex and require in-depth knowledge of both Kubernetes and the specific application being managed.
            2. **Overhead**: running Operators adds additional components to your Kubernetes cluster, which can increase resource consumption and operational overhead.
            3. **Limited Use Cases**: not all applications benefit from the complexity of an Operator; for simple stateless applications, Operators might be overkill.
            4. **Maintenance**: Operators need to be regularly maintained and updated, especially as Kubernetes ifselt keeps evolving, which can add to the maintenance burden.
??? question "🌶️🌶️🌶️ How would you optimize a CI/CD pipeline for performance and reliability?"
    ??? success "Recall for longterm memory"
        It all depends highly on the tech stack and my specific context. However, three are some potential solutions:
        
        1. **Parallelize Jobs**: I try to run independent jobs in parallel to reduce overall build and test times. The result is faster feedback and speeds up the entire pipeline.
        2. **Optimizing Build Caching**: I use caching mechanisms to avoid redundant work (like re-downloading dependencies or rebuilding unchanged components). This can significantly reduce build times.
        3. **Incremental Builds**: I implement incremental builds that only rebuild parts of the codebase that have changed, rather than the entire project. It is useful for large projects with big codebases.
        4. **Efficient Testing**: prioritize and parallelize tests, running faster unit tests early and reserving more intensive integration or end-to-end tests for later stages. I use test impact analysis to only run test affected by recent code changes.
        5. **Monitor Pipeline Health**: continuosly monitor the pipeline for bottlenecks, failures, and performance issues. Use metrics and logs to identify and address inefficiencies.
        6. **Environment Consistency**: I use containerization and/or Infrastructure as Code (IaC) to maintain environment parity. My code works in all environments.
        7. **Pipeline Stages**: I use pipeline stages to catch issues early (for example, fail fast on linting or static code analysis before moving on to more resource-intensive stages)
</div>