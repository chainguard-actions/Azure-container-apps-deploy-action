<!-- markdownlint-disable -->

# Hardening Report: Azure--container-apps-deploy-action/v1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **Azure--container-apps-deploy-action/v1** was hardened automatically. 119 finding(s) were identified and resolved across 2 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

These composite steps reference actions by a version tag instead of a full 40-character commit SHA: 'uses: azure/login@v1' (line 189), 'uses: docker/login-action@v2.2.0' (line 194) and 'uses: docker/login-action@v2.2.0' (line 202).

Locations:

- `action.yml:189`
- `action.yml:194`
- `action.yml:202`

### github-env-injection (severity: high)

Step 'Export Container Registry information to environment variable' writes values built from inputs.registryUrl, inputs.registryUsername and inputs.registryPassword to $GITHUB_ENV without printf '%s' | tr -d '\n\r' sanitization.

Locations:

- `action.yml:212`

### github-env-injection (severity: high)

Step 'Export Azure Container Registry information...' writes values built from inputs.acrName, inputs.acrUsername and inputs.acrPassword to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:225`

### github-env-injection (severity: high)

Step 'Get access token to log in to Azure Container Registry' writes CA_GH_ACTION_REGISTRY_URL, built from inputs.acrName, to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:238`

### github-env-injection (severity: high)

Step 'Export Dockerfile path to environment variable' writes a value built from inputs.appSourcePath and inputs.dockerfilePath to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:248`

### github-env-injection (severity: high)

Step 'Check for existing Dockerfile in application source' writes dockerfilePath, built from inputs.appSourcePath, to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:255`

### github-env-injection (severity: high)

Step 'Export name of image to build' writes inputs.imageToBuild to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:262`

### github-env-injection (severity: high)

Step 'Determine name of image to build if not provided' writes a value built from env.CA_GH_ACTION_REGISTRY_URL and github.* to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:269`

### github-env-injection (severity: high)

Step 'Export name of image to deploy' writes inputs.imageToDeploy to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:276`

### github-env-injection (severity: high)

Step 'Update name of image to deploy if not provided' writes env.CA_GH_ACTION_IMAGE_TO_BUILD to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:283`

### github-env-injection (severity: high)

Step 'Export resource group to environment variable' writes inputs.resourceGroup to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:290`

### github-env-injection (severity: high)

Step 'Determine resource group if not provided' writes a value built from inputs.containerAppName to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:297`

### github-env-injection (severity: high)

Step 'Set default location for Container Apps if location was provided' writes inputs.location to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:322`

### github-env-injection (severity: high)

Step 'Export location argument to environment variable' writes '--location ${{ inputs.location }}' to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:337`

### github-env-injection (severity: high)

Step 'Export environment to environment variable' writes inputs.containerAppEnvironment to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:353`

### github-env-injection (severity: high)

Step 'Determine environment name if not provided' writes a value built from inputs.containerAppName to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:360`

### github-env-injection (severity: high)

Step 'Reuse an existing Container App environment' writes an az query result, obtained using env.CA_GH_ACTION_RESOURCE_GROUP, to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:377`

### github-env-injection (severity: high)

Step 'Export ingress value to environment variable' writes '--ingress ${{ inputs.ingress }}' to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:412`

### github-env-injection (severity: high)

Step 'Export target port to environment variable' writes inputs.targetPort to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:421`

### github-env-injection (severity: high)

Step 'Export target port information...' writes env.CA_GH_ACTION_TARGET_PORT to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:442`

### github-env-injection (severity: high)

Step 'Export environment variables argument... if the Container App does not exist' writes inputs.environmentVariables to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:449`

### github-env-injection (severity: high)

Step 'Export environment variables argument... if the Container App does exist' writes inputs.environmentVariables to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:456`

### github-env-injection (severity: high)

Step 'Parse the given runtime stack input...' writes values parsed from inputs.runtimeStack to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:501`

### github-env-injection (severity: high)

Step 'Set platform environment variables for builder invocation' writes values built from env.CA_GH_ACTION_RUNTIME_STACK_* to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:512`

