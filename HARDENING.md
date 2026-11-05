<!-- markdownlint-disable -->

# Hardening Report: Azure--container-apps-deploy-action/v0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **Azure--container-apps-deploy-action/v0** was hardened automatically. 101 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

action.yml has composite-action steps whose uses: refs are tags, not 40-character commit SHAs: `uses: azure/login@v1` and `uses: docker/login-action@v2.0.0`.

Locations:

- `action.yml:165`
- `action.yml:170`

### script-injection (severity: high)

Sub-rule (a), step 'Export Azure Container Registry information...'. The run: script puts expressions straight into the shell: `CA_GH_ACTION_ACR_LOGIN_ARG="--registry-server ${{ inputs.acrName }}.azurecr.io --registry-username ${{ inputs.acrUsername }} --registry-password ${{ inputs.acrPassword }}"`.

Locations:

- `action.yml:181`

### script-injection (severity: high)

Sub-rule (a), step 'Get access token to log in to Azure Container Registry'. The script contains `az acr login --name ${{ inputs.acrName }} ...` and `docker login ${{ inputs.acrName }}.azurecr.io ... -p $CA_GH_ACTION_ACR_ACCESS_TOKEN`, and the token variable is not quoted.

Locations:

- `action.yml:188`
- `action.yml:190`

### script-injection (severity: high)

Sub-rule (a), step 'Export Dockerfile path to environment variable'. The script contains `CA_GH_ACTION_DOCKERFILE_PATH="${{ inputs.appSourcePath }}/${{ inputs.dockerfilePath }}"`.

Locations:

- `action.yml:196`

### script-injection (severity: high)

Sub-rule (a), step 'Check for existing Dockerfile in application source'. The script contains `dockerfilePath=${{ inputs.appSourcePath }}/Dockerfile`, with no quoting.

Locations:

- `action.yml:203`

### script-injection (severity: high)

Sub-rule (a), step 'Export name of image to build'. The script contains `CA_GH_ACTION_IMAGE_TO_BUILD="${{ inputs.imageToBuild }}"`.

Locations:

- `action.yml:210`

### script-injection (severity: high)

Sub-rule (a), step 'Determine name of image to build if not provided'. The script contains `CA_GH_ACTION_IMAGE_TO_BUILD="${{ inputs.acrName }}.azurecr.io/github-action/container-app:${{ github.run_id }}.${{ github.run_attempt }}"`.

Locations:

- `action.yml:217`

### script-injection (severity: high)

Sub-rule (a), step 'Export name of image to deploy'. The script contains `CA_GH_ACTION_IMAGE_TO_DEPLOY="${{ inputs.imageToDeploy }}"`.

Locations:

- `action.yml:224`

### script-injection (severity: high)

Sub-rule (a), step 'Update name of image to deploy if not provided'. The script contains `CA_GH_ACTION_IMAGE_TO_DEPLOY="${{ env.CA_GH_ACTION_IMAGE_TO_BUILD }}"`.

Locations:

- `action.yml:231`

### script-injection (severity: high)

Sub-rule (a), step 'Export resource group'. The script contains `CA_GH_ACTION_RESOURCE_GROUP="${{ inputs.resourceGroup }}"`.

Locations:

- `action.yml:238`

### script-injection (severity: high)

Sub-rule (a), step 'Determine resource group if not provided'. The script contains `CA_GH_ACTION_RESOURCE_GROUP="${{ inputs.containerAppName }}-rg"`.

Locations:

- `action.yml:245`

### script-injection (severity: high)

Sub-rule (a), step 'Check if the previously generated resource group exists'. The script contains `-n ${{ env.CA_GH_ACTION_RESOURCE_GROUP }}`.

Locations:

- `action.yml:253`

### script-injection (severity: high)

Sub-rule (a), step 'Set default location for Container Apps if location was provided'. The script contains `CA_GH_ACTION_DEFAULT_LOCATION="${{ inputs.location }}"`.

Locations:

- `action.yml:270`

### script-injection (severity: high)

Sub-rule (a), step 'Create resource group if it doesn't exist'. The script contains `-n ${{ env.CA_GH_ACTION_RESOURCE_GROUP }}` and `-l ${{ env.CA_GH_ACTION_DEFAULT_LOCATION }}`.

Locations:

- `action.yml:278`

### script-injection (severity: high)

