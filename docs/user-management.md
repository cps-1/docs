# User management

CPS1 supports two types of user accounts: `regular` and `admin`.

A regular user can manage templates and workspaces.

An admin user has full control over the CPS1 instance, including the ability to:

- Create and delete user accounts
- Manage licensing information
- Configure OAuth authentication

CPS1 supports authentication via GitHub and GitLab using OAuth, as well as its own local authentication system.

## Creating a local user account

To create an admin account:

1. Go to the `Users` page in the left sidebar, under the `Administration` section.
2. Click `New User`.
3. Fill in the required information.
4. If this is an Admin user, ensure the `Admin` checkbox is enabled.
5. Click `Create` to finish.

## Configuring OAuth

You can configure OAuth either through the CPS1 web interface or by setting values in the provided Helm charts.

Currently, only GitHub and GitLab are supported as OAuth providers.

After configuring OAuth, you can continue to create local users as needed.

### Setup GitLab as OAuth provider

First, create a new application on your GitLab instance:

1. On your GitLab instance, navigate to your Group page, then go to `Settings` → `Applications`, and create a new application.
2. Set the `Redirect URI` to `https://cps1.example.com/api/auth/gitlab/authorized`, replacing `cps1.example.com` with your CPS1 instance domain. See the [Production Installation](installation/production-installation.md) documentation for more details.
3. Enable the following scopes: `read_api`, `read_user`, `read_repository`, `write_repository`, and `openid`.
4. Save the application and copy the generated secret and Application ID.
5. On your GitLab instance, navigate to your Group page, then go to `Settings` → `General`, and copy your Group ID.

For more information, see the [GitLab OAuth Provider documentation](https://docs.gitlab.com/integration/oauth_provider/).

Next, configure CPS1:

1. Go to the `OAuth` page in the left sidebar, under the `Administration` section.
2. Click on the GitLab tab.
3. In the CPS1 GitLab configuration tab, enter the information provided by GitLab:
    * Application ID
    * Group ID
    * Hostname (default: gitlab.com)
    * Secret
4. Click `Update` to save your settings.
5. The GitLab login option should now appear on the CPS1 login page.

### Setting up GitHub as an OAuth provider

First, create an OAuth App on GitHub by following the [Creating an OAuth app](https://docs.github.com/en/apps/oauth-apps/building-oauth-apps/creating-an-oauth-app) guide with the following configuration:

1. Set the `Homepage URL` to `https://cps1.example.com/`, replacing `cps1.example.com` with your CPS1 instance domain. See the [Production Installation](installation/production-installation.md) documentation for more details.
2. Set the `Authorization callback URL` to `https://cps1.example.com/api/auth/github/authorized`, replacing `cps1.example.com` with your CPS1 instance domain.
3. Register the new OAuth App.
4. On the OAuth App's settings page, click `Generate a new client secret` and copy it.

Next, configure CPS1:

1. Go to the `OAuth` page in the left sidebar, under the `Administration` section.
2. Click on the GitHub tab.
3. In the CPS1 GitHub configuration tab, enter the information provided by GitHub:
    - Client ID
    - Organization Name (the GitHub organization that owns the OAuth App)
    - Secret
4. Click `Update` to save your settings.
5. The GitHub login option should now appear on the CPS1 login page.

