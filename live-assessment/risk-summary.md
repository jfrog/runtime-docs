# Risk Summary

Risks provide insights into the security health of your applications. JFrog's Runtime solution defines a set of risks that emphasize key security concerns, including

* **Malicious Packages**: Malicious packages are software components identified as containing harmful or malicious code, posing a threat to your system by executing unauthorized actions. JFrog's Runtime solution is designed to detect and flag these packages, effectively preventing potential security breaches.
* **Untrusted Images**: Untrusted images are sourced from registries that lack recognition or verification of trustworthiness. Utilizing such images can introduce security risks. JFrog's Runtime solution identifies and alerts users against the use of untrusted images in the Runtime environment, promoting the use of only reliable sources.
* **Critical Applicable CVEs**: Critical and Applicable CVEs (Common Vulnerabilities and Exposures) are vulnerabilities classified with critical severity and identified as applicable through JFrog Advanced Security's Contextual Analysis.
* **Integrity Violation**: An integrity violation occurs when the binaries of an image in the Artifactory image registry differ from the binaries of the same image running in the customer's Kubernetes cluster. This discrepancy suggests potential tampering or corruption, raising concerns about the image’s security. JFrog's runtime solution continuously monitors for such issues, ensuring the integrity of running images is maintained.

<figure><img src="../.gitbook/assets/Screenshot 2024-09-03 at 16.11.10.png" alt=""><figcaption></figcaption></figure>