### github-env-injection (severity: high)

Step 'Set port environment variable for builder invocation' writes the inherited CA_GH_ACTION_ORYX_BUILDER_ENV_ARG and env.CA_GH_ACTION_TARGET_PORT to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:519`

### github-env-injection (severity: high)

Step 'Reset the environment variables argument environment variable for the up command' writes inputs.environmentVariables to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:658`

### github-env-injection (severity: high)

Step 'End timer that's tracking action execution length' writes a value derived from env.CA_GH_ACTION_START_MILLISECONDS to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:693`

### script-injection (severity: high)

(a) Step 'Export Container Registry information...' puts expressions directly in run:, e.g. 'CA_GH_ACTION_REGISTRY_LOGIN_ARG="--registry-server ${{ inputs.registryUrl }} --registry-username ${{ inputs.registryUsername }} --registry-password ${{ inputs.registryPassword }}"'.

Locations:

- `action.yml:213`

### script-injection (severity: high)

(a) Step 'Export Azure Container Registry information...' contains '--registry-server ${{ inputs.acrName }}.azurecr.io --registry-username ${{ inputs.acrUsername }} --registry-password ${{ inputs.acrPassword }}'.

Locations:

- `action.yml:226`

### script-injection (severity: high)

(a) Step 'Get access token...' contains 'az acr login --name ${{ inputs.acrName }} ...' and 'docker login ${{ inputs.acrName }}.azurecr.io ...'.

Locations:

- `action.yml:239`

### script-injection (severity: high)

(a) Step 'Export Dockerfile path...' contains 'CA_GH_ACTION_DOCKERFILE_PATH="${{ inputs.appSourcePath }}/${{ inputs.dockerfilePath }}"'.

Locations:

- `action.yml:249`

### script-injection (severity: high)

(a) Step 'Check for existing Dockerfile...' contains 'dockerfilePath=${{ inputs.appSourcePath }}/Dockerfile'.

Locations:

- `action.yml:256`

### script-injection (severity: high)

(a) Step 'Export name of image to build' contains 'CA_GH_ACTION_IMAGE_TO_BUILD="${{ inputs.imageToBuild }}"'.

Locations:

- `action.yml:263`

### script-injection (severity: high)

(a) Step 'Determine name of image to build' contains '"${{ env.CA_GH_ACTION_REGISTRY_URL }}/github-action/container-app:${{ github.run_id }}.${{ github.run_attempt }}"'.

Locations:

- `action.yml:270`

### script-injection (severity: high)

(a) Step 'Export name of image to deploy' contains 'CA_GH_ACTION_IMAGE_TO_DEPLOY="${{ inputs.imageToDeploy }}"'.

Locations:

- `action.yml:277`

### script-injection (severity: high)

(a) Step 'Update name of image to deploy' contains 'CA_GH_ACTION_IMAGE_TO_DEPLOY="${{ env.CA_GH_ACTION_IMAGE_TO_BUILD }}"'.

Locations:

- `action.yml:284`

### script-injection (severity: high)

(a) Step 'Export resource group' contains 'CA_GH_ACTION_RESOURCE_GROUP="${{ inputs.resourceGroup }}"'.

Locations:

- `action.yml:291`

### script-injection (severity: high)

(a) Step 'Determine resource group if not provided' contains 'CA_GH_ACTION_RESOURCE_GROUP="${{ inputs.containerAppName }}-rg"'.

Locations:

- `action.yml:298`

### script-injection (severity: high)

(a) Step 'Check if the previously generated resource group exists' contains '-n ${{ env.CA_GH_ACTION_RESOURCE_GROUP }}'.

Locations:

- `action.yml:306`

### script-injection (severity: high)

(a) Step 'Set default location... if location was provided' contains 'CA_GH_ACTION_DEFAULT_LOCATION="${{ inputs.location }}"'.

