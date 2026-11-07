<!-- markdownlint-disable -->

# Hardening Report: Azure--container-apps-deploy-action/v0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **Azure--container-apps-deploy-action/v0** was hardened automatically. 107 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Two actions are referenced by tag instead of a 40-character commit SHA: 'uses: azure/login@v1' (line 162) and 'uses: docker/login-action@v2.0.0' (line 167).

Locations:

- `action.yml:162`
- `action.yml:167`

### github-env-injection (severity: high)

Step 'Export Azure Container Registry information...' writes inputs.acrName, inputs.acrUsername and inputs.acrPassword to $GITHUB_ENV without printf '%s' | tr -d '\n\r'.

Locations:

- `action.yml:179`

### github-env-injection (severity: high)

Step 'Export Dockerfile path to environment variable' writes inputs.appSourcePath and inputs.dockerfilePath to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:194`

### github-env-injection (severity: high)

Step 'Check for existing Dockerfile in application source' writes dockerfilePath, which comes from inputs.appSourcePath, to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:201`

### github-env-injection (severity: high)

Step 'Export name of image to build' writes inputs.imageToBuild to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:208`

### github-env-injection (severity: high)

Step 'Determine name of image to build if not provided' writes inputs.acrName and github.run_id to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:215`

### github-env-injection (severity: high)

Step 'Export name of image to deploy' writes inputs.imageToDeploy to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:222`

### github-env-injection (severity: high)

Step 'Update name of image to deploy if not provided' writes env.CA_GH_ACTION_IMAGE_TO_BUILD to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:229`

### github-env-injection (severity: high)

Step 'Export resource group' writes inputs.resourceGroup to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:236`

### github-env-injection (severity: high)

Step 'Determine resource group if not provided' writes inputs.containerAppName to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:243`

### github-env-injection (severity: high)

Step 'Set default location ... if location was provided' writes inputs.location to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:268`

### github-env-injection (severity: high)

Step 'Export location argument' writes inputs.location to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:283`

### github-env-injection (severity: high)

Step 'Export environment to environment variable' writes inputs.containerAppEnvironment to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:299`

### github-env-injection (severity: high)

Step 'Determine environment name if not provided' writes inputs.containerAppName to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:306`

### github-env-injection (severity: high)

Step 'Export runtime stack' writes inputs.runtimeStack to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:342`

### github-env-injection (severity: high)

Step 'Export ingress value' writes inputs.ingress to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:381`

### github-env-injection (severity: high)

Step 'Export target port' writes inputs.targetPort to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:388`

### github-env-injection (severity: high)

Step 'Export target port information ... for Azure CLI command' writes env.CA_GH_ACTION_TARGET_PORT to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:408`

### github-env-injection (severity: high)

Step 'Export environment variables argument ... does not exist' writes inputs.environmentVariables to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:415`

### github-env-injection (severity: high)

Step 'Export environment variables argument ... does exist' writes inputs.environmentVariables to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:422`

### github-env-injection (severity: high)

Step 'Reset the environment variables argument ... for the up command' writes inputs.environmentVariables to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:554`

### github-env-injection (severity: high)

Step 'Get access token to log in to Azure Container Registry' writes CA_GH_ACTION_ACR_ACCESS_TOKEN to $GITHUB_ENV without sanitization. The value comes from 'az acr login --name ${{ inputs.acrName }}'.

Locations:

- `action.yml:186`

### github-env-injection (severity: high)

Step 'Reuse an existing Container App environment' writes the az output (queried with env.CA_GH_ACTION_RESOURCE_GROUP) to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:324`

### github-env-injection (severity: high)

Step 'Determine runtime stack if not provided' writes content read from a file under inputs.appSourcePath to $GITHUB_ENV without sanitization.

Locations:

- `action.yml:355`

### script-injection (severity: high)

(a) The step puts inputs directly into run: 'CA_GH_ACTION_ACR_LOGIN_ARG="--registry-server ${{ inputs.acrName }}.azurecr.io --registry-username ${{ inputs.acrUsername }} --registry-password ${{ inputs.acrPassword }}"'.

Locations:

- `action.yml:178`

### script-injection (severity: high)

