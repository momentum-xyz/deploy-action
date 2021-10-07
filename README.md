# Github action to deploy Odyssey momentum projects

Shared build steps for Odyssey projects to deploy a project.
Requires the project to be build (so docker images pushed which can be picked up by the Kubernetes environment).


> :warning: **Currently only deploys development version**

## Usage

```yml
      - id: deploy
        if: ${{ github.ref == 'refs/heads/develop'}}
        uses: OdysseyMomentumExperience/deploy-action@v1
        with:
          project-name: ${{ env.PROJECT_NAME }}
          version: ${{ env.VERSION }}
          k8s-credential-name: ${{ secrets.REF_K8S_DEV }}
```


This requires there is a Github secret with Kubernetes credentials (JSON), with the name given by the `k8s-credential-name` input. This specifies which Kubernetes environment is deployed to.
The repository name is used by default as the project name, which should have a <name>-deployment resource in Kubernetes.

### Inputs
| Name | Description | Default |
| --- | --- | --- |
| `project` | Name of the project to deploy | The name of the repository |
| `version` | (**required**) Version |  |
| `k8s-credential-name` | (**required**) Name of the secret to use for Kubernetes credentials. |  |

