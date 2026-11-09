# Week 14: Cloud architecture at client scale

**Month 4: The Enterprise and Consulting Track (Optional Stretch)** · You are deploying into someone else’s environment, not your own · 4 lessons · about 14 hours

[← Roadmap](../README.md#the-16-weeks) · [Week 13](week-13.md) · [Week 15 →](week-15.md)

> Weeks 13 to 16 are the optional enterprise track, for Palantir-scale FDE roles: messy client data, cloud at client scale, and the consulting side of the job.

## What you will be able to do

- Core cloud networking concepts: VPCs, private clusters, and how a client’s on-prem data center connects securely to a cloud environment
- Container orchestration basics: what a managed Kubernetes service actually handles for you versus what you still own
- Infrastructure as code with Terraform: if you cannot spin up a database, a compute cluster, and an access policy from a script, you are not ready to deploy into a client’s account
- Data exfiltration and security perimeters: why regulated clients (finance, government, healthcare) require strict controls on which services can move data where

## You ship this week

> A Terraform script that stands up a small but complete environment (a managed database, a compute service, and an access policy) from scratch in under five minutes.

Done means:

- [ ] It runs from a clean clone by following your README
- [ ] It has tests, and they pass
- [ ] No secrets in the repository; config comes from environment variables
- [ ] The README says what it does, how to run it, and one thing you would improve next

## Lessons

### 1. Cloud networking for client deployments - VPCs, private clusters and connecting the on-prem data centre

*About 3 hours*

In Weeks 1 to 12 you deployed into your own account, where everything had a public IP and the database was one connection string away. An enterprise client is the opposite. Their bank or hospital network was built over twenty years, the data you need sits in an on-premises data centre in Navi Mumbai or Chennai, and their security team will not allow your AI service, its database or its cluster to be reachable from the internet. Before you write a line of application code you will be asked: which VPC, which subnets, what CIDR range, how traffic reaches the data centre, and what is publicly exposed. If you cannot answer, the project waits weeks for a network review. This lesson gives you the vocabulary and the mental model to hold that conversation and to design a network that passes review.

Covers: The mental model: a VPC is a private network you define, and routes decide everything; Plan the addresses before anything else.

### 2. Managed Kubernetes - what EKS, GKE and AKS run for you, and what you still own

*About 3 hours*

Large clients increasingly standardise on Kubernetes: the platform team runs EKS, GKE or AKS clusters and expects every vendor, including you, to ship a container and a set of manifests rather than a VM with a script. The word "managed" misleads people. The provider runs the control plane, but your pods, their permissions, their network rules, their resource requests, the node versions on many setups and the add-ons are still yours. When an FDE's service is OOMKilled at 2 a.m., when a node upgrade evicts the only replica, or when a pod's service account can read every secret in the cluster, the client does not blame the cloud provider. This lesson draws the line precisely, so you can say what you own in a kickoff meeting and run your workload well on a cluster you did not build.

Covers: The mental model: Kubernetes is a reconciliation machine; What "managed" means, provider by provider; What you still own, in the manifests you ship.

### 3. Infrastructure as code with Terraform - state, plans, and a database, network and access policy from one script

*About 3.5 hours*

In a client's cloud account you are rarely allowed to click around the console, and even when you are, nobody can review, repeat or audit clicks. Enterprise platform teams expect infrastructure to arrive as code in a pull request: they read the plan, approve it, and the pipeline applies it. If you can stand up a database, a network and an access policy from a script, you can rebuild a broken environment in minutes, create an identical staging copy, hand everything over cleanly at the end of the engagement, and prove to an auditor exactly what exists and why. If you cannot, you are the vendor whose "temporary" resources nobody can explain six months later. Terraform is the most widely used tool for this, and OpenTofu, its open-source fork, uses the same language. This lesson teaches how it really works, especially state and plans, which is where people get hurt.

Covers: The mental model: declare the end state, let the tool compute the diff.

### 4. Data exfiltration and security perimeters for regulated clients, then the Week 14 Terraform deliverable

*About 4 hours*

A bank, a hospital chain or a government department does not mainly worry that your AI system will give a wrong answer. It worries that the system becomes a new way for data to leave: a leaked key used from an unknown laptop, a compromised dependency that copies customer records to someone else's bucket, a well-meaning engineer who exports a table to debug it, or an LLM call that quietly sends patient notes to an endpoint in another country. In India these worries are backed by rules, such as the RBI's requirement that payment system data be stored only in India and the phased obligations of the Digital Personal Data Protection Act and Rules. Clouds offer controls that restrict *which identities can move which data to where*: private endpoints, endpoint policies, organisation-wide data perimeters and service perimeters such as Google's VPC Service Controls. An FDE who understands these controls gets through security review; one who does not gets stuck there. This lesson explains them and then plans the Week 14 deliverable.

Covers: The mental model: identity controls who, perimeters control where.

## Free resources

Primary sources used in this week's lessons: official docs, papers and engineering blogs.

- [Amazon VPC: Subnets for your VPC (public, private and isolated subnets)](https://docs.aws.amazon.com/vpc/latest/userguide/configure-subnets.html)
- [Azure: What is ExpressRoute?](https://learn.microsoft.com/en-us/azure/expressroute/expressroute-introduction)
- [Google Cloud: Cloud Interconnect overview](https://docs.cloud.google.com/network-connectivity/docs/interconnect/concepts/overview)
- [Amazon EKS: Cluster API server endpoint access](https://docs.aws.amazon.com/eks/latest/userguide/cluster-endpoint.html)
- [Kubernetes: Cluster architecture (control plane and node components)](https://kubernetes.io/docs/concepts/architecture/)
- [GKE: Shared responsibility](https://docs.cloud.google.com/kubernetes-engine/docs/concepts/shared-responsibility)
- [GKE: Autopilot overview](https://docs.cloud.google.com/kubernetes-engine/docs/concepts/autopilot-overview)
- [Amazon EKS best practices: Security and the shared responsibility model](https://docs.aws.amazon.com/eks/latest/best-practices/security.html)
- [Amazon EKS: Automate cluster infrastructure with EKS Auto Mode](https://docs.aws.amazon.com/eks/latest/userguide/automode.html)
- [Terraform language documentation](https://developer.hashicorp.com/terraform/language)
- [Terraform: S3 backend, including use_lockfile and deprecated DynamoDB locking](https://developer.hashicorp.com/terraform/language/backend/s3)
- [Terraform tutorials: Get started on AWS](https://developer.hashicorp.com/terraform/tutorials/aws-get-started)
- [OpenTofu: State and plan encryption](https://opentofu.org/docs/language/state/encryption/)
- [Google Cloud: Overview of VPC Service Controls](https://docs.cloud.google.com/vpc-service-controls/docs/overview)
- [AWS IAM: Establish permissions guardrails using data perimeters](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_data-perimeters.html)
- [AWS PrivateLink: Control access to VPC endpoints using endpoint policies](https://docs.aws.amazon.com/vpc/latest/privatelink/vpc-endpoints-access.html)
- [Azure: What is Azure Private Link?](https://learn.microsoft.com/en-us/azure/private-link/private-link-overview)
- [RBI: FAQs on storage of payment system data](https://www.rbi.org.in/commonman/english/scripts/FAQs.aspx?Id=2995)

## Check yourself

Answer out loud before opening each answer.

<details><summary>What makes a subnet public or private?</summary>

Its route table. A public subnet has a route for internet-bound traffic to an internet gateway and resources with public IPs; a private subnet has no such route and reaches the internet, if at all, through a NAT gateway.

</details>

<details><summary>A packet is destined for `10.2.8.15`. The route table has `10.40.0.0/16 -&gt; local`, `10.0.0.0/14 -&gt; VPN` and `0.0.0.0/0 -&gt; NAT`. Where does it go and why?</summary>

To the VPN, because `10.0.0.0/14` is the most specific route that contains the address. `0.0.0.0/0` also matches but has a shorter prefix.

</details>

<details><summary>What does a managed Kubernetes service always run for you, and what does it never run for you?</summary>

It always runs the control plane: API servers, etcd, its backups and availability. It never owns your workloads: manifests, images, resource settings, RBAC, workload permissions and network policies are yours.

</details>

<details><summary>Your pod shows a rising restart count and `OOMKilled` as the last termination reason. What happened and what do you check?</summary>

The container exceeded its memory limit and the kernel killed it. Check actual memory use under realistic load, the limit and request values, and whether something such as a large batch or model copy grows memory unexpectedly.

</details>

<details><summary>What three things does Terraform compare when it makes a plan?</summary>

The configuration (what the code declares), the state (what Terraform recorded about the objects it manages) and the real infrastructure as reported by the provider's API. The plan is the set of actions needed to make reality match the configuration.

</details>

<details><summary>A plan line shows `-/+` next to your database. What does it mean and what do you do?</summary>

The database will be destroyed and recreated, usually because an argument that cannot be changed in place was modified, or the resource was renamed. Stop, find which argument forces replacement, and either revert it, use a `moved` block, or plan a proper migration.

</details>

<details><summary>An attacker steals a valid access key for the client's application role. Which perimeter stops them from using it on their own laptop, and how?</summary>

The network perimeter. Policies that require requests to come from the client's VPCs, specific VPC endpoints or corporate IP ranges deny the request because it originates from an unexpected network, even though the key is valid.

</details>

<details><summary>What does an AWS VPC endpoint policy add, and what is its default?</summary>

It filters which principals, actions and resources can be reached through that endpoint, in addition to IAM and resource policies. The default policy allows full access, so it must be replaced to be useful for exfiltration control.

</details>

---

**Learn Week 14 hands-on** with worked code, practice problems and an AI tutor that knows which step you are on: [Zero to FDE](https://zero-to-fde-90-days.site/forward-deployed-engineer-program?utm_source=github&utm_medium=referral&utm_campaign=roadmap_repo&utm_content=week14). Week 1 is free.