(a) 'az acr login --name ${{ inputs.acrName }} ...' and 'docker login ${{ inputs.acrName }}.azurecr.io ...' put inputs directly into run:. (b) $CA_GH_ACTION_ACR_ACCESS_TOKEN is unquoted.

Locations:

- `action.yml:185`
- `action.yml:187`

### script-injection (severity: high)

(a) 'CA_GH_ACTION_DOCKERFILE_PATH="${{ inputs.appSourcePath }}/${{ inputs.dockerfilePath }}"' puts inputs directly into run:.

Locations:

- `action.yml:193`

### script-injection (severity: high)

(a) 'dockerfilePath=${{ inputs.appSourcePath }}/Dockerfile' puts an input directly into run:, unquoted.

Locations:

- `action.yml:200`

### script-injection (severity: high)

(a) 'CA_GH_ACTION_IMAGE_TO_BUILD="${{ inputs.imageToBuild }}"' puts an input directly into run:.

Locations:

- `action.yml:207`

### script-injection (severity: high)

(a) 'CA_GH_ACTION_IMAGE_TO_BUILD="${{ inputs.acrName }}.azurecr.io/github-action/container-app:${{ github.run_id }}.${{ github.run_attempt }}"' puts expressions directly into run:.

Locations:

- `action.yml:214`

### script-injection (severity: high)

(a) 'CA_GH_ACTION_IMAGE_TO_DEPLOY="${{ inputs.imageToDeploy }}"' puts an input directly into run:.

Locations:

- `action.yml:221`

### script-injection (severity: high)

(a) 'CA_GH_ACTION_IMAGE_TO_DEPLOY="${{ env.CA_GH_ACTION_IMAGE_TO_BUILD }}"' puts an expression directly into run:.

Locations:

- `action.yml:228`

### script-injection (severity: high)

(a) 'CA_GH_ACTION_RESOURCE_GROUP="${{ inputs.resourceGroup }}"' puts an input directly into run:.

Locations:

- `action.yml:235`

### script-injection (severity: high)

(a) 'CA_GH_ACTION_RESOURCE_GROUP="${{ inputs.containerAppName }}-rg"' puts an input directly into run:.

Locations:

- `action.yml:242`

### script-injection (severity: high)

(a) '-n ${{ env.CA_GH_ACTION_RESOURCE_GROUP }}' in az group show puts an expression directly into run:.

Locations:

- `action.yml:250`

### script-injection (severity: high)

(a) 'CA_GH_ACTION_DEFAULT_LOCATION="${{ inputs.location }}"' puts an input directly into run:.

Locations:

- `action.yml:267`

### script-injection (severity: high)

(a) '-n ${{ env.CA_GH_ACTION_RESOURCE_GROUP }}' and '-l ${{ env.CA_GH_ACTION_DEFAULT_LOCATION }}' in az group create put expressions directly into run:.

Locations:

- `action.yml:275`

### script-injection (severity: high)

(a) 'CA_GH_ACTION_CONTAINER_APP_LOCATION_ARG="--location ${{ inputs.location }}"' puts an input directly into run:.

Locations:

- `action.yml:282`

### script-injection (severity: high)

(a) az containerapp show puts '-g ${{ env.CA_GH_ACTION_RESOURCE_GROUP }}' and '-n ${{ inputs.containerAppName }}' directly into run:.

Locations:

- `action.yml:289`

### script-injection (severity: high)

(a) 'CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT="${{ inputs.containerAppEnvironment }}"' puts an input directly into run:.

Locations:

- `action.yml:298`

### script-injection (severity: high)

(a) 'CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT="${{ inputs.containerAppName }}-env"' puts an input directly into run:.

Locations:

- `action.yml:305`

### script-injection (severity: high)

(a) az containerapp env show puts '-g ${{ env.CA_GH_ACTION_RESOURCE_GROUP }}' and '-n ${{ env.CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT }}' directly into run:.

Locations:

- `action.yml:313`

### script-injection (severity: high)

(a) 'az containerapp env list -g ${{ env.CA_GH_ACTION_RESOURCE_GROUP }}' puts an expression directly into run:. (b) $CA_GH_ACTION_TEMP_ENV_NAME is unquoted.

Locations:

- `action.yml:322`

### script-injection (severity: high)

