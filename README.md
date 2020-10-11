# Static Website Template

This is a template for a static website that is published over a CDN.

After you create a project from this template, change and extend it to fit your
specific requirements.

## Before you begin

### 1. Create a free Altostra account
To create an account, simply login to the [Altostra Web Console](https://app.altostra.com).

### 2. Install the Altostra CLI
```sh
# make sure you have Node.js 10 or above installed
npm install -g @altostra/cli
```

### 3. Connect an a AWS account
To connect an AWS account, click **Connect Cloud Account** on the [Web Console settings](https://app.altostra.com/settings) page.

> If you don't wish to connect your account just yet, you can deploy to the [Playground](https://docs.altostra.com/reference/concepts/playground-environment.html) environment that simulates the cloud without creating actual resources.

## Using the template

You have several options to get started with this template:
* Initialize a new project from the Altostra CLI and specify the template:

```sh
mkdir static-website
cd static-website
alto init --template static-website
```

* Create a new project from the [Altostra Web Console](https://app.altostra.com/projects), you can select the `static-website` template from the list.

* Apply the template to an existing Altostra project from Visual Studio Code by going to the Altostra view in the main toolbar and clicking on `static-website` in the templates list.

## Deploying the project

Start by logging in from the Altostra CLI:
```sh
alto login
```

>The deployment process is simple and involves a few commands.
>For more information on each command refer to the [Altostra CLI documentation](https://docs.altostra.com/reference/CLI/altostra-cli.html).

Create an [image](https://docs.altostra.com/howto/projects/deploy-project.html#create-a-project-image) of the project:
```sh
alto push v1.0
```

Deploy the image as a new
[deployment](https://docs.altostra.com/reference/concepts/deployments.html) named `main` in the `Production` environment:
```sh
alto deploy main:v1.0 --new Production # omit "--new Production" to update rather than create
```

## View the deployment status and details
You have two options, list the deployment details in the terminal or open the Web Console.

* Using the Altostra CLI:
```sh
alto deployments # list the deployments for the current project
```
```sh
alto deployments main # show details for the deployment "main"
```

* Using the Web Console:
```sh
alto console # will open the Web Console for the current project
```

## Upload and invalidate site content

The infrastructure of our website is ready, but not the content, such as HTML and CSS files.  
To complete our website deployment we need to upload the content files to the bucket, and invalidate the CDN cache.

1. Wait for the infrastructure deployment to complete before proceeding. The
bucket and CDN must be created on your cloud account before you can upload.  
> CDN resources can take up to 20 mins to become available on AWS.

2. Upload the content files for the `main` deployment:

```shell
# uploads files for all buckets and makes the files public
alto sync main --all --public
```

3. Invalidate the CDN cache for the `main` deployment:

```shell
# invalidates the cache for all CDNs
alto invalidate main --all
```

## Modifying the project
To modify the project, install Altostra Tools for Visual Studio Code:

From the terminal:
```sh
code --install-extension Altostra.altostra
```

or, search for Altostra Tools in the Visual Studio Code extensions view.

or, directly from the [marketplace](https://marketplace.visualstudio.com/items?itemName=Altostra.altostra).

> The extension adds an Altostra panel and visual additor that help you modify and
> design the project infrastructure.

## Template content

### Cloud resources
* S3 Bucket
* CloudFront CDN

### Website Files
The template comes with an example website that consists of two files:
- index.html
- style.css

These files are located in the `public` directory in the project root.
To change the directory that you wish to upload, modify the bucket resource settings using Altostra.
For more information, visit
[Altostra's documentation](https://d1nn0ezj50ac1m.cloudfront.net/howto/create-static-website.html#option-b-design-the-architecture)
website.