Locations:

- `action.yml:323`

### script-injection (severity: high)

(a) Step 'Create resource group' contains '-n ${{ env.CA_GH_ACTION_RESOURCE_GROUP }}' and '-l ${{ env.CA_GH_ACTION_DEFAULT_LOCATION }}'.

Locations:

- `action.yml:331`

### script-injection (severity: high)

(a) Step 'Export location argument' contains 'CA_GH_ACTION_CONTAINER_APP_LOCATION_ARG="--location ${{ inputs.location }}"'.

Locations:

- `action.yml:338`

### script-injection (severity: high)

(a) Step 'Check if the Container App already exists' contains '-g ${{ env.CA_GH_ACTION_RESOURCE_GROUP }}' and '-n ${{ inputs.containerAppName }}'.

Locations:

- `action.yml:345`

### script-injection (severity: high)

(a) Step 'Export environment to environment variable' contains 'CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT="${{ inputs.containerAppEnvironment }}"'.

Locations:

- `action.yml:354`

### script-injection (severity: high)

(a) Step 'Determine environment name' contains 'CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT="${{ inputs.containerAppName }}-env"'.

Locations:

- `action.yml:361`

### script-injection (severity: high)

(a) Step 'Check if Container App environment already exists' contains '-g ${{ env.CA_GH_ACTION_RESOURCE_GROUP }}' and '-n ${{ env.CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT }}'.

Locations:

- `action.yml:369`

### script-injection (severity: high)

(a) Step 'Reuse an existing Container App environment' contains 'az containerapp env list -g ${{ env.CA_GH_ACTION_RESOURCE_GROUP }}'. (b) It also uses an unquoted '[[ $CA_GH_ACTION_TEMP_ENV_NAME != '' ]]'.

Locations:

- `action.yml:378`

### script-injection (severity: high)

(a) Step 'Create Container App environment' contains '-g ${{ env.CA_GH_ACTION_RESOURCE_GROUP }}', '-n ${{ env.CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT }}' and '${{ env.CA_GH_ACTION_CONTAINER_APP_LOCATION_ARG }}'.

Locations:

- `action.yml:389`

### script-injection (severity: high)

(a) Step 'Export ingress value' contains 'CA_GH_ACTION_INGRESS_ARG="--ingress ${{ inputs.ingress }}"'.

Locations:

- `action.yml:415`

### script-injection (severity: high)

(a) Step 'Export target port' contains 'CA_GH_ACTION_TARGET_PORT="${{ inputs.targetPort }}"'.

Locations:

- `action.yml:422`

### script-injection (severity: high)

(a) Step 'Export target port information' contains 'CA_GH_ACTION_TARGET_PORT_ARG="--target-port ${{ env.CA_GH_ACTION_TARGET_PORT }}"'.

Locations:

- `action.yml:443`

### script-injection (severity: high)

(a) Step 'Export environment variables argument (does not exist)' contains '"--env-vars ${{ inputs.environmentVariables }}"'.

Locations:

- `action.yml:450`

### script-injection (severity: high)

(a) Step 'Export environment variables argument (does exist)' contains '"--replace-env-vars ${{ inputs.environmentVariables }}"'.

Locations:

- `action.yml:457`

### script-injection (severity: high)

(a) Step 'Install pack CLI on non-Windows runner' contains 'curl -sSL "https://github.com/buildpacks/pack/releases/download/v0.31.0/pack-v0.31.0-${{ runner.os }}.tgz"'.

Locations:

- `action.yml:463`

### script-injection (severity: high)

(a) Step 'Parse the given runtime stack input' contains 'IFS=':' read -ra CA_GH_ACTION_RUNTIME_STACK <<< "${{ inputs.runtimeStack }}"'.

Locations:

- `action.yml:502`

### script-injection (severity: high)

