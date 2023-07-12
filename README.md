# CMI Docu-Build

This GitHub Action converts markdown files using MkDocs to a versionized GitHub Pages documentation using mike.

## What does this action do?

This GitHub Action automates the process of converting markdown files into a versionized GitHub Pages documentation using MkDocs. It not only generates and deploys the documentation for each version but also includes a version discovery page. The version discovery page serves as a central hub where users can easily navigate and explore different versions of your documentation. By accessing the version discovery page, users can conveniently switch between versions and access the specific documentation they need. This helps streamline the user experience and ensures that visitors can find the information relevant to their desired version with ease. With this action, powered by MkDocs, you can effortlessly maintain versionized documentation and provide a seamless browsing experience for your users.

- The version discovery page ist reachable on: `/index.html`
- The versionized documentations are reachable on: `/[Version]/...`

## Requirements

To use this GitHub Action, make sure you meet the following requirements:

- **MkDocs Configuration**: You need to have an `mkdocs.yml` file in the root directory of your repository. This file serves as the configuration file for MkDocs and defines the structure and settings of your documentation.

### Setting up `mkdocs.yml`

To set up the `mkdocs.yml` file, follow these steps:

1. Create a file named `mkdocs.yml` in the root directory of your repository.
2. Open the `mkdocs.yml` file and define the structure and configuration options for your documentation.
3. Customize the settings according to your project's requirements. You can specify the theme, navigation, plugins, and other options as needed.

For detailed information on configuring `mkdocs.yml`, refer to the [MkDocs User Guide](https://www.mkdocs.org/user-guide/configuration/). The user guide provides comprehensive documentation on various configuration options, including themes, navigation, Markdown extensions, and more.

To ensure proper functionality, the following configuration needs to be included in the mkdocs.yml file:

```yaml
extra:
  version:
    provider: mike
```

This configuration is needed for mike to work properly with MkDocs. It enables versioning of your documentation.

## Usage

To use this action, include the following steps in your workflow:

```yaml
steps:
    - name: Checkout
        uses: actions/checkout@v3
        with:
            fetch-depth: 0 // Fetch-Depth is important, because we need all branches and the complete history
            
    - name: Build documentation and publish
        uses: CMInformatik/docu-build@v1
        with:
            github-token: ${{ secrets.GITHUB_TOKEN }}
            version: [Documentation version]
            versionDiscoveryPageLocation: [Path to version discovery page]
```

## Inputs

- `github-token` (required): GitHub token used for authentication and accessing repositories. Usually you can use `${{ secrets.GITHUB_TOKEN }}`
- `version` (required): Specifies the version of the documentation (Example: v.1.1.0)
- `versionDiscoveryPageLocation` (required): Specifies the location (directory) of the version discovery page. You can find an example of the version discovery page in this repository by navigating to the ./version-discovery-page-example directory