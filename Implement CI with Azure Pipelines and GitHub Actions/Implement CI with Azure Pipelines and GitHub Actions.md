# Implement CI with Azure Pipelines and GitHub Actions

URL: https://github.com/adilshehzad786/ContosoAir

# ****Setting up the environment****

1. Fork this repository → ‣

![Untitled](file://C:\Users\ashehzad\Downloads\Export-b48107c3-0936-4d74-be86-55ae681868f9\Implement%20CI%20with%20Azure%20Pipelines%20and%20GitHub%20Actio%2099b9acc747964c2d8178e4ed3c9b2cf3\Untitled.png)

1. Clone the repository to your local machine

## ****Lab Scenario:****

In this lab, we’ll be illustrating the integration and automation benefits of **Azure DevOps**. We will take on the role of helping a fictitious airline—Contoso Air—that has developed its flagship web site using Node.js. To improve their operations, they want to implement pipelines for continuous integration and continuous delivery so that they can quickly update their public services and take advantage of the full benefits of DevOps and the cloud.

## Installing Azure Pipelines from GitHub Market Place

To install Azure Pipelines from GitHub Marketplace, follow these steps:

1. Sign in to your GitHub account and navigate to the Azure Pipelines page on the GitHub Marketplace.
2. Click the "Install it for free" button.
3. On the installation page, select the account you want to install Azure Pipelines to. You can either install it to an existing Azure DevOps organization or create a new one.
4. Click the "Install" button.
5. On the next page, you will be prompted to authorize the installation. Click the "Authorize" button to proceed.
6. After authorization, you will be redirected back to the Azure Pipelines page. You will see a message indicating that Azure Pipelines has been installed successfully.
7. To start using Azure Pipelines, click the "Go to Azure DevOps" button. This will take you to your Azure DevOps organization, where you can create a new pipeline or import an existing one.

## ****Configuring a Continuous Integration Pipeline****

1. Go to Pipelines and click on create new pipeline
2. Select GitHub as your remote origin and then select the repository you forked earlier
3. Select Node and then replace the code with the code given below

![Untitled](file://C:\Users\ashehzad\Downloads\Export-b48107c3-0936-4d74-be86-55ae681868f9\Implement%20CI%20with%20Azure%20Pipelines%20and%20GitHub%20Actio%2099b9acc747964c2d8178e4ed3c9b2cf3\Untitled%201.png)

```yaml
pool:
  vmImage: 'ubuntu-latest'
trigger:
  - master
  - main
steps:
  - task: CopyFiles@2
    displayName: 'Copy Files to: $(build.artifactstagingdirectory)/Templates'
    inputs:
      SourceFolder: deployment
      Contents: '*.json'
      TargetFolder: '$(build.artifactstagingdirectory)/Templates'
  - task: Npm@1
    displayName: 'npm custom'
    inputs:
      command: custom
      verbose: false
      customCommand: 'install --production'
  - task: ArchiveFiles@2
    displayName: 'Archive $(Build.SourcesDirectory)'
    inputs:
      rootFolderOrFile: '$(Build.SourcesDirectory)'
      includeRootFolder: false
  - task: PublishBuildArtifacts@1
    displayName: 'Publish Artifact: drop'
```

1. confirm the **Save and run** to commit the YAML definition directly to the master branch of the repo.

![Untitled](file://C:\Users\ashehzad\Downloads\Export-b48107c3-0936-4d74-be86-55ae681868f9\Implement%20CI%20with%20Azure%20Pipelines%20and%20GitHub%20Actio%2099b9acc747964c2d8178e4ed3c9b2cf3\Untitled%202.png)

## ****Adding a build status badge****

An important sign for a quality project is its build status badge. When someone finds a project that has a badge indicating that the project is currently in a successful build state, it’s a sign that the project is maintained effectively.

1. Click the build pipeline to navigate to its overview page.
2. From the **ellipses (…)** dropdown, select **Status badge**
  .

![Untitled](file://C:\Users\ashehzad\Downloads\Export-b48107c3-0936-4d74-be86-55ae681868f9\Implement%20CI%20with%20Azure%20Pipelines%20and%20GitHub%20Actio%2099b9acc747964c2d8178e4ed3c9b2cf3\Untitled%203.png)

1. Copy the markdown and add it your clone repository code

![Untitled](file://C:\Users\ashehzad\Downloads\Export-b48107c3-0936-4d74-be86-55ae681868f9\Implement%20CI%20with%20Azure%20Pipelines%20and%20GitHub%20Actio%2099b9acc747964c2d8178e4ed3c9b2cf3\Untitled%204.png)

push these changes to Github by following the commands

```yaml
git add . 
git commit -m "adding azure devops status badge"
git push origin master
```

<aside>
💡 **This is it for Continuous Integration, we will do more labs in the next sections. Here are some points you need to remember for exam.**

</aside>

## Configuring a job

Below the source’s node, you can add one or more jobs that will perform the bulk of the work that
you want to perform. Jobs can be added using the ellipsis on the Pipeline header. There are two types of jobs available:
• **Agentless jobs**: Agentless jobs can be used to run tasks that do not require an agent. They are
run on Azure DevOps Server.
• **Agent jobs**: Agent jobs are used to run tasks that require an agent to run on, which is the case
for the bulk of the tasks

## Variable groups

As well as creating the variables that go with a specific build, you can create various groups. These
variable groups can, in turn, be linked to one or more builds. This is an effective way of sharing variables between builds.

## Triggering the build

Check the Enable continuous integration box. This means that Azure DevOps will track for
changes in your repository and queue a new build as soon as a new chance is available.

## Task groups

When working in a team or organization that has more than one pipeline, it often doesn’t take long
before multiple pipelines that have the same shape emerge. For example, in some companies, all
pipelines contain tasks for security scanning, running tests, and calculating the test coverage.
Instead of repeating these tasks everywhere, they can be extracted from an existing pipeline into a task group. Task groups, in turn, can be used within multiple pipelines as if they are tasks themselves. Doing this reduces the effort needed to create a new pipeline or update all the pipelines with a new requirement. Doing this also ensures that all the pipelines using the task group have the same task configuration.

<aside>
💡 **The next Section is co-relate to this section, i will continue this lab CD part to the next section.**

</aside>

[What are feeds? - Azure Artifacts](https://learn.microsoft.com/en-us/azure/devops/artifacts/concepts/feeds?view=azure-devops)