(a) az containerapp env create puts '${{ env.CA_GH_ACTION_RESOURCE_GROUP }}', '${{ env.CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT }}' and '${{ env.CA_GH_ACTION_CONTAINER_APP_LOCATION_ARG }}' directly into run:.

Locations:

- `action.yml:333`

### script-injection (severity: high)

(a) 'CA_GH_ACTION_RUNTIME_STACK="${{ inputs.runtimeStack }}"' puts an input directly into run:.

Locations:

- `action.yml:341`

### script-injection (severity: high)

(a) '-v ${{ inputs.appSourcePath }}:/app', 'head -n 1 ${{ inputs.appSourcePath }}/oryx-runtime.txt' and 'rm ${{ inputs.appSourcePath }}/oryx-runtime.txt' put an input directly into run:.

Locations:

- `action.yml:350`
- `action.yml:354`
- `action.yml:356`

### script-injection (severity: high)

(a) 'CA_GH_ACTION_INGRESS_ARG="--ingress ${{ inputs.ingress }}"' puts an input directly into run:.

Locations:

- `action.yml:380`

### script-injection (severity: high)

(a) 'CA_GH_ACTION_TARGET_PORT="${{ inputs.targetPort }}"' puts an input directly into run:.

Locations:

- `action.yml:387`

### script-injection (severity: high)

(a) 'if [[ "${{ env.CA_GH_ACTION_RUNTIME_STACK }}" == "python:"* ]]' puts an expression directly into run:.

Locations:

- `action.yml:394`

### script-injection (severity: high)

(a) 'CA_GH_ACTION_TARGET_PORT_ARG="--target-port ${{ env.CA_GH_ACTION_TARGET_PORT }}"' puts an expression directly into run:.

Locations:

- `action.yml:407`

### script-injection (severity: high)

(a) 'CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT_VARIABLES_ARG="--env-vars ${{ inputs.environmentVariables }}"' puts an input directly into run:.

Locations:

- `action.yml:414`

### script-injection (severity: high)

(a) 'CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT_VARIABLES_ARG="--replace-env-vars ${{ inputs.environmentVariables }}"' puts an input directly into run:.

Locations:

- `action.yml:421`

### script-injection (severity: high)

(a) The curl URL '.../pack-v0.27.0-${{ runner.os }}.tgz' puts a runner.os expression directly into run:.

Locations:

- `action.yml:427`

### script-injection (severity: high)

(a) pack build puts '${{ env.CA_GH_ACTION_IMAGE_TO_DEPLOY }}', '--path ${{ inputs.appSourcePath }}', '${{ env.CA_GH_ACTION_RUNTIME_STACK }}' and '${{ env.CA_GH_ACTION_ORYX_BUILDER_TELEMETRY_ARG }}' directly into run:.

Locations:

- `action.yml:462`

### script-injection (severity: high)

(a) docker build puts '--tag ${{ env.CA_GH_ACTION_IMAGE_TO_DEPLOY }}', '--file ${{ env.CA_GH_ACTION_DOCKERFILE_PATH }}' and '${{ inputs.appSourcePath }}' directly into run:.

Locations:

- `action.yml:473`

### script-injection (severity: high)

(a) 'docker push ${{ env.CA_GH_ACTION_IMAGE_TO_DEPLOY }}' puts an expression directly into run:.

Locations:

- `action.yml:480`

### script-injection (severity: high)

(a) az containerapp create (YAML) puts '${{ env.CA_GH_ACTION_RESOURCE_GROUP }}', '${{ inputs.containerAppName }}' and '--yaml ${{ inputs.yamlConfigPath }}' directly into run:.

Locations:

- `action.yml:487`

### script-injection (severity: high)

(a) az containerapp create (arguments) puts many expressions directly into run:, for example '-n ${{ inputs.containerAppName }}', '-i ${{ env.CA_GH_ACTION_IMAGE_TO_DEPLOY }}' and '${{ env.CA_GH_ACTION_ACR_LOGIN_ARG }}'.

Locations:

- `action.yml:496`

### script-injection (severity: high)

(a) az containerapp update (YAML) puts '${{ env.CA_GH_ACTION_RESOURCE_GROUP }}', '${{ inputs.containerAppName }}' and '--yaml ${{ inputs.yamlConfigPath }}' directly into run:.

Locations:

- `action.yml:510`

### script-injection (severity: high)

(a) az containerapp registry set puts '--server ${{ inputs.acrName }}.azurecr.io', '--username ${{ inputs.acrUsername }}' and '--password ${{ inputs.acrPassword }}' directly into run:.

Locations:

- `action.yml:526`

### script-injection (severity: high)

(a) az containerapp update puts '${{ env.CA_GH_ACTION_RESOURCE_GROUP }}', '${{ inputs.containerAppName }}', '${{ env.CA_GH_ACTION_IMAGE_TO_DEPLOY }}' and '${{ env.CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT_VARIABLES_ARG }}' directly into run:.

Locations:

- `action.yml:537`

### script-injection (severity: high)

(a) 'CA_GH_ACTION_CONTAINER_APP_ENVIRONMENT_VARIABLES_ARG="--env-vars ${{ inputs.environmentVariables }}"' (reset for up) puts an input directly into run:.

Locations:

- `action.yml:553`

### script-injection (severity: high)

(a) az containerapp up puts many expressions directly into run:, for example '${{ inputs.containerAppName }}', '${{ env.CA_GH_ACTION_IMAGE_TO_DEPLOY }}' and '${{ env.CA_GH_ACTION_ACR_LOGIN_ARG }}'.

Locations:

- `action.yml:561`

### script-injection (severity: high)

(a) az containerapp ingress disable puts '-g ${{ env.CA_GH_ACTION_RESOURCE_GROUP }}' and '-n ${{ inputs.containerAppName }}' directly into run:.

Locations:

- `action.yml:574`

### script-injection (severity: high)

(a) 'CA_GH_ACTION_START_MILLISECONDS=${{ env.CA_GH_ACTION_START_MILLISECONDS }}' puts an expression directly into run:.

Locations:

- `action.yml:589`

### script-injection (severity: high)

(a) In 'Log telemetry for action', the line '-c "oryx telemetry ... ${{ env.CA_GH_ACTION_LENGTH_MILLISECONDS_ARG }} ${{ env.CA_GH_ACTION_SCENARIO_ARG }} ${{ env.CA_GH_ACTION_RESULT_ARG }}"' puts expressions directly into run:.

Locations:

- `action.yml:622`

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

**Fixes applied:** unpinned-uses, github-env-injection, script-injection, static-inline-injection

**Notes:**

All changes are in action.yml. Nothing was run or tested; I checked the edits by re-reading the file and searching it.

- **unpinned-uses:** azure/login@v1 is now pinned to cb79c773a3cfa27f31f25eb3f677781210c9ce3d and docker/login-action@v2.0.0 to 49ed152c8eca782a232dede0303416e8f356c37b, each with a `# tag` comment.
- **script-injection / static-inline-injection:** every `${{ inputs.* }}`, `${{ github.run_id/run_attempt }}` and `${{ runner.os }}` used in a run: block now goes through the step's env: block (INPUT_* / GH_* vars) or uses the runner's built-in variable (RUNNER_OS). Every `${{ env.CA_GH_ACTION_* }}` became a direct reference to the variable, which GITHUB_ENV has already set. Single values are double-quoted.
- **Combined flag strings** (the stored ACR login, ingress, target port, env-vars, location, Oryx telemetry and telemetry-property values): upstream pasted these in unquoted, so the shell split them and honoured quotes inside them. To keep that behaviour, each step now splits them into an array with the guarded `xargs -r` method, so a flag and its value stay separate arguments.
- **Final telemetry step:** it now passes the split arguments to `bash -c 'oryx telemetry ... "$@"'` instead of building the command text by string interpolation.
- **github-env-injection:** every value written to GITHUB_ENV from an input or command output now goes through `printf '%s' | tr -d '\n\r'`, and `$GITHUB_ENV` is quoted.
- **Two small behaviour-preserving changes:** the default location from az and the reused Container App environment name now have their JSON double quotes stripped before being saved. Upstream relied on the shell removing those quotes when it pasted the value in unquoted.
- **Tradeoff:** an environmentVariables input written over several lines now has its line breaks removed, so the last pair on one line runs into the first pair on the next (for example `A=1` and `B=2` become `A=1B=2`). Upstream would have written a broken GITHUB_ENV entry in that case anyway.