Sub-rule (a), step 'Export location argument'. The script contains `CA_GH_ACTION_CONTAINER_APP_LOCATION_ARG="--location ${{ inputs.location }}"`.

Locations:

- `action.yml:285`

### script-injection (severity: high)

Sub-rule (a), step 'Check if the Container App already exists'. The script contains `-g ${{ env.CA_GH_ACTION_RESOURCE_GROUP }}` and `-n ${{ inputs.containerAppName }}`.

Locations:

- `action.yml:292`

### script-injection (severity: high)

Sub-rule (a), step 'Export environment to environment variable'. The script contains `CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT="${{ inputs.containerAppEnvironment }}"`.

Locations:

- `action.yml:301`

### script-injection (severity: high)

Sub-rule (a), step 'Determine environment name if not provided'. The script contains `CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT="${{ inputs.containerAppName }}-env"`.

Locations:

- `action.yml:308`

### script-injection (severity: high)

Sub-rule (a), step 'Check if Container App environment already exists'. The script contains `-g ${{ env.CA_GH_ACTION_RESOURCE_GROUP }}` and `-n ${{ env.CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT }}`.

Locations:

- `action.yml:316`

### script-injection (severity: high)

Sub-rules (a) and (b), step 'Reuse an existing Container App environment'. The script contains `az containerapp env list -g ${{ env.CA_GH_ACTION_RESOURCE_GROUP }}`, and `$CA_GH_ACTION_TEMP_ENV_NAME` is expanded without quotes.

Locations:

- `action.yml:325`

### script-injection (severity: high)

Sub-rule (a), step 'Create Container App environment'. The script contains `-g ${{ env.CA_GH_ACTION_RESOURCE_GROUP }}`, `-n ${{ env.CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT }}` and `${{ env.CA_GH_ACTION_CONTAINER_APP_LOCATION_ARG }}`.

Locations:

- `action.yml:336`

### script-injection (severity: high)

Sub-rule (a), step 'Export runtime stack'. The script contains `CA_GH_ACTION_RUNTIME_STACK="${{ inputs.runtimeStack }}"`.

Locations:

- `action.yml:344`

### script-injection (severity: high)

Sub-rule (a), step 'Determine runtime stack if not provided'. The script contains `-v ${{ inputs.appSourcePath }}:/app`, `head -n 1 ${{ inputs.appSourcePath }}/oryx-runtime.txt` and `rm ${{ inputs.appSourcePath }}/oryx-runtime.txt`.

Locations:

- `action.yml:353`
- `action.yml:357`
- `action.yml:359`

### script-injection (severity: high)

Sub-rule (a), step 'Export ingress value'. The script contains `CA_GH_ACTION_INGRESS_ARG="--ingress ${{ inputs.ingress }}"`.

Locations:

- `action.yml:383`

### script-injection (severity: high)

Sub-rule (a), step 'Export target port'. The script contains `CA_GH_ACTION_TARGET_PORT="${{ inputs.targetPort }}"`.

Locations:

- `action.yml:390`

### script-injection (severity: high)

Sub-rule (a), step 'Determine default target port'. The script contains `if [[ "${{ env.CA_GH_ACTION_RUNTIME_STACK }}" == "python:"* ]]`.

Locations:

- `action.yml:397`

### script-injection (severity: high)

Sub-rule (a), step 'Export target port information'. The script contains `CA_GH_ACTION_TARGET_PORT_ARG="--target-port ${{ env.CA_GH_ACTION_TARGET_PORT }}"`.

Locations:

- `action.yml:410`

### script-injection (severity: high)

Sub-rule (a), steps 'Export environment variables argument...' (two steps) and 'Reset the environment variables argument...'. The scripts contain `--env-vars ${{ inputs.environmentVariables }}` and `--replace-env-vars ${{ inputs.environmentVariables }}`.

Locations:

- `action.yml:417`
- `action.yml:424`
- `action.yml:556`

### script-injection (severity: high)

Sub-rule (a), step 'Install pack CLI on non-Windows runner'. The script contains `curl -sSL "https://github.com/buildpacks/pack/releases/download/v0.27.0/pack-v0.27.0-${{ runner.os }}.tgz"`.

Locations:

- `action.yml:430`

### script-injection (severity: high)

