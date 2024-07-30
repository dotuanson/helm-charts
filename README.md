# How to package a helm chart

* Step 1: Create a helm chart

    Create from scratch
    ```shell
    # Create a very new chart
    cd ./helm-charts/charts
    helm create passbolt
    ```
  
    Create from an existing chart
* 
    ```shell
    cd ./helm-charts/charts
    # Download the chart
    helm pull passbolt-repo/https://download.passbolt.com/charts/passbolt

    # Extract the chart and modify it
    tar -xvf passbolt-0.7.0.tgz
    ```
    

* Step 2: Package the helm chart

    ```shell
    cd ./helm-charts/charts
    helm package passbolt
    
    # After that, we will have a file named passbolt-0.7.0.tgz, we need to move it to the root of the repo:
    mv passbolt-0.7.0.tgz ../
    ```

* Step 3: Now we are going to add our chart to that repo:

    ```shell
    cd ..
    helm repo index helm-charts/ --url https://dotuanson.github.io/helm-charts/
    
    # Then the index.yaml file will be updated with the new chart, now we need to push the changes to the repo:
    cd helm-charts
    git add .
    git commit -m "Add poly 3.0.1 chart"
    git push origin gh-pages
    ```

* Step 4: Now we can use our chart from the repo:

  ```yaml
  apiVersion: v2
  name: custom-app
  description: A Helm chart for Kubernetes
  
  # A chart can be either an 'application' or a 'library' chart.
  #
  # Application charts are a collection of templates that can be packaged into versioned archives
  # to be deployed.
  #
  # Library charts provide useful utilities or functions for the chart developer. They're included as
  # a dependency of application charts to inject those utilities and functions into the rendering
  # pipeline. Library charts do not define any templates and therefore cannot be deployed.
  type: application
  
  # This is the chart version. This version number should be incremented each time you make changes
  # to the chart and its templates, including the app version.
  # Versions are expected to follow Semantic Versioning (https://semver.org/)
  version: 0.1.0
  
  # This is the version number of the application being deployed. This version number should be
  # incremented each time you make changes to the application. Versions are not expected to
  # follow Semantic Versioning. They should reflect the version the application is using.
  # It is recommended to use it with quotes.
  appVersion: "1.16.0"
  
  dependencies:
    - name: passbolt
      repository: https://dotuanson.github.io/helm-charts/
      version: 0.7.0
  ```
