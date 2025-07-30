# Cohesive setup of Branches, Environments, etc.

To help keep your repo secure, you can use environments and branches together to organize your environment

Branches are were your code is stored and organized

Environments are where the code is deployed

Branches are secured using Branch Protections and Rulesets

Environments are secured using Deployment Policies


**Short-Lived vs Long-Lived Branches**

Long-lived branches include: main, develop, release, staging, etc.

Short-lived branches include: feature/\*, bugfix/\*, hotfix/\*, etc.

**How it Works Together**

Environments --> Long-lived Branches  
Environments --> Deployment Policies  
Long-lived Branches --> Branch Protections  
Short-lived Branches --> Rulesets  


## Basics

Branch protections will vary by the branch or branch strategy employed by a repo.

A 'development' branch can have less restrictions that 'main' or 'release'.

It's recommended to follow common naming conventions for branch names.


Common branch names:

- feature/*
- bugfix/*
- hotfix/*
- release/*


This repo uses Github Action Workflows to setup: 

- environments 
- branches
- branch protections
- deployment policies

It uses the Github API to create everything.

**Github API Docs:**

- [Branch Protections](https://docs.github.com/en/rest/branches/branch-protection?apiVersion=2022-11-28#update-branch-protection)

- [Environments](https://docs.github.com/en/rest/deployments/environments?apiVersion=2022-11-28#create-or-update-an-environment)


**Environments:**

- development
- staging (optional)
- production


**Example Branch Protections:**

develop*

- require approval before merge  
- restrict deletions  
- restrict force pushes  


feature*

- develop branch protections  
- require approval from 1 reviewer

main

- require approval from 2 reviewers  
- require linear history  
- read-only



## Branch Protections

Branch Protections are used to define what can be done on a branch and by who

**Example branch protections:**

- Define a Branch Naming Pattern (main, feature/*, etc.)

- Require a Pull Request before Merging
- Require 1 Approval before Merging
- Dismiss Stale Pull Request Approvals when New Commits are Pushed
- Require Status Checks to Pass before Merging
- Require Conversation Resolution before Merging
- Require Signed Commits
- Require Linear History
- Require Deployments to Succeed before Merging     (select environments)
- Lock Branch                                       (branch is read-only)
- Do not allow Bypassing the Above Settings
- Allow Force Pushes                                (off by default)
- Allow Deletions                                   (off by default)



## Environments

Environments can have:

- Deployment Protection Rules
- Deployment Branches and Tags
- Environment Secrets and Variables


**Deployment Protection Rules:**

This is defined when creating an environment

Can specify:

- Required Reviewers - Specify people/teams that may approve workflow runs when they access this environment
- Can add up to 6 Reviewers
- Can prevent Self-Review
- Wait Timer - Set an amount of time to wait before allowing deployments to proceed


**Deployment Branches and Tags**

Limit which branches and tags can deploy to this environment based on rules or naming patterns.

Can specify:

- No restriction            (anyone can deploy to the environment)
- Protected Branches only   (all Protected Branches can deploy)
- Select Branches and Tags  (specify a naming pattern to allow)



## Rulesets

Can be created to enforce rules on branches that may not exist yet

Ideal for short-lived branches like feature, bugfix, etc.

Has basically the same options as branch protections

