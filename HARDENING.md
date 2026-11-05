<!-- markdownlint-disable -->

# Hardening Report: Azure--container-apps-deploy-action/v1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **Azure--container-apps-deploy-action/v1** was hardened automatically. 118 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Three composite steps use actions pinned to a tag instead of a 40-character commit SHA: `uses: azure/login@v1` (line 188), `uses: docker/login-action@v2.2.0` (line 193) and `uses: docker/login-action@v2.2.0` (line 201).

Locations:

- `action.yml:188`
- `action.yml:193`
- `action.yml:201`

### script-injection (severity: high)

(a) Step 'Export Container Registry information to environment variable' puts ${{ inputs.registryUrl }}, ${{ inputs.registryUsername }} and ${{ inputs.registryPassword }} directly into the run script, e.g. `CA_GH_ACTION_REGISTRY_URL=${{ inputs.registryUrl }}`.

Locations:

- `action.yml:212`

### script-injection (severity: high)

(a) Step 'Export Azure Container Registry information...' puts ${{ inputs.acrName }}, ${{ inputs.acrUsername }} and ${{ inputs.acrPassword }} directly into the run script.

Locations:

- `action.yml:225`

### script-injection (severity: high)

(a) Step 'Get access token to log in to Azure Container Registry' puts ${{ inputs.acrName }} directly into the script: `az acr login --name ${{ inputs.acrName }} ...` and `docker login ${{ inputs.acrName }}.azurecr.io`. (b) `$CA_GH_ACTION_ACR_ACCESS_TOKEN` is expanded without quotes.

Locations:

- `action.yml:238`

### script-injection (severity: high)

(a) Step 'Export Dockerfile path to environment variable': `CA_GH_ACTION_DOCKERFILE_PATH="${{ inputs.appSourcePath }}/${{ inputs.dockerfilePath }}"`.

Locations:

- `action.yml:248`

### script-injection (severity: high)

(a) Step 'Check for existing Dockerfile in application source': `dockerfilePath=${{ inputs.appSourcePath }}/Dockerfile`.

Locations:

- `action.yml:255`

### script-injection (severity: high)

(a) Step 'Export name of image to build to environment variable': `CA_GH_ACTION_IMAGE_TO_BUILD="${{ inputs.imageToBuild }}"`.

Locations:

- `action.yml:262`

### script-injection (severity: high)

(a) Step 'Determine name of image to build if not provided' puts ${{ env.CA_GH_ACTION_REGISTRY_URL }}, ${{ github.run_id }} and ${{ github.run_attempt }} directly into the run script.

Locations:

- `action.yml:269`

### script-injection (severity: high)

(a) Step 'Export name of image to deploy to environment variable': `CA_GH_ACTION_IMAGE_TO_DEPLOY="${{ inputs.imageToDeploy }}"`.

Locations:

- `action.yml:276`

### script-injection (severity: high)

(a) Step 'Update name of image to deploy if not provided': `CA_GH_ACTION_IMAGE_TO_DEPLOY="${{ env.CA_GH_ACTION_IMAGE_TO_BUILD }}"`.

Locations:

- `action.yml:283`

### script-injection (severity: high)

(a) Step 'Export resource group to environment variable': `CA_GH_ACTION_RESOURCE_GROUP="${{ inputs.resourceGroup }}"`.

Locations:

- `action.yml:290`

### script-injection (severity: high)

(a) Step 'Determine resource group if not provided': `CA_GH_ACTION_RESOURCE_GROUP="${{ inputs.containerAppName }}-rg"`.

Locations:

- `action.yml:297`

### script-injection (severity: high)

(a) Step 'Check if the previously generated resource group exists': `-n ${{ env.CA_GH_ACTION_RESOURCE_GROUP }}`.

Locations:

- `action.yml:305`

### script-injection (severity: high)

(b) Step 'Get default location...': `echo $CA_GH_ACTION_DEFAULT_LOCATION` is expanded without quotes.

