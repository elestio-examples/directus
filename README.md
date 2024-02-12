# Directus docker compose demo CI/CD pipeline

<a href="https://dash.elest.io/deploy?source=cicd&social=dockerCompose&url=https://github.com/elestio-examples/docker-compose-directus"><img src="deploy-on-elestio.png" alt="Deploy on Elest.io" width="180px" /></a>

Example CI/CD pipeline showing how to deploy a direct instance to elestio.

<img src="directus.jpg" style='width: 100%;'/>
<br/>
<br/>

# Once deployed ...

You can connect to the Directus Dashboard:

    Access URL: https://[CI_CD_DOMAIN]/
    Login: [ADMIN_EMAIL] (set in env var)
    Password: [ADMIN_PASSWORD] (set in env var)

# Note

By default, it is preloaded with version 9.26.0, and subsequent versions will be accompanied by a BSL license. For additional information on the Directus BSL license, you can check <a href="https://directus.io/bsl">here.</a>

# Directus Extensions Installation Guide

This guide provides instructions on how to install extensions to your Directus project.

## Prerequisites

Before proceeding with the installation, ensure that you have the following:

If you want to install extensions to your Directus, follow the instructions:

- Access to your Directus project.
- An extension package with the following files:

  - `package.json`
  - `api.js`
  - `app.js`

## Installation Steps

1.  **Locate an Extension:** Find the extension you wish to install. For example https://github.com/utomic-media/directus-extension-field-actions

2.  **Access Your Project:** Open your Directus project using VS Code. You can do this by navigating to the Elestio dashboard, clicking on the `Tools` tab, and selecting `VS Code`.

3.  **Navigate to Extensions Folder:** In VS Code, locate the `extensions` folder within your project.

4.  **Create a New Folder:** Inside the extensions folder, create a new folder. This folder name must begin with the prefix `directus-extensions-`. For example, if you're installing the extension from the provided link, name the folder `directus-extension-field-actions`.

5.  **Prepare the Folder Structure:** Inside the newly created folder, `directus-extension-field-actions`, create another folder named dist. This structure ensures that the extension files are organized properly.

6.  **Copy Files:** Copy the `package.json` file into the `directus-extension-field-actions` folder, and copy `api.js` and `app.js` into the `dist` folder. Your folder structure should look like this:

        ├── extensions
        │   ├── directus-extension-field-actions
        │   │   ├── dist
        │   │   │   ├── app.js
        │   │   │   ├── api.js
        │   │   ├── package.json

7.  **Restart Directus:** Quit VS Code and return to the Elestio dashboard. Click on the `Restart` button to apply the changes.

## Conclusion

You have successfully installed the extension to your Directus project. You can now utilize its functionality within your Directus environment.
