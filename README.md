# ADO Pipeline Template for Docker Build

This template contains an Azure pipeline that can be extended to build an image from a docker file under different Azure pipelines.

## use case

You need to have a service connection related to GitHub on the Azure DevOps project.
To call this in your pipeline you can follow this example:

   ```yaml
  # azure-pipeline.yml
  parameters:

    - name: RegistryToken
      type: string

    - name: imageRepository
      type: string

    - name: tags
      type: string

  resources:
    repositories:
      - repository: Docker
        type: github
        name: NashTech-Labs/ado.docker.push
        ref: main
        endpoint: '<GitHub Service Connection>'

  steps:

  - template: build.yml@Docker
    parameters:
        containerRegistry: '${{parameters.RegistryToken}}'
        repository: '${{parameters.imageRepository}}'
        tags: ${{parameters.tags}}
  ```

You can also use Variable Group and Azure Key Vault for values.