Locations:

- `action.yml:314`

### script-injection (severity: high)

(a) Step 'Set default location for Container Apps if location was provided': `CA_GH_ACTION_DEFAULT_LOCATION="${{ inputs.location }}"`.

Locations:

- `action.yml:322`

### script-injection (severity: high)

(a) Step 'Create resource group if it doesn't exist': `-n ${{ env.CA_GH_ACTION_RESOURCE_GROUP }}` and `-l ${{ env.CA_GH_ACTION_DEFAULT_LOCATION }}`.

Locations:

- `action.yml:330`

### script-injection (severity: high)

(a) Step 'Export location argument to environment variable': `CA_GH_ACTION_CONTAINER_APP_LOCATION_ARG="--location ${{ inputs.location }}"`.

Locations:

- `action.yml:337`

### script-injection (severity: high)

(a) Step 'Check if the Container App already exists in the resource group': `-g ${{ env.CA_GH_ACTION_RESOURCE_GROUP }}` and `-n ${{ inputs.containerAppName }}`.

Locations:

- `action.yml:344`

### script-injection (severity: high)

(a) Step 'Export environment to environment variable': `CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT="${{ inputs.containerAppEnvironment }}"`.

Locations:

- `action.yml:353`

### script-injection (severity: high)

(a) Step 'Determine environment name if not provided': `CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT="${{ inputs.containerAppName }}-env"`.

Locations:

- `action.yml:360`

### script-injection (severity: high)

(a) Step 'Check if Container App environment already exists...': `-g ${{ env.CA_GH_ACTION_RESOURCE_GROUP }}` and `-n ${{ env.CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT }}`.

Locations:

- `action.yml:368`

### script-injection (severity: high)

(a) Step 'Reuse an existing Container App environment...': `az containerapp env list -g ${{ env.CA_GH_ACTION_RESOURCE_GROUP }}`. (b) `[[ $CA_GH_ACTION_TEMP_ENV_NAME != '' ]]` is expanded without quotes.

Locations:

- `action.yml:377`

### script-injection (severity: high)

(a) Step 'Create Container App environment...': `-g ${{ env.CA_GH_ACTION_RESOURCE_GROUP }}`, `-n ${{ env.CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT }}` and `${{ env.CA_GH_ACTION_CONTAINER_APP_LOCATION_ARG }}`.

Locations:

- `action.yml:388`

### script-injection (severity: high)

(a) Step 'Export ingress value to environment variable': `CA_GH_ACTION_INGRESS_ARG="--ingress ${{ inputs.ingress }}"`.

Locations:

- `action.yml:414`

### script-injection (severity: high)

(a) Step 'Export target port to environment variable': `CA_GH_ACTION_TARGET_PORT="${{ inputs.targetPort }}"`.

Locations:

- `action.yml:421`

### script-injection (severity: high)

(a) Step 'Export target port information...': `CA_GH_ACTION_TARGET_PORT_ARG="--target-port ${{ env.CA_GH_ACTION_TARGET_PORT }}"`.

Locations:

- `action.yml:442`

### script-injection (severity: high)

(a) Step 'Export environment variables argument ... does not exist': `CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT_VARIABLES_ARG="--env-vars ${{ inputs.environmentVariables }}"`.

Locations:

- `action.yml:449`

### script-injection (severity: high)

(a) Step 'Export environment variables argument ... does exist': `CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT_VARIABLES_ARG="--replace-env-vars ${{ inputs.environmentVariables }}"`.

Locations:

- `action.yml:456`

### script-injection (severity: high)

(a) Step 'Install pack CLI on non-Windows runner': `curl -sSL "https://github.com/buildpacks/pack/releases/download/v0.31.0/pack-v0.31.0-${{ runner.os }}.tgz"`. Any `${{ }}` inside a run block fails this check, including runner.*.

Locations:

- `action.yml:462`

### script-injection (severity: high)

