# ARCHIVE INFORMATION
> [!IMPORTANT]
> Due to lack of usage and maintenance, this repository has been archived.  
> Please read the [repository archival FAQ](https://docs.corp.spoton.sh/developer/undocumented-repositories-archival-faq/) for more information!


<!-- markdownlint-disable -->
<a href="https://cpco.io/homepage"><img src=".github/banner.png?raw=true" alt="Project Banner"/></a><br/>
    <p align="right">
<a href="https://github.com/cloudposse/github-action-deploy-helmfile/releases/latest"><img src="https://img.shields.io/github/release/cloudposse/github-action-deploy-helmfile.svg" alt="Latest Release"/></a><a href="https://slack.cloudposse.com"><img src="https://slack.cloudposse.com/badge.svg" alt="Slack Community"/></a></p>
<!-- markdownlint-restore -->

<!--




  ** DO NOT EDIT THIS FILE
  **
  ** This file was automatically generated by the `cloudposse/build-harness`.
  ** 1) Make all changes to `README.yaml`
  ** 2) Run `make init` (you only need to do this once)
  ** 3) Run`make readme` to rebuild this file.
  **
  ** (We maintain HUNDREDS of open source projects. This is how we maintain our sanity.)
  **





-->

Deploy on Kubernetes with HelmFile




## Introduction

Deploy on Kubernetes with HelmFile. 




## Usage

Deploy environment
```yaml
  name: Pull Request
  on:
    pull_request:
      branches: [ 'main' ]
      types: [opened, synchronize, reopened]

  jobs:
    deploy:
      runs-on: ubuntu-latest
      environment:
        name: preview
        url: ${{ steps.deploy.outputs.webapp-url }}  
      steps:
        
        - name: Configure AWS Credentials
          uses: aws-actions/configure-aws-credentials@v1.7.0
          with:
            aws-region: us-west-2
            role-to-assume: arn:aws:iam::111111111111:role/preview
            role-session-name: deploy
      
        - name: Deploy
          uses: cloudposse/github-action-deploy-helmfile@main
          id: deploy
          with:
            aws-region: us-west-2
            cluster: preview-eks
            environment: preview
            namespace: preview
            image: nginx
            image-tag: latest
            operation: deploy
            debug: false
  ```


Destroy environment
```yaml
  name: Pull Request
  on:
    pull_request:
      branches: [ 'main' ]
      types: [closed]

  jobs:
    destroy:
      runs-on: ubuntu-latest
      steps:
        - name: Configure AWS Credentials
          uses: aws-actions/configure-aws-credentials@v1.7.0
          with:
            aws-region: us-west-2
            role-to-assume: arn:aws:iam::111111111111:role/preview
            role-session-name: destroy          
      
        - name: Destroy
          uses: cloudposse/github-action-deploy-helmfile@main
          id: destroy
          with:
            aws-region: us-west-2
            cluster: preview-eks
            environment: preview
            namespace: preview
            image: "<none>"
            image-tag: "<none>"
            operation: destroy
            debug: false
  ```






<!-- markdownlint-disable -->

## Inputs

| Name | Description | Default | Required |
|------|-------------|---------|----------|
| aws-region | AWS region | us-east-1 | false |
| chamber\_version | Kubectl version | 2.11.1 | false |
| cluster | Cluster name | N/A | true |
| debug | Debug mode | false | false |
| environment | Helmfile environment | preview | false |
| gitref-sha | Git SHA |  | false |
| helm\_version | Helm version | 3.11.1 | false |
| helmfile | Helmfile name | helmfile.yaml | false |
| helmfile-path | The path where lives the helmfile. | deploy | false |
| helmfile\_version | Helmfile version | 0.143.5 | false |
| image | Docker image | N/A | true |
| image-tag | Docker image tag | N/A | true |
| kubectl\_version | Kubectl version | 1.26.3 | false |
| namespace | Kubernetes namespace | N/A | true |
| operation | Operation with helmfiles. (valid options - `deploy`, `destroy`) | deploy | true |
| release\_label\_name | The name of the label used to describe the helm release | release | false |
| values\_yaml | YAML string with extra values to use in a helmfile deploy | N/A | false |


## Outputs

| Name | Description |
|------|-------------|
| webapp-url | Web Application url |
<!-- markdownlint-restore -->