Sub-rule (a), step 'Create runnable application image using Oryx++ Builder'. The script contains `${{ env.CA_GH_ACTION_IMAGE_TO_DEPLOY }}`, `--path ${{ inputs.appSourcePath }}`, `mcr.microsoft.com/oryx/${{ env.CA_GH_ACTION_RUNTIME_STACK }}` and `${{ env.CA_GH_ACTION_ORYX_BUILDER_TELEMETRY_ARG }}`.

Locations:

- `action.yml:465`

### script-injection (severity: high)

Sub-rule (a), step 'Create runnable application image using provided Dockerfile'. The script contains `--tag ${{ env.CA_GH_ACTION_IMAGE_TO_DEPLOY }}`, `--file ${{ env.CA_GH_ACTION_DOCKERFILE_PATH }}` and `${{ inputs.appSourcePath }}`.

Locations:

- `action.yml:476`

### script-injection (severity: high)

Sub-rule (a), step 'Push image to Azure Container Registry'. The script contains `docker push ${{ env.CA_GH_ACTION_IMAGE_TO_DEPLOY }}`.

Locations:

- `action.yml:483`

### script-injection (severity: high)

Sub-rule (a), step 'Create the Container App from a YAML configuration file'. The script contains `-g ${{ env.CA_GH_ACTION_RESOURCE_GROUP }}`, `-n ${{ inputs.containerAppName }}` and `--yaml ${{ inputs.yamlConfigPath }}`.

Locations:

- `action.yml:490`

### script-injection (severity: high)

Sub-rule (a), step 'Create the Container App from provided arguments'. The script contains `-n ${{ inputs.containerAppName }}`, `-i ${{ env.CA_GH_ACTION_IMAGE_TO_DEPLOY }}`, `${{ env.CA_GH_ACTION_ACR_LOGIN_ARG }}`, `${{ env.CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT_VARIABLES_ARG }}` and other env expressions.

Locations:

- `action.yml:499`

### script-injection (severity: high)

Sub-rule (a), step 'Update the existing Container App from a YAML configuration file'. The script contains `-n ${{ inputs.containerAppName }}` and `--yaml ${{ inputs.yamlConfigPath }}`.

Locations:

- `action.yml:513`

### script-injection (severity: high)

Sub-rule (a), step 'Update the Container Registry details'. The script contains `--server ${{ inputs.acrName }}.azurecr.io`, `--username ${{ inputs.acrUsername }}` and `--password ${{ inputs.acrPassword }}`.

Locations:

- `action.yml:529`

### script-injection (severity: high)

Sub-rule (a), step 'Update the existing Container App ... via update'. The script contains `-n ${{ inputs.containerAppName }}`, `-i ${{ env.CA_GH_ACTION_IMAGE_TO_DEPLOY }}` and `${{ env.CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT_VARIABLES_ARG }}`.

Locations:

- `action.yml:540`

### script-injection (severity: high)

Sub-rule (a), step 'Update the existing Container App ... via up'. The script contains `-n ${{ inputs.containerAppName }}`, `${{ env.CA_GH_ACTION_INGRESS_ARG }}`, `${{ env.CA_GH_ACTION_ACR_LOGIN_ARG }}` and other env expressions.

Locations:

- `action.yml:564`

### script-injection (severity: high)

Sub-rule (a), step 'Disable ingress on the existing Container App'. The script contains `-g ${{ env.CA_GH_ACTION_RESOURCE_GROUP }}` and `-n ${{ inputs.containerAppName }}`.

Locations:

- `action.yml:577`

### script-injection (severity: high)

Sub-rule (a), step 'End timer'. The script contains `CA_GH_ACTION_START_MILLISECONDS=${{ env.CA_GH_ACTION_START_MILLISECONDS }}`, which is unquoted and later used in arithmetic expansion.

Locations:

- `action.yml:592`

### script-injection (severity: high)

Sub-rule (a), step 'Log telemetry for action'. The script contains `-c "oryx telemetry --event-name 'ContainerAppsGitHubAction' ${{ env.CA_GH_ACTION_LENGTH_MILLISECONDS_ARG }} ${{ env.CA_GH_ACTION_SCENARIO_ARG }} ${{ env.CA_GH_ACTION_RESULT_ARG }}"`.

Locations:

- `action.yml:625`

### github-env-injection (severity: high)

Step 'Export Azure Container Registry information' writes CA_GH_ACTION_ACR_LOGIN_ARG to $GITHUB_ENV without running `printf '%s' | tr -d '\n\r'` first. The value is built from inputs.acrName, inputs.acrUsername and inputs.acrPassword.

