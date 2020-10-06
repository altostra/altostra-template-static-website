# Static Website Template
Use this template to create a static website that is published over a CDN.

## Getting started

## Things you'll need for this tutorial
1. AWS [SAM-CLI](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html)
1. An Altostra Account (Don't have one yet? Just [login](https://app.altostra.com) here)
1. Altostra CLI installed (`npm i -g @altostra/cli` or [see docs](../reference/CLI/altostra-cli.html#installation))
1. Altostra Tools extension for Visual Studio Code ([VSCode Marketplace](https://marketplace.visualstudio.com/items?itemName=Altostra.altostra) or [see docs](../getting-started/installation.html#install-the-visual-studio-code-extension))
1. A connected AWS cloud account ( [Web Console settings](https://app.altostra.com/settings)  or [see docs](../getting-started/connect-your-accounts.html#connect-your-cloud-service-accounts))
1. An Environment connected to your AWS Account ([Web Console environments](https://app.altostra.com/environments) or [see docs](../howto/envs/manage-environments.html)) - We'll call it `Dev` for berevity, but you can pick any of your environments


### Using the template

You have several options to get started with this template.  
Either go to the Altostra Web Console and create a new project.  
When asked to use a template, select "static-website".

Alternatively, you can use the Altostra CLI to initialize a new project from the template by running:
```sh
$ alto init --template static-website
```

You can also apply the template to an existing Altostra project from Visual Studio Code by going
to the Altostra view in the main toolbar and clickign on "static-website" in the templates list.

### Project deployment

Run the following commands to create a deployment image of the project and deploy it as a new instance.

For more information on each command refer to the [Altostra CLI docs](https://docs.altostra.com/reference/CLI/altostra-cli.html).

1. Create an
[image](https://docs.altostra.com/howto/projects/deploy-project.html#create-a-project-image)
from the project:
```shell
$ altos push v1.0
```
2. Deploy the image to a new deployment named `main` in the `Dev` environment:
```shell
$ alto deploy main:v1.0 --new Dev
```
3. Manage the project in the Altostra Web Console:
```shell
$ alto console
```

> To update an existing deployment with new images just omit the `--new` flag and environment name:
> ```shell
> $ alto deploy main:v2.0
>```

### Upload and invalidate site content

The infrastructure of our site is ready, but the site contains no content.  
To complete our web-site we need to upload the site content to its bucket,
and invalidate the CDN's cache.

1. Upload content of all S3 buckets of `main` deployment:
```shell
$ alto sync main --all --public
```
2. Invalidate all CDN caches of `main` deployment:
```shell
$ alto invalidate main --all
```

## Content

The template is made of two resources:
- An S3 Bucket
- A CloudFront CDN

### Website Files
The template comes with an example website that consists of two files:
- index.html
- style.css

These files are located in the `public` directory in the project root.
To change the directory that you wish to upload, modify the bucket resource settings using Altostra.
For more information, visit
[Altostra's documentation](https://d1nn0ezj50ac1m.cloudfront.net/howto/create-static-website.html#option-b-design-the-architecture)
website.