(a) Step 'Set platform environment variables for builder invocation' contains '--env ORYX_PLATFORM_NAME=${{ env.CA_GH_ACTION_RUNTIME_STACK_PLATFORM }} --env ORYX_PLATFORM_VERSION=${{ env.CA_GH_ACTION_RUNTIME_STACK_VERSION }}'.

Locations:

- `action.yml:513`

### script-injection (severity: high)

(a) Step 'Set port environment variable for builder invocation' contains '--env ORYX_RUNTIME_PORT=${{ env.CA_GH_ACTION_TARGET_PORT }}'.

Locations:

- `action.yml:520`

### script-injection (severity: high)

(a) Step 'Create runnable application image using bullseye Oryx++ Builder' contains 'pack build ${{ env.CA_GH_ACTION_IMAGE_TO_DEPLOY }} --path ${{ inputs.appSourcePath }} ... ${{ env.CA_GH_ACTION_ORYX_BUILDER_ENV_ARG }} ${{ env.CA_GH_ACTION_ORYX_BUILDER_TELEMETRY_ARG }}'.

Locations:

- `action.yml:527`

### script-injection (severity: high)

(a) Step 'Create runnable application image using bookworm Oryx++ Builder' contains 'pack build ${{ env.CA_GH_ACTION_IMAGE_TO_DEPLOY }} --path ${{ inputs.appSourcePath }} ...'.

Locations:

- `action.yml:541`

### script-injection (severity: high)

(a) Step 'Create runnable application image using builder version specified by input' contains '--builder mcr.microsoft.com/oryx/builder:${{ inputs.builderStack }}' and '--path ${{ inputs.appSourcePath }}'.

Locations:

- `action.yml:554`

### script-injection (severity: high)

(a) Step 'Create runnable application image using provided Dockerfile' contains 'docker build --tag ${{ env.CA_GH_ACTION_IMAGE_TO_DEPLOY }} --file ${{ env.CA_GH_ACTION_DOCKERFILE_PATH }} ${{ inputs.appSourcePath }}'.

Locations:

- `action.yml:574`

### script-injection (severity: high)

(a) Step 'Push image to Container Registry' contains 'run: docker push ${{ env.CA_GH_ACTION_IMAGE_TO_DEPLOY }}'.

Locations:

- `action.yml:582`

### script-injection (severity: high)

(a) Step 'Create the Container App from a YAML configuration file' contains '-n ${{ inputs.containerAppName }}' and '--yaml ${{ inputs.yamlConfigPath }}'.

Locations:

- `action.yml:588`

### script-injection (severity: high)

(a) Step 'Create the Container App from provided arguments' contains '-n ${{ inputs.containerAppName }}', '-i ${{ env.CA_GH_ACTION_IMAGE_TO_DEPLOY }}', '${{ env.CA_GH_ACTION_REGISTRY_LOGIN_ARG }}' and '${{ env.CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT_VARIABLES_ARG }}'.

Locations:

- `action.yml:598`

### script-injection (severity: high)

(a) Step 'Update the existing Container App from a YAML configuration file' contains '-n ${{ inputs.containerAppName }}' and '--yaml ${{ inputs.yamlConfigPath }}'.

Locations:

- `action.yml:613`

### script-injection (severity: high)

(a) Step 'Update the Container Registry details' contains '--server ${{ env.CA_GH_ACTION_REGISTRY_URL }} --username ${{ env.CA_GH_ACTION_REGISTRY_USERNAME }} --password ${{ env.CA_GH_ACTION_REGISTRY_PASSWORD }}'.

Locations:

- `action.yml:630`

### script-injection (severity: high)

(a) Step 'Update the existing Container App ... via update' contains '-n ${{ inputs.containerAppName }}', '-i ${{ env.CA_GH_ACTION_IMAGE_TO_DEPLOY }}' and '${{ env.CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT_VARIABLES_ARG }}'.

Locations:

- `action.yml:641`

### script-injection (severity: high)

(a) Step 'Reset the environment variables argument for the up command' contains '"--env-vars ${{ inputs.environmentVariables }}"'.