Locations:

- `action.yml:182`

### github-env-injection (severity: high)

Step 'Export Dockerfile path' writes CA_GH_ACTION_DOCKERFILE_PATH, built from inputs.appSourcePath and inputs.dockerfilePath, to $GITHUB_ENV without sanitizing it.

Locations:

- `action.yml:197`

### github-env-injection (severity: high)

Step 'Check for existing Dockerfile' writes dockerfilePath, built from inputs.appSourcePath, to $GITHUB_ENV without sanitizing it.

Locations:

- `action.yml:204`

### github-env-injection (severity: high)

Step 'Export name of image to build' writes CA_GH_ACTION_IMAGE_TO_BUILD, taken from inputs.imageToBuild, to $GITHUB_ENV without sanitizing it.

Locations:

- `action.yml:211`

### github-env-injection (severity: high)

Step 'Determine name of image to build' writes CA_GH_ACTION_IMAGE_TO_BUILD, built from inputs.acrName, to $GITHUB_ENV without sanitizing it.

Locations:

- `action.yml:218`

### github-env-injection (severity: high)

Step 'Export name of image to deploy' writes CA_GH_ACTION_IMAGE_TO_DEPLOY, taken from inputs.imageToDeploy, to $GITHUB_ENV without sanitizing it.

Locations:

- `action.yml:225`

### github-env-injection (severity: high)

Step 'Update name of image to deploy' writes CA_GH_ACTION_IMAGE_TO_DEPLOY, taken from env.CA_GH_ACTION_IMAGE_TO_BUILD, to $GITHUB_ENV without sanitizing it.

Locations:

- `action.yml:232`

### github-env-injection (severity: high)

Step 'Export resource group' writes CA_GH_ACTION_RESOURCE_GROUP, taken from inputs.resourceGroup, to $GITHUB_ENV without sanitizing it.

Locations:

- `action.yml:239`

### github-env-injection (severity: high)

Step 'Determine resource group' writes CA_GH_ACTION_RESOURCE_GROUP, built from inputs.containerAppName, to $GITHUB_ENV without sanitizing it.

Locations:

- `action.yml:246`

### github-env-injection (severity: high)

Step 'Set default location' writes CA_GH_ACTION_DEFAULT_LOCATION, taken from inputs.location, to $GITHUB_ENV without sanitizing it.

Locations:

- `action.yml:271`

### github-env-injection (severity: high)

Step 'Export location argument' writes CA_GH_ACTION_CONTAINER_APP_LOCATION_ARG, built from inputs.location, to $GITHUB_ENV without sanitizing it.

Locations:

- `action.yml:286`

### github-env-injection (severity: high)

Step 'Export environment' writes CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT, taken from inputs.containerAppEnvironment, to $GITHUB_ENV without sanitizing it.

Locations:

- `action.yml:302`

### github-env-injection (severity: high)

Step 'Determine environment name' writes CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT, built from inputs.containerAppName, to $GITHUB_ENV without sanitizing it.

Locations:

- `action.yml:309`

### github-env-injection (severity: high)

Step 'Export runtime stack' writes CA_GH_ACTION_RUNTIME_STACK, taken from inputs.runtimeStack, to $GITHUB_ENV without sanitizing it.

Locations:

- `action.yml:345`

### github-env-injection (severity: high)

Step 'Export ingress value' writes CA_GH_ACTION_INGRESS_ARG, built from inputs.ingress, to $GITHUB_ENV without sanitizing it.

Locations:

- `action.yml:384`

### github-env-injection (severity: high)

Step 'Export target port' writes CA_GH_ACTION_TARGET_PORT, taken from inputs.targetPort, to $GITHUB_ENV without sanitizing it.

Locations:

- `action.yml:391`

### github-env-injection (severity: high)

Step 'Export target port information' writes CA_GH_ACTION_TARGET_PORT_ARG, built from env.CA_GH_ACTION_TARGET_PORT, to $GITHUB_ENV without sanitizing it.

Locations:

- `action.yml:411`

### github-env-injection (severity: high)

Three steps write CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT_VARIABLES_ARG, built from inputs.environmentVariables, to $GITHUB_ENV without sanitizing it: the two 'Export environment variables argument...' steps and 'Reset the environment variables argument...'.

Locations:

- `action.yml:418`
- `action.yml:425`
- `action.yml:557`