(a) Step 'Parse the given runtime stack input...': `IFS=':' read -ra CA_GH_ACTION_RUNTIME_STACK <<< "${{ inputs.runtimeStack }}"`.

Locations:

- `action.yml:501`

### script-injection (severity: high)

(a) Step 'Set platform environment variables for builder invocation': `--env ORYX_PLATFORM_NAME=${{ env.CA_GH_ACTION_RUNTIME_STACK_PLATFORM }} --env ORYX_PLATFORM_VERSION=${{ env.CA_GH_ACTION_RUNTIME_STACK_VERSION }}`.

Locations:

- `action.yml:512`

### script-injection (severity: high)

(a) Step 'Set port environment variable for builder invocation': `--env ORYX_RUNTIME_PORT=${{ env.CA_GH_ACTION_TARGET_PORT }}`.

Locations:

- `action.yml:519`

### script-injection (severity: high)

(a) Step 'Create runnable application image using bullseye Oryx++ Builder': `pack build ${{ env.CA_GH_ACTION_IMAGE_TO_DEPLOY }} --path ${{ inputs.appSourcePath }} ... ${{ env.CA_GH_ACTION_ORYX_BUILDER_ENV_ARG }} ${{ env.CA_GH_ACTION_ORYX_BUILDER_TELEMETRY_ARG }}`.

Locations:

- `action.yml:527`

### script-injection (severity: high)

(a) Step 'Create runnable application image using bookworm Oryx++ Builder': `pack build ${{ env.CA_GH_ACTION_IMAGE_TO_DEPLOY }} --path ${{ inputs.appSourcePath }} ...` plus env-arg expressions.

Locations:

- `action.yml:541`

### script-injection (severity: high)

(a) Step 'Create runnable application image using builder version specified by input': `--builder mcr.microsoft.com/oryx/builder:${{ inputs.builderStack }}`, `--path ${{ inputs.appSourcePath }}` and env expressions.

Locations:

- `action.yml:554`

### script-injection (severity: high)

(a) Step 'Create runnable application image using provided Dockerfile': `--tag ${{ env.CA_GH_ACTION_IMAGE_TO_DEPLOY }} --file ${{ env.CA_GH_ACTION_DOCKERFILE_PATH }} ${{ inputs.appSourcePath }}`.

Locations:

- `action.yml:574`

### script-injection (severity: high)

(a) Step 'Push image to Container Registry': `run: docker push ${{ env.CA_GH_ACTION_IMAGE_TO_DEPLOY }}`.

Locations:

- `action.yml:581`

### script-injection (severity: high)

(a) Step 'Create the Container App from a YAML configuration file': `-g ${{ env.CA_GH_ACTION_RESOURCE_GROUP }} -n ${{ inputs.containerAppName }} --yaml ${{ inputs.yamlConfigPath }}`.

Locations:

- `action.yml:588`

### script-injection (severity: high)

(a) Step 'Create the Container App from provided arguments' puts ${{ inputs.containerAppName }} and several ${{ env.* }} expressions into the script, including `${{ env.CA_GH_ACTION_REGISTRY_LOGIN_ARG }}` and `${{ env.CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT_VARIABLES_ARG }}`.

Locations:

- `action.yml:598`

### script-injection (severity: high)

(a) Step 'Update the existing Container App from a YAML configuration file': `-n ${{ inputs.containerAppName }} --yaml ${{ inputs.yamlConfigPath }}`.

Locations:

- `action.yml:613`

### script-injection (severity: high)

(a) Step 'Update the Container Registry details on the existing Container App': `--server ${{ env.CA_GH_ACTION_REGISTRY_URL }} --username ${{ env.CA_GH_ACTION_REGISTRY_USERNAME }} --password ${{ env.CA_GH_ACTION_REGISTRY_PASSWORD }}`.

Locations:

- `action.yml:630`

### script-injection (severity: high)