Locations:

- `action.yml:659`

### script-injection (severity: high)

(a) Step 'Update the existing Container App ... via up' contains 'az containerapp up -g ${{ env.CA_GH_ACTION_RESOURCE_GROUP }} -n ${{ inputs.containerAppName }} ... ${{ env.CA_GH_ACTION_REGISTRY_LOGIN_ARG }}'.

Locations:

- `action.yml:666`

### script-injection (severity: high)

(a) Step 'Disable ingress on the existing Container App' contains '-g ${{ env.CA_GH_ACTION_RESOURCE_GROUP }}' and '-n ${{ inputs.containerAppName }}'.

Locations:

- `action.yml:679`

### script-injection (severity: high)

(a) Step 'End timer' contains 'CA_GH_ACTION_START_MILLISECONDS=${{ env.CA_GH_ACTION_START_MILLISECONDS }}'.

Locations:

- `action.yml:695`

### script-injection (severity: high)

(a) Step 'Log telemetry for action' contains '-c "oryx telemetry --event-name 'ContainerAppsGitHubAction' ${{ env.CA_GH_ACTION_LENGTH_MILLISECONDS_ARG }} ${{ env.CA_GH_ACTION_SCENARIO_ARG }} ${{ env.CA_GH_ACTION_RESULT_ARG }}"'.

Locations:

- `action.yml:727`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.registryUrl }}" appears directly in run: block of step "Export Container Registry information to environment variable"; move to env: map

Locations:

- `action.yml:213`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.registryUsername }}" appears directly in run: block of step "Export Container Registry information to environment variable"; move to env: map

Locations:

- `action.yml:213`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.registryPassword }}" appears directly in run: block of step "Export Container Registry information to environment variable"; move to env: map

Locations:

- `action.yml:213`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.registryUrl }}" appears directly in run: block of step "Export Container Registry information to environment variable"; move to env: map

Locations:

- `action.yml:214`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.registryUsername }}" appears directly in run: block of step "Export Container Registry information to environment variable"; move to env: map

Locations:

- `action.yml:215`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.registryPassword }}" appears directly in run: block of step "Export Container Registry information to environment variable"; move to env: map

Locations:

- `action.yml:216`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.acrName }}" appears directly in run: block of step "Export Azure Container Registry information to environment variable for Azure CLI command"; move to env: map

Locations:

- `action.yml:226`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.acrUsername }}" appears directly in run: block of step "Export Azure Container Registry information to environment variable for Azure CLI command"; move to env: map

Locations:

- `action.yml:226`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.acrPassword }}" appears directly in run: block of step "Export Azure Container Registry information to environment variable for Azure CLI command"; move to env: map

Locations:

- `action.yml:226`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.acrName }}" appears directly in run: block of step "Export Azure Container Registry information to environment variable for Azure CLI command"; move to env: map

Locations:

- `action.yml:227`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.acrUsername }}" appears directly in run: block of step "Export Azure Container Registry information to environment variable for Azure CLI command"; move to env: map

Locations:

- `action.yml:228`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.acrPassword }}" appears directly in run: block of step "Export Azure Container Registry information to environment variable for Azure CLI command"; move to env: map

Locations:

- `action.yml:229`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.acrName }}" appears directly in run: block of step "Get access token to log in to Azure Container Registry"; move to env: map

Locations:

- `action.yml:239`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.acrName }}" appears directly in run: block of step "Get access token to log in to Azure Container Registry"; move to env: map

Locations:

- `action.yml:241`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.acrName }}" appears directly in run: block of step "Get access token to log in to Azure Container Registry"; move to env: map

Locations:

- `action.yml:242`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.appSourcePath }}" appears directly in run: block of step "Export Dockerfile path to environment variable"; move to env: map

Locations:

- `action.yml:249`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.dockerfilePath }}" appears directly in run: block of step "Export Dockerfile path to environment variable"; move to env: map

Locations:

