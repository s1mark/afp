# Information the engineers get in real life
## Summary of the meeting with the customer
The customer would like to hire external IT experts who can provide a solution to successfully migrate the company's semi-scripted tasks into a more mature automated solution.
Currently there are a lot of human errors during their work because there are many manual steps in their existing processes. They would like to have a framework that helps them "automate everything".
They also do not want to use complicated tools because it would be hard for their team to onboard and understand it. They also want to be able to collaborate on a shared environment/framework. 
The customer wants it to be ready as soon as possible. They also highlighted to following points:
- The provided solution should be documented as detailed as possible. They want to be able to easily teach this framework to their colleagues
- Possibility to test their code
- Introduce approval workflow
- They would like to have some example terraform codes
- From a technical perspective they want to have an integrated system that manages code, issue tracking and automated processes.

## Manager's request
- Based on the meeting notes try to brake down the project into tasks
- Create a sketch, diagramm or roadmap about the project. You could maybe use miro.com or draw.io
- Create a technical architect diagramm about the solution
- Be ready by tomorrow ;)

# AFP class related information
The goal is to simulate a project work. That is why every team should utilize as much of the features that github offers as possible.
Please use projects, issues, milestones to track the progress. Sometimes would be nice to create a few releases (tags). Team members can collaborate more easily by using separate branches and pull requests.
## Create team workspace
- Every team should have their own github repository created and the team members added.
- Invite me as a collaborator to your repo: Settings / Collaborators / Add people (simark2357@gmail.com).
- Copy the [.gitignore](https://github.com/s1mark/mzl7y1/blob/31674b2071135266cc112cff2f66fa4915e8d871/.gitignore) file to the root of your repository and commit/push your changes to the main branch
- Create the root `main.tf` file
- Enable terraform pipeline in the repository:
  - In the 'Actions' tab search for the 'terraform' keyword and press configure
  - In the generated yaml the `if` statement in the `terraform apply` step needs to be changed from `if: github.ref == 'refs/heads/"main"' && github.event_name == 'push'` to `if: github.ref == 'refs/heads/main' && github.event_name == 'push'` otherwise the apply step will not execute in case of pushing to main branch.
  - You can also optionally delete the step that does the `fmt check`.
  - In case of any doubt you can use this [terraform.yml](https://github.com/s1mark/mzl7y1/blob/31674b2071135266cc112cff2f66fa4915e8d871/.github/workflows/terraform.yml) for reference
  - commit and push your changes to the `main` branch. At this point you should have the following struture
```
.
├── .github
│   └── workflows
│       └── terraform.yml
│── .gitignore
└── main.tf
```
This repository will be the team's workspace and everyone should work on the tasks in that space

## Work
Maybe you already found out that what the customer wants is basically can be covered with the github features
- issues
- milestones
- projects
- pipelines
- documentation
- pull requests and code reviews
- approval workflows
- releases (tags)
- release notes
- etc...
  
### Documentation
Atleast a well structured README.md file should be created in the root of the repo. It would be a nice touch to have pictures, diagramms in the documentation. Parts of the documentation could be:
- system design (for example how the github pipeline mechanism works --> uses a docker runtime that github hosts)
- pull request mechanism
- issues/projects
- terraform code
- test code
- pipeline workflow
- pull request approval workflow

### terraform code
Create three example terraform codes that simply creates files
- simply use the [local_file](https://registry.terraform.io/providers/hashicorp/local/latest/docs/resources/file#example-usage) resource
- use the `local_file` resource but now with [variables](https://www.terraformbyexample.com/variables/)
- create `n` number of files with the `local_file` resource with the help of the [count](https://developer.hashicorp.com/terraform/language/meta-arguments/count#basic-syntax) meta-argument

### test code
An extra step should be created in the pipeline named test or validation that would check if the files were created or not. For example a `bash` script could be used to check the existence of the files...
