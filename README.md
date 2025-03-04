![image](https://github.com/user-attachments/assets/7f726d0b-5433-4564-a351-c778f96bf68e)


# k8sgptai
K8sGPT is an incredible tool that gives Kubernetes SREs superpowers.  It provides a simple and efficient way to scan your Kubernetes clusters and diagnose issues in plain English.  The tool is designed to have SRE experience codified into its analysers, which helps to pull out the most relevant information and enrich it with AI.

K8sGPT brings you ChatGPT for your K8s platform. It enables you to analyse issues in the cluster and report them back with suggestions to fix the issue.

Prerequisites  

Ensure k8sgpt is installed correctly on your environment by following the installation.

You need to be connected to any Kubernetes cluster(Minikube, Kind, GKE, EKS, AKS, DIY K8S Clusters).

Installing K8sgpt

Installing K8sgpt can be done in various ways, but one simple method is by running the brew command. You can refer to the official repository for the relevant commands specific to your platform.

brew tap k8sgpt-ai/k8sgpt

brew install k8sgpt

Quick Start

Are you ready to get started with k8sgpt and analyse your Kubernetes configurations? Follow these simple steps to quickly get up and running:

Generate an API key from OpenAI by running the command k8sgpt generate. This will open a link in your browser to generate the API key. Currently the default AI provider is OpenAI but in future you can change to Bard or any other AI.

Once you have generated the API key, run k8sgpt auth to set it in k8sgpt. You can also provide the API key directly using the --password flag.

If you want to manage the active filters used by the analyzer, run k8sgpt filters. By default, all filters are executed during analysis.

Run k8sgpt analyze to start the scan. This will analyze your Kubernetes configurations and provide a summary of any issues found.

To get a more detailed explanation of the issues, use the --explain flag with the k8sgpt analyze command.

That’s it! With these simple steps, you can quickly start using k8sgpt to analyze your Kubernetes configurations and ensure that your clusters are secure and well-optimized.

We can run the following and be able to view the file as a json so that we can understand more.

K8sgpt analyze -o json - explain - filter=Pod | jq .

K8sGPT comes equipped with analyzers to help you detect and troubleshoot issues in your Kubernetes cluster. These analyzers are included in the platform by default, and some of them are even enabled automatically. The built-in analyzers consist of podAnalyzer, pvcAnalyzer, rsAnalyzer, serviceAnalyzer, eventAnalyzer, and ingressAnalyzer. However, you also have the option of adding optional analyzers such as hpaAnalyzer and pdbAnalyzer. Plus, you can even create your own analyzers to suit your specific needs. With K8sGPT’s comprehensive set of analyzers, you can ensure that your cluster is always running smoothly and efficiently.

Usage:

  k8sgpt [command]
Available Commands:
  analyze     This command will find problems within your Kubernetes cluster
  auth        Authenticate with your chosen backend
  completion  Generate the autocompletion script for the specified shell
  filters     Manage filters for analyzing Kubernetes resources
  generate    Generate Key for your chosen backend (opens browser)
  help        Help about any command
  version     Print the version number of k8sgpt
Flags:
      --config string       config file (default is $HOME/.k8sgpt.git.yaml)
  -h, --help                help for k8sgpt
      --kubeconfig string   Path to a kubeconfig. Only required if out-of-cluster.
      --master string       The address of the Kubernetes API server. Overrides any value in kubeconfig. Only required if out-of-cluster.
  -t, --toggle              Help message for toggle

Use "k8sgpt [command] --help" for more information about a command.
In K8sGPT, filters are used to manage which resources to analyze. You can list the available filters by running the command k8sgpt filters list. The default filters are already enabled, but you can add or remove filters as needed. To add filters, run k8sgpt filters add followed by the filter(s) you want to add. You can add multiple filters by separating them with commas. To remove filters, run k8sgpt filters remove followed by the filter(s) you want to remove.

k8sgpt filters list
To add a single filter:

k8sgpt filters add Service
To add multiple filters:

k8sgpt filters add Ingress,Pod
To remove a single filter:

k8sgpt filters remove Service
To remove multiple filters:

k8sgpt filters remove Ingress,Pod
To run a scan with the default analyzers and get a detailed explanation of the issues:

k8sgpt generate
k8sgpt auth
k8sgpt analyze --explain
Built in analyzers
Enabled by default
podAnalyzer
pvcAnalyzer
rsAnalyzer
serviceAnalyzer
eventAnalyzer
ingressAnalyzer
statefulSetAnalyzer
deploymentAnalyzer
cronJobAnalyzer
nodeAnalyzer
Optional
hpaAnalyzer
pdbAnalyzer
networkPolicyAnalyzer
To filter the results by a specific resource, e.g. “Service”:

k8sgpt analyze --explain --filter=Service
To filter the results by a specific namespace, e.g. “default”:

k8sgpt analyze --explain --filter=Pod --namespace=default
To output the results in JSON format:

k8sgpt analyze --explain --filter=Service --output=json

Analysis Anonymised
Security is a top priority, so we’ve got your back with the anonymization feature. This nifty little trick masks sensitive data like Kubernetes object names and labels before sending it to the AI backend for analysis.

This means your data stays safe and sound, and nobody’s peeking where they shouldn’t be.

Here’s how to use anonymization with k8sgpt:

k8sgpt analyze --explain --anonymize
During the analysis, k8sgpt retrieves sensitive data which is then masked before being sent to the AI backend. The backend receives the masked data, processes it, and returns a solution to the user.

Once the solution is returned to the user, the masked data is replaced with the actual Kubernetes object names and labels.

Note: anonymization does not apply to events.

Integrations command

Did you know that you can integrate other tools with K8SGPT? With the k8sgpt integrations command, you can easily add and remove these helpful integrations.

First things first, let’s list all available integrations with following command.

k8sgpt integrations list

Next, let's activate an integration by running k8sgpt integration activate followed by the name of the integration you want. For example, trivy is a popular one that'll install Trivy's Helm chart on the cluster.

k8sgpt integration activate trivy
But wait, there’s more! You can even use these integrations in your analysis by specifying them with the — filter option. So if you’re using Trivy, just run the following command and watch the magic happen.

k8sgpt analyze --filter VulnerabilityReport
And, if you need to remove an integration, just run the following command followed by the name of the integration.

k8sgpt integration deactivate trivy
K8SGPT with GKE

Refer to this GitHub repository https://github.com/k8sgpt-ai/k8sgpt for more details on the features available and play around to see powers of the tool.
