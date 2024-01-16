# ADR023: Paramaterise Common Terraform Roots

Date: 2024-01-15

## Status

> Accepted

## Context

Previously, forms-deploy's terraform had four separate but almost identical descriptions of an environment (one for each environment: dev, staging, prod, user-research).

Visually, the structure of our terraform looked like this:

```
infra/
├── deployments
│    ├── development        <-- Environment
│    │    └── forms-api     <-- Root
│    ├── production
│    │    └── forms-api
│    ├── staging
│    │    └── forms-api
│    └── user-research
│         └── forms-api
└── modules
     ├── forms-api/         <-- Module
     ├── ecs-service/
     └── ...
```

This has caused a number of problems, including:
* it is easy for one environment to differ from another through human error. We must add new modules to each environment separately, and then deploy them all by hand, and there is ample room for an operator to forget, or for misconfigurations to occur.
* it is difficult technically, and expensive in time, to create new environments, because of the number of configuration files which need to be duplicated.

## Decision

To address these problems, we proposed to **create and parameterise the common roots** - i.e. to create a single set of roots that describe a whole environment, which are parameterised for each environment.

We would achieve this by extracting the inputs to every existing root across all environments, normalising them, and structuring them as a new set of inputs that can be shared. We store these paramaterised inputs in the root folders, separated according to environment.  Following this, we take one representative set of roots from an environment, and promote that to being the set of roots for all environments. Finally, we would wrap some tooling around Terraform actions to ensure the correct sets of parameters are used for each environment.

We now have three separate deployments:
* **account:** this Terraform root deployment lays the groundwork for an AWS account.
* **deploy:** this contains the root modules for infrastructure that deploys the forms product. This is where the pipeline roots and the ECR roots live. 
* **forms:** this contains the Terraform root modules that combine to create a full deployment of the GOV.UK Forms product. This is where the forms-api/admin/runner/product-pages modules live, as well as the rds, redis, auth0 and ses modules.

Visually, the structure of our terraform now looks like this (note, the `infra/modules/` directory remains unchanged.):

```
infra/
├── deployments
│    ├── account
│    │   ├── ...
│    │   └── tfvars
│    │       ├── dev.tfvars <-- Specific config for an environment
│    │       ├── prod.tfvars
│    │       ├── staging.tfvars
│    │       └── user-research.tfvars
│    ├── deploy
│    │   ├── ...
│    │   └── tfvars
│    │       ├── dev.tfvars
│    │       ├── prod.tfvars
│    │       ├── staging.tfvars
│    │       └── user-research.tfvars
│    └── forms
│        ├── forms-api
│        ├── ...
│        └── tfvars
│            ├── dev.tfvars
│            ├── prod.tfvars
│            ├── staging.tfvars
│            └── user-research.tfvars
└── modules
     ├── forms-api	<-- Module
     ├── ecs-service
     └── ...
```

## Consequences

### Pros
* creating a new environment with this terraform structure will be quicker and easier, since there is less configuration that will need to be done
* we have removed repeated code, making the terraform easier to read
* this reduces the chance that environments will differ due to human error, since paramaterised inputs are stored together within the root

### Cons
* manually deploying terraform is now a bit more complicated. We have remedied this with the addition of a [makefile](https://github.com/alphagov/forms-deploy/blob/main/Makefile) which can now be used to run terraform locally