- `action.yml:249`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.appSourcePath }}" appears directly in run: block of step "Check for existing Dockerfile in application source"; move to env: map

Locations:

- `action.yml:256`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.imageToBuild }}" appears directly in run: block of step "Export name of image to build to environment variable"; move to env: map

Locations:

- `action.yml:263`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.imageToDeploy }}" appears directly in run: block of step "Export name of image to deploy to environment variable"; move to env: map

Locations:

- `action.yml:277`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.resourceGroup }}" appears directly in run: block of step "Export resource group to environment variable"; move to env: map

Locations:

- `action.yml:291`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.containerAppName }}" appears directly in run: block of step "Determine resource group if not provided"; move to env: map

Locations:

- `action.yml:298`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.location }}" appears directly in run: block of step "Set default location for Container Apps if location was provided"; move to env: map

Locations:

- `action.yml:323`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.location }}" appears directly in run: block of step "Export location argument to environment variable"; move to env: map

Locations:

- `action.yml:338`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.containerAppName }}" appears directly in run: block of step "Check if the Container App already exists in the resource group"; move to env: map

Locations:

- `action.yml:346`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.containerAppEnvironment }}" appears directly in run: block of step "Export environment to environment variable"; move to env: map

Locations:

- `action.yml:354`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.containerAppName }}" appears directly in run: block of step "Determine environment name if not provided"; move to env: map

Locations:

- `action.yml:361`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.ingress }}" appears directly in run: block of step "Export ingress value to environment variable"; move to env: map

Locations:

- `action.yml:415`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.targetPort }}" appears directly in run: block of step "Export target port to environment variable"; move to env: map

Locations:

- `action.yml:422`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.environmentVariables }}" appears directly in run: block of step "Export environment variables argument to environment variable if the Container App does not exist"; move to env: map

Locations:

- `action.yml:450`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.environmentVariables }}" appears directly in run: block of step "Export environment variables argument to environment variable if the Container App does exist"; move to env: map

Locations:

- `action.yml:457`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.runtimeStack }}" appears directly in run: block of step "Parse the given runtime stack input and export the platform and version to environment variables"; move to env: map

Locations:

- `action.yml:502`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.appSourcePath }}" appears directly in run: block of step "Create runnable application image using bullseye Oryx++ Builder"; move to env: map

Locations:

- `action.yml:529`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.appSourcePath }}" appears directly in run: block of step "Create runnable application image using bookworm Oryx++ Builder"; move to env: map

Locations:

- `action.yml:543`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.appSourcePath }}" appears directly in run: block of step "Create runnable application image using builder version specified by input"; move to env: map

Locations:

- `action.yml:556`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.builderStack }}" appears directly in run: block of step "Create runnable application image using builder version specified by input"; move to env: map

Locations:

- `action.yml:557`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.appSourcePath }}" appears directly in run: block of step "Create runnable application image using provided Dockerfile"; move to env: map

Locations:

- `action.yml:577`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.containerAppName }}" appears directly in run: block of step "Create the Container App from a YAML configuration file"; move to env: map

Locations:

- `action.yml:590`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.yamlConfigPath }}" appears directly in run: block of step "Create the Container App from a YAML configuration file"; move to env: map

Locations:

- `action.yml:591`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.containerAppName }}" appears directly in run: block of step "Create the Container App from provided arguments"; move to env: map

Locations:

- `action.yml:600`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.containerAppName }}" appears directly in run: block of step "Update the existing Container App from a YAML configuration file"; move to env: map

Locations:

- `action.yml:615`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.yamlConfigPath }}" appears directly in run: block of step "Update the existing Container App from a YAML configuration file"; move to env: map

Locations:

- `action.yml:616`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.containerAppName }}" appears directly in run: block of step "Update the Container Registry details on the existing Container App"; move to env: map

Locations:

- `action.yml:632`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.containerAppName }}" appears directly in run: block of step "Update the existing Container App from provided arguments via 'update' (no ingress values provided)"; move to env: map

