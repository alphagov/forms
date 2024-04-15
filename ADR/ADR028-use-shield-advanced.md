# ADR028: Use AWS Shield Advanced

Date: 2024-04-15

## Status

Accepted 

## Context

The review of our Business Continuity and Disaster Recovery (BCDR) plans highlighted the need to mitigate against a malicious attack from outside our organisation. Such malicious attacks, for example a Distributed Denial of Service (DDoS) attack, would potentially degrade the service and impact end users unless measures were taken to prevent them.

The team investigated[AWS Shield Advanced](https://docs.aws.amazon.com/waf/latest/developerguide/shield-chapter.html) as a possible tool to address this issue since AWS Shield Standard was already enabled on GOV.UK Forms.

AWS Shield Advanced is a managed service that helps protect application against external threats, like DDoS attacks, volumetric bots, and vulnerability exploitation attempts.

## Decision

The team decided to use AWS Shield Advanced and implement it on the relevant infrastructure components.

## Consequences

We will enable AWS Shield Advanced on our ingress traffic-facing components (e.g., AWS CloudFront, load balancers, etc.). AWS Shield Advanced works in tandem with GOV.UK Form's existing Web Application Firewall (WAF) and web Access Control Lists (ACL) rules to better protect our services.

### Advantages

Implementing AWS Shield Advanced allows GOV.UK Forms to mitigate against potential malicious attacks from outside our organisation and therefore improve our BCP/DR abilities.

Moreover, GOV.UK Forms will benefit from the Shield Advanced automatic application layer mitigation as well as a dedicated Shield Response Team. This team will proactively contact GOV.UK Forms if the availability or performance of our applications are impacted by a possible attack.

### Disadvantages

There are two main disadvantages:

* Maintaining the new resources in our Terraform codebase
* Cost (although this is expected to be minimal)