### github-env-injection (severity: high)

Step 'End timer' writes CA_GH_ACTION_LENGTH_MILLISECONDS_ARG to $GITHUB_ENV without sanitizing it. The value is computed from env.CA_GH_ACTION_START_MILLISECONDS, an env value controlled by the calling workflow.

Locations:

- `action.yml:594`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.acrName }}" appears directly in run: block of step "Export Azure Container Registry information to environment variable for Azure CLI command"; move to env: map

Locations:

- `action.yml:181`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.acrUsername }}" appears directly in run: block of step "Export Azure Container Registry information to environment variable for Azure CLI command"; move to env: map

Locations:

- `action.yml:181`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.acrPassword }}" appears directly in run: block of step "Export Azure Container Registry information to environment variable for Azure CLI command"; move to env: map

Locations:

- `action.yml:181`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.acrName }}" appears directly in run: block of step "Get access token to log in to Azure Container Registry"; move to env: map

Locations:

- `action.yml:188`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.acrName }}" appears directly in run: block of step "Get access token to log in to Azure Container Registry"; move to env: map

Locations:

- `action.yml:190`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.appSourcePath }}" appears directly in run: block of step "Export Dockerfile path to environment variable"; move to env: map

Locations:

- `action.yml:196`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.dockerfilePath }}" appears directly in run: block of step "Export Dockerfile path to environment variable"; move to env: map

Locations:

- `action.yml:196`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.appSourcePath }}" appears directly in run: block of step "Check for existing Dockerfile in application source"; move to env: map

Locations:

- `action.yml:203`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.imageToBuild }}" appears directly in run: block of step "Export name of image to build to environment variable"; move to env: map

Locations:

- `action.yml:210`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.acrName }}" appears directly in run: block of step "Determine name of image to build if not provided"; move to env: map

Locations:

- `action.yml:217`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.imageToDeploy }}" appears directly in run: block of step "Export name of image to deploy to environment variable"; move to env: map

Locations:

- `action.yml:224`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.resourceGroup }}" appears directly in run: block of step "Export resource group to environment variable"; move to env: map

Locations:

- `action.yml:238`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.containerAppName }}" appears directly in run: block of step "Determine resource group if not provided"; move to env: map

Locations:

- `action.yml:245`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.location }}" appears directly in run: block of step "Set default location for Container Apps if location was provided"; move to env: map

Locations:

- `action.yml:270`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.location }}" appears directly in run: block of step "Export location argument to environment variable"; move to env: map

Locations:

- `action.yml:285`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.containerAppName }}" appears directly in run: block of step "Check if the Container App already exists in the resource group"; move to env: map

Locations:

- `action.yml:293`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.containerAppEnvironment }}" appears directly in run: block of step "Export environment to environment variable"; move to env: map

Locations:

- `action.yml:301`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.containerAppName }}" appears directly in run: block of step "Determine environment name if not provided"; move to env: map

Locations:

- `action.yml:308`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.runtimeStack }}" appears directly in run: block of step "Export runtime stack to environment variable"; move to env: map

Locations:

- `action.yml:344`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.appSourcePath }}" appears directly in run: block of step "Determine runtime stack if not provided"; move to env: map

Locations:

- `action.yml:353`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.appSourcePath }}" appears directly in run: block of step "Determine runtime stack if not provided"; move to env: map

Locations:

- `action.yml:357`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.appSourcePath }}" appears directly in run: block of step "Determine runtime stack if not provided"; move to env: map

Locations:

- `action.yml:359`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.ingress }}" appears directly in run: block of step "Export ingress value to environment variable"; move to env: map

Locations:

- `action.yml:383`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.targetPort }}" appears directly in run: block of step "Export target port to environment variable"; move to env: map

Locations:

- `action.yml:390`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.environmentVariables }}" appears directly in run: block of step "Export environment variables argument to environment variable if the Container App does not exist"; move to env: map

Locations:

- `action.yml:417`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.environmentVariables }}" appears directly in run: block of step "Export environment variables argument to environment variable if the Container App does exist"; move to env: map

Locations:

- `action.yml:424`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.appSourcePath }}" appears directly in run: block of step "Create runnable application image using Oryx++ Builder"; move to env: map

Locations:

- `action.yml:466`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.appSourcePath }}" appears directly in run: block of step "Create runnable application image using provided Dockerfile"; move to env: map

Locations:

- `action.yml:478`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.containerAppName }}" appears directly in run: block of step "Create the Container App from a YAML configuration file"; move to env: map

Locations:

- `action.yml:491`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.yamlConfigPath }}" appears directly in run: block of step "Create the Container App from a YAML configuration file"; move to env: map

Locations:

- `action.yml:492`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.containerAppName }}" appears directly in run: block of step "Create the Container App from provided arguments"; move to env: map

Locations:

- `action.yml:500`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.containerAppName }}" appears directly in run: block of step "Update the existing Container App from a YAML configuration file"; move to env: map

Locations:

- `action.yml:514`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.yamlConfigPath }}" appears directly in run: block of step "Update the existing Container App from a YAML configuration file"; move to env: map

Locations:

- `action.yml:515`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.containerAppName }}" appears directly in run: block of step "Update the Container Registry details on the existing Container App"; move to env: map

Locations:

- `action.yml:530`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.acrName }}" appears directly in run: block of step "Update the Container Registry details on the existing Container App"; move to env: map

Locations:

- `action.yml:531`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.acrUsername }}" appears directly in run: block of step "Update the Container Registry details on the existing Container App"; move to env: map

Locations:

- `action.yml:532`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.acrPassword }}" appears directly in run: block of step "Update the Container Registry details on the existing Container App"; move to env: map

Locations:

- `action.yml:533`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.containerAppName }}" appears directly in run: block of step "Update the existing Container App from provided arguments via 'update' (no ingress values provided)"; move to env: map

Locations:

- `action.yml:541`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.environmentVariables }}" appears directly in run: block of step "Reset the environment variables argument environment variable for the 'up' command"; move to env: map

Locations:

- `action.yml:556`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.containerAppName }}" appears directly in run: block of step "Update the existing Container App from provided arguments via 'up' (ingress values provided)"; move to env: map

Locations:

- `action.yml:565`

### static-inline-injection (severity: high)

shell injection: expression "${{ inputs.containerAppName }}" appears directly in run: block of step "Disable ingress on the existing Container App"; move to env: map

Locations:

- `action.yml:578`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, script-injection, github-env-injection, static-inline-injection

**Notes:**

Changes to action.yml. Nothing has been run yet, so none of it is tested:

- **Pinned actions:** azure/login@cb79c773a3cfa27f31f25eb3f677781210c9ce3d # v1 and docker/login-action@49ed152c8eca782a232dede0303416e8f356c37b # v2.0.0.
- **Inputs moved out of scripts:** every input expression in a run: script now goes through the step's env: block and is double-quoted where it expands. Values the action had already written to $GITHUB_ENV are read as shell variables instead of being pasted in with ${{ env.X }}. github.run_id, run_attempt and runner.os are read from GITHUB_RUN_ID, GITHUB_RUN_ATTEMPT and RUNNER_OS.
- **Values written to $GITHUB_ENV:** anything built from an input or from command output (az, jq, the oryx runtime file) has newlines stripped with `printf '%s' ... | tr -d '\n\r'` before it is written.
- **Registry credentials:** CA_GH_ACTION_ACR_LOGIN_ARG now only holds the marker 'true', so the ACR password is no longer stored in $GITHUB_ENV. The create, up and registry-set steps build the `--registry-*` arguments as an array straight from the inputs.
- **docker login:** the access token is now passed with `--password-stdin` instead of an unquoted `-p`.
- **Combined argument strings** (ingress, target port, env vars): these are split into an array with the quote-aware xargs method (empty-value guard, `xargs -r true` check for unmatched quotes), because upstream pasted them straight into the script. Location and telemetry arguments use a plain whitespace split with `read -d ''`.
- **Fixed telemetry values:** I removed their inner quotes (for example `--env CALLER_ID=github-actions-v0` and `--property result=failed`), so the whitespace split gives the same arguments the shell used to.
- **Telemetry container:** the oryx telemetry call now passes its arguments as "$@" instead of building a command string for the container's shell.
- **End timer:** CA_GH_ACTION_START_MILLISECONDS is checked to be digits only before the arithmetic. If it isn't, the duration is reported as 0.

Two side effects of no longer pasting values into the script, both handled by changing the az calls:
- Upstream relied on the shell removing the JSON quotes from az output. The environment lookup now uses `-o tsv`, and the default-location sed also strips `"`. Without this, environment and location names would reach later commands wrapped in literal quotes.

