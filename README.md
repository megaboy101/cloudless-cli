Project Deliverables:
- Account creation
- Account login
- Creation of new application stack
- Creation of new application

Delieverable Specification:
- Account Creation
  - Takes credentials (email, username, password)
  - Creates new user in Firebase
  - Sends access keys back to client
  - Creates namespace for user in cluster
  - Installs application builder ServiceAccount to users namespace
  - Automatically deploys default stack with default application
- Account Login
  - Take credentials (email/username, password)
  - Sends access keys back to client
- Creation of new application stack
  - Creates Helm Chart
- Creation of new application

CLI Command Spec:
- All commands start with the global `cloud`
- `cloud register`
  - Prompts user for email, username, and password
  - Creates account for user
  - Creates credential file locally for user
  - Creates namespace for user in cluster
  - Installs application builder ServiceAccount to namespace
  - Deploys "default" stack as a Helm chart
- `cloud login`
  - Either reports that user is already logged in,
    or requests the users credentials
  - Updates users credential file
- `cloud add stack <STACK_NAME>`
  - Creates a new Helm chart template in the users
    namespace
- `cloud delete stack <STACK_NAME>`
  - Deletes a chart from a users namespace, along with
    all apps added inside it
- `cloud add app <GIT_URL> <APP_NAME>`
  - `--stack=<STACK_NAME>`
    - Required, specifies the stack to create the app
    inside
  - `<GIT_URL>`
    - Optional, specifies the git repository to deploy
      from and listen to for updates
    - If not specified, packages the current directory
      to cloud storage and deploys from there
  - Deploys an application to the specified stack
- `cloud update app <APP_NAME>`
  - Manually redeploys and app. If using a repo, will
    rebuild and deploy app. If not using repo, this
    is the only way to redeploy code
- `cloud delete app <APP_NAME>`
  - `--stack=<STACK_NAME>`
    - Required, specifies which stack the deleted app
      resides
- `cloud list stacks`
  - Lists all stacks in users account
- `cloud list apps`
  - `--stack=<STACK_NAME>`
    - Optional, filters apps to only specified stack
  - Lists all apps deployed by user
- `cloud install <STACK_NAME>`
  - Installs a public Helm chart to the users namespace
- `cloud uninstall <STACK_NAME>`
  - Removes a public Helm chart from the users namespace