Locations:

- `action.yml:643`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.environmentVariables }}" appears directly in run: block of step "Reset the environment variables argument environment variable for the 'up' command"; move to env: map

Locations:

- `action.yml:659`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.containerAppName }}" appears directly in run: block of step "Update the existing Container App from provided arguments via 'up' (ingress values provided)"; move to env: map

Locations:

- `action.yml:668`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.containerAppName }}" appears directly in run: block of step "Disable ingress on the existing Container App"; move to env: map

Locations:

- `action.yml:681`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, github-env-injection, script-injection, static-inline-injection

**Notes:**

All changes are in action.yml; the file was re-read in full afterwards, nothing was run.

- **unpinned-uses:** azure/login is now pinned to cb79c773a3cfa27f31f25eb3f677781210c9ce3d (# v1). Both docker/login-action uses are pinned to 465a07811f14bebb1938fbed4728c6a1ff8901fc (# v2.2.0).
- **script-injection / static-inline-injection:** every inputs.* expression used in a run: block now goes through the step's env: block (INPUT_* variables). Every ${{ env.X }} is now a quoted $X, and github.run_id, github.run_attempt and runner.os became $GITHUB_RUN_ID, $GITHUB_RUN_ATTEMPT and $RUNNER_OS. Single values (names, paths, image, registry details) are passed double-quoted.
- **Combined argument strings:** some saved values hold several arguments (CA_GH_ACTION_*_ARG: ingress, target port, registry login, env vars, location, Oryx builder env and telemetry). Upstream pasted these straight into the script, so the shell split them and honoured quotes, e.g. --env "CALLER_ID=...". To keep that, each consuming step splits them into a bash array with the quote-aware xargs split (empty-value guard, unmatched-quote check, xargs -r) and passes "${args[@]}".
- **Telemetry step:** it now builds the docker bash -c string from env vars instead of expressions. The container's shell still parses it as before.
- **Timer step:** it reads CA_GH_ACTION_START_MILLISECONDS from the environment and checks it is all digits before the arithmetic.
- **github-env-injection:** every value written to GITHUB_ENV is now passed through printf '%s' | tr -d '\n\r'. A side effect: a multi-line environmentVariables value now has its lines joined with no space, so 'a=1' and 'b=2' on two lines become 'a=1b=2'. Upstream mishandled that too: each extra line was written to GITHUB_ENV as a separate variable.
- **Reuse environment step:** it also strips the JSON double quotes from the az query result. Upstream's inline expression had the shell drop them, so the environment name reaching az is the same.
- **Unquoted check:** the [[ $CA_GH_ACTION_TEMP_ENV_NAME != '' ]] test is now quoted.
- **Left unchanged on purpose:** upstream's dead dotnetcore check (it is missing a $, so it never matches) stays, so behaviour doesn't change. Fixed-string GITHUB_ENV writes, which take no outside input, were also left alone.

### Iteration 1

**Fixes applied:** script-injection

**Notes:**

I fixed the script-injection finding in the 'Log telemetry for action' step of action.yml. I haven't run the action to test the change.

The step used to paste three environment variables (CA_GH_ACTION_LENGTH_MILLISECONDS_ARG, CA_GH_ACTION_SCENARIO_ARG and CA_GH_ACTION_RESULT_ARG) into a command string that a second bash inside the container ran. Now:
- Each variable is checked against the exact forms the action itself writes: a numeric processing time, scenario=used-image/dockerfile/builder, and result=succeeded/failed.
- Only the inner value is kept and added to a bash array.
- The array goes to the container as separate arguments, with `bash -c 'oryx telemetry --event-name ContainerAppsGitHubAction "$@"' _ args...`, so the inner bash only passes them on and never runs them as code.

oryx should receive the same arguments as before, because upstream's inner bash also stripped the single quotes around each value. One difference: a value that doesn't match an allowed form (for example, one the calling workflow set to something else) is now silently dropped instead of passed on.

