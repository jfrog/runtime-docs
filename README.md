# JFrog Runtime Security

JFrog Runtime offers an in-depth analysis of Kubernetes cluster environments for security and DevOps specialists. It allows for continuous evaluation of the runtime environment states and real-time detection of risks during runtime execution; _critical+applicable CVEs, Malicious Packages,  integrity violations, and untrusted registry_.  The solution also systematically monitors the Kubernetes cluster, accurately identifying workloads and containers, matching them with their corresponding processes and files, and mapping them to their locations within JFrog's Artifactory system.

### Narrowing the threat funnel - JFrog Runtime Triage <a href="#h.rfhdez7v9kp8" id="h.rfhdez7v9kp8"></a>

The threat funnel is a process that helps security professionals manage the flood of security indicators and prioritize security events based on their potential impact. The goal of the threat funnel is to reduce the number of security events that require attention by filtering and prioritizing security events based on their relevance and severity. The objective is to reduce the volume of security events or the number of events that require manual intervention, enabling security teams to focus on the most critical security issues.

<figure><img src=".gitbook/assets/Diagram4.png" alt=""><figcaption></figcaption></figure>

The diagram above illustrates the threat funnel process. The process starts with all artifacts stored in Artifactory and becomes narrower as the artifacts pass through Xray, JFrog Advanced Security, and Runtime Security. The goal is to reduce the volume of security events or the number of events that require manual intervention, enabling security teams to focus on the most critical security issues. By combining information from multiple security solutions, such as Xray, JFrog Advanced Security, and JFrog Runtime, security teams can more effectively identify and address security vulnerabilities. The overall objective is to improve the organization's security posture by enabling security teams to quickly and accurately respond to security incidents and reduce the risk of security breaches.





