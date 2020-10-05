# Static Website Template
Use this template to create a static website that is published over a CDN.

## Getting started

### Things you'll need 
1. AWS [SAM-CLI](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html)
1. An Altostra Account( Don't have one yet? Just [login](https://app.altostra.com) here)
1. Altostra CLI Installed ([how?](../reference/CLI/altostra-cli.html#installation))
1. VSCode with Altostra Editor ([how?](../getting-started/installation.html#install-the-visual-studio-code-extension))
1. A Connected AWS Account ([how?](../getting-started/connect-your-accounts.html#connect-your-cloud-service-accounts))
1. An Environment connected to your AWS Account ([how?](../howto/envs/manage-environments.html)) - We'll call it `Dev` for berevity, but you can pick any of your environments

### Using the template

You have several options to get started with this template.  
Either go to the Altostra Web Console and create a new project.  
When asked to use a template, select "Static Website".

Alternatively, you can use the Altostra CLI to initialize a new project from the template by running:
```sh
$ alto init --template static-website
```

You can also apply the template to an existing Altostra project from Visual Studio Code by going 
to the Altostra view in the main toolbar and clickign on "Static Website" in the templates list.

### Required configuration

This template contains a few parameters that must be 
[set in the the environment](https://docs.altostra.com/howto/envs/manage-environments.html#manage-configuration-values)
in which the deployment was created.

You may also provide all or part of the configuration when 
[creating or updating the deployment](https://docs.altostra.com/reference/CLI/commands/altostra-cli-deploy.html#providing-configuration).

#### Template parameters

- `DOMAIN`:  
The fully qualified root domain of your application or arganization.
- `DOMAIN_HOST_NAME`:  
A host name for the site CDN.  
It is combined with `DOMAIN` to create a fully qualified domain for the CDN.  
I.E. If we set `DOMAIN: example.com` and `DOMAIN_HOST_NAME: my-site` the CDN would
accept requests for `my-site.example.com`.
- `DOMAIN_CERT`:  
An Amazon certificate manager (ACM) certificate ARN approprite for the domain.

### Project deployment

Here are simple instruction to get you started.  
For more information on each command please consult [Altostra docs](https://docs.altostra.com/reference/CLI/altostra-cli.html).

1. Create an image from the project:
```shell
$ altos push v1.0
```
2. Deploy the image to a new deployment named `main` in the `Dev` environment:
```shell
$ alto deploy main:v1.0 --new Dev
```
3. Update the deployment with new images:
```shell
$ alto deploy main:v2.0
```
4. Manage the project in the Altostra Web Console:
```shell
$ alto console
```

### Upload and invalidate site content:

1. Upload content of all S3 buckets of `main` deployment:
```shell
$ alto sync main --all --public
```
2. Invalidate all CDN caches of `main` deployment:
```shell
$ alto invalidate main --all
```

## Content

The template is made of three resources: 
- An S3 Bucket
- A CloudFront CDN
- Domain Name

### Website Files
The template comes with an example website that consists of two files:
- index.html
- style.css

These files are located in the `public` directory in the project root. 
To change the directory that you wish to upload, modify the bucket resource settings using Altostra.
For more information, visit 
[Altostra's documentation](https://d1nn0ezj50ac1m.cloudfront.net/howto/create-static-website.html#option-b-design-the-architecture)
website.