(a) Step 'Update the existing Container App from provided arguments via update': `-n ${{ inputs.containerAppName }} -i ${{ env.CA_GH_ACTION_IMAGE_TO_DEPLOY }} ${{ env.CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT_VARIABLES_ARG }}`.

Locations:

- `action.yml:641`

### script-injection (severity: high)

(a) Step 'Reset the environment variables argument environment variable for the up command': `CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT_VARIABLES_ARG="--env-vars ${{ inputs.environmentVariables }}"`.

Locations:

- `action.yml:657`

### script-injection (severity: high)

(a) Step 'Update the existing Container App ... via up': `-n ${{ inputs.containerAppName }}` and several ${{ env.* }} argument expressions.

Locations:

- `action.yml:665`

### script-injection (severity: high)

(a) Step 'Disable ingress on the existing Container App': `-g ${{ env.CA_GH_ACTION_RESOURCE_GROUP }} -n ${{ inputs.containerAppName }}`.

Locations:

- `action.yml:678`

### script-injection (severity: high)

(a) Step 'End timer...': `CA_GH_ACTION_START_MILLISECONDS=${{ env.CA_GH_ACTION_START_MILLISECONDS }}`.

Locations:

- `action.yml:693`

### script-injection (severity: high)

(a) Step 'Log telemetry for action': `-c "oryx telemetry --event-name 'ContainerAppsGitHubAction' ${{ env.CA_GH_ACTION_LENGTH_MILLISECONDS_ARG }} ${{ env.CA_GH_ACTION_SCENARIO_ARG }} ${{ env.CA_GH_ACTION_RESULT_ARG }}"`. These are workflow-controllable env values placed inside a nested bash -c string.

Locations:

- `action.yml:726`

### github-env-injection (severity: high)

Step 'Export Container Registry information to environment variable' writes registry URL, username, password and login arg values built from inputs.registryUrl, inputs.registryUsername and inputs.registryPassword to $GITHUB_ENV without `printf '%s' | tr -d '\n\r'` sanitization.

Locations:

- `action.yml:216`

### github-env-injection (severity: high)

Step 'Export Azure Container Registry information...' writes values built from inputs.acrName, inputs.acrUsername and inputs.acrPassword to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:229`

### github-env-injection (severity: high)

Step 'Get access token...' writes `CA_GH_ACTION_REGISTRY_URL` (built from ${{ inputs.acrName }}) to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:242`

### github-env-injection (severity: high)

Step 'Export Dockerfile path to environment variable' writes a value built from inputs.appSourcePath and inputs.dockerfilePath to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:249`

### github-env-injection (severity: high)

Step 'Check for existing Dockerfile in application source' writes `CA_GH_ACTION_DOCKERFILE_PATH=${dockerfilePath}` (built from inputs.appSourcePath) to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:256`

### github-env-injection (severity: high)

Step 'Export name of image to build to environment variable' writes inputs.imageToBuild to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:263`

### github-env-injection (severity: high)

Step 'Determine name of image to build if not provided' writes a value built from env.CA_GH_ACTION_REGISTRY_URL to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:270`

### github-env-injection (severity: high)

Step 'Export name of image to deploy to environment variable' writes inputs.imageToDeploy to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:277`

### github-env-injection (severity: high)

Step 'Update name of image to deploy if not provided' writes env.CA_GH_ACTION_IMAGE_TO_BUILD to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:284`

### github-env-injection (severity: high)

Step 'Export resource group to environment variable' writes inputs.resourceGroup to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:291`

### github-env-injection (severity: high)

Step 'Determine resource group if not provided' writes a value built from inputs.containerAppName to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:298`

### github-env-injection (severity: high)

Step 'Set default location for Container Apps if location was provided' writes inputs.location to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:323`

### github-env-injection (severity: high)

Step 'Export location argument to environment variable' writes `--location ${{ inputs.location }}` to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:338`

### github-env-injection (severity: high)