## Related Projects

Check out these related projects.



## References

For additional context, refer to some of these links.

- [github-actions-workflows](https://github.com/cloudposse/github-actions-workflows) - Reusable workflows for different types of projects
- [example-github-action-release-workflow](https://github.com/cloudposse/example-github-action-release-workflow) - Example application with complicated release workflow




## ✨ Contributing

This project is under active development, and we encourage contributions from our community.



Many thanks to our outstanding contributors:

<a href="https://github.com/cloudposse/github-action-deploy-helmfile/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=cloudposse/github-action-deploy-helmfile&max=24" />
</a>

For 🐛 bug reports & feature requests, please use the [issue tracker](https://github.com/cloudposse/github-action-deploy-helmfile/issues).

In general, PRs are welcome. We follow the typical "fork-and-pull" Git workflow.
 1. Review our [Code of Conduct](https://github.com/cloudposse/github-action-deploy-helmfile/?tab=coc-ov-file#code-of-conduct) and [Contributor Guidelines](https://github.com/cloudposse/.github/blob/main/CONTRIBUTING.md).
 2. **Fork** the repo on GitHub
 3. **Clone** the project to your own machine
 4. **Commit** changes to your own branch
 5. **Push** your work back up to your fork
 6. Submit a **Pull Request** so that we can review your changes

**NOTE:** Be sure to merge the latest changes from "upstream" before making a pull request!

### 🌎 Slack Community

Join our [Open Source Community](https://cpco.io/slack?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/github-action-deploy-helmfile&utm_content=slack) on Slack. It's **FREE** for everyone! Our "SweetOps" community is where you get to talk with others who share a similar vision for how to rollout and manage infrastructure. This is the best place to talk shop, ask questions, solicit feedback, and work together as a community to build totally *sweet* infrastructure.

### 📰 Newsletter

Sign up for [our newsletter](https://cpco.io/newsletter?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/github-action-deploy-helmfile&utm_content=newsletter) and join 3,000+ DevOps engineers, CTOs, and founders who get insider access to the latest DevOps trends, so you can always stay in the know.
Dropped straight into your Inbox every week — and usually a 5-minute read.

### 📆 Office Hours <a href="https://cloudposse.com/office-hours?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/github-action-deploy-helmfile&utm_content=office_hours"><img src="https://img.cloudposse.com/fit-in/200x200/https://cloudposse.com/wp-content/uploads/2019/08/Powered-by-Zoom.png" align="right" /></a>

[Join us every Wednesday via Zoom](https://cloudposse.com/office-hours?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/github-action-deploy-helmfile&utm_content=office_hours) for your weekly dose of insider DevOps trends, AWS news and Terraform insights, all sourced from our SweetOps community, plus a _live Q&A_ that you can’t find anywhere else.
It's **FREE** for everyone!
## License

<a href="https://opensource.org/licenses/Apache-2.0"><img src="https://img.shields.io/badge/License-Apache%202.0-blue.svg?style=for-the-badge" alt="License"></a>

<details>
<summary>Preamble to the Apache License, Version 2.0</summary>
<br/>
<br/>

Complete license is available in the [`LICENSE`](LICENSE) file.

```text
Licensed to the Apache Software Foundation (ASF) under one
or more contributor license agreements.  See the NOTICE file
distributed with this work for additional information
regarding copyright ownership.  The ASF licenses this file
to you under the Apache License, Version 2.0 (the
"License"); you may not use this file except in compliance
with the License.  You may obtain a copy of the License at

  https://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an
"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
KIND, either express or implied.  See the License for the
specific language governing permissions and limitations
under the License.
```
</details>

## Trademarks

All other trademarks referenced herein are the property of their respective owners.


---
Copyright © 2017-2024 [Cloud Posse, LLC](https://cpco.io/copyright)


<a href="https://cloudposse.com/readme/footer/link?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/github-action-deploy-helmfile&utm_content=readme_footer_link"><img alt="README footer" src="https://cloudposse.com/readme/footer/img"/></a>

<img alt="Beacon" width="0" src="https://ga-beacon.cloudposse.com/UA-76589703-4/cloudposse/github-action-deploy-helmfile?pixel&cs=github&cm=readme&an=github-action-deploy-helmfile"/>