Step 'Export environment to environment variable' writes inputs.containerAppEnvironment to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:354`

### github-env-injection (severity: high)

Step 'Determine environment name if not provided' writes a value built from inputs.containerAppName to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:361`

### github-env-injection (severity: high)

Step 'Export ingress value to environment variable' writes `--ingress ${{ inputs.ingress }}` to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:415`

### github-env-injection (severity: high)

Step 'Export target port to environment variable' writes inputs.targetPort to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:422`

### github-env-injection (severity: high)

Step 'Export target port information...' writes a value built from env.CA_GH_ACTION_TARGET_PORT to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:443`

### github-env-injection (severity: high)

Step 'Export environment variables argument ... does not exist' writes inputs.environmentVariables to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:450`

### github-env-injection (severity: high)

Step 'Export environment variables argument ... does exist' writes inputs.environmentVariables to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:457`

### github-env-injection (severity: high)

Step 'Parse the given runtime stack input...' writes platform and version values parsed from inputs.runtimeStack to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:505`

### github-env-injection (severity: high)

Step 'Set platform environment variables for builder invocation' writes values built from env.CA_GH_ACTION_RUNTIME_STACK_* to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:513`

### github-env-injection (severity: high)

Step 'Set port environment variable for builder invocation' writes a value built from the inherited ${CA_GH_ACTION_ORYX_BUILDER_ENV_ARG} and env.CA_GH_ACTION_TARGET_PORT to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:520`

### github-env-injection (severity: high)

Step 'Reset the environment variables argument environment variable for the up command' writes inputs.environmentVariables to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:658`

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

**Fixes applied:** unpinned-uses, script-injection, github-env-injection, static-inline-injection

**Notes:**

My first targeted edits left action.yml corrupted in two places, so I rewrote the whole file with write_file. A search afterwards found no leftover fragments. The fixes have not been run or tested.

- unpinned-uses: pinned azure/login to cb79c773a3cfa27f31f25eb3f677781210c9ce3d (# v1). Pinned both docker/login-action steps to 465a07811f14bebb1938fbed4728c6a1ff8901fc (# v2.2.0).
- script-injection / static-inline-injection: every ${{ inputs.* }} used in a run: script now goes through the step's env: block (INPUT_*) and is used as a double-quoted variable. ${{ env.CA_GH_ACTION_* }} references now read the shell variable directly, since values written to GITHUB_ENV are already there. runner.os, github.run_id and github.run_attempt became $RUNNER_OS, $GITHUB_RUN_ID and $GITHUB_RUN_ATTEMPT. The variables flagged as unquoted ($CA_GH_ACTION_ACR_ACCESS_TOKEN, $CA_GH_ACTION_TEMP_ENV_NAME and the default-location echo) are now quoted.
- Variables that hold a flag plus its value (ingress, target port, location, env vars, Oryx builder env, builder telemetry, the telemetry properties) are split into bash arrays with the quote-aware xargs pattern, which matches how the shell read them when they were pasted into the script. There is an empty-value guard, xargs -r, and a check that fails on an unmatched quote.
- The registry login flags are no longer split from the combined string. They are built from the separate URL/username/password variables, and the combined CA_GH_ACTION_REGISTRY_LOGIN_ARG is still written because the if: conditions check it.
- The telemetry docker run now passes its arguments as positional parameters (bash -c '... "$@"' bash "${args[@]}") instead of building a nested command string.
- github-env-injection: every value derived from an input is cleaned with printf '%s' | tr -d '\n\r' before it is written to GITHUB_ENV. For environmentVariables, newlines are turned into spaces first so a multi-line list keeps its separate entries.

Two behaviour points to check:
1. The JSON quotes in the az outputs for the default location and the reused environment name are now stripped explicitly. Before, the shell removed them when the value was pasted unquoted into later commands. Now that those values are quoted, the literal quotes would otherwise reach az.
2. Upstream's no-op dotnetcore comparison (it is missing a $) is left as it was.

