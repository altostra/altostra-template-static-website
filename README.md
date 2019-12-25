# Static Website Template
Use this template to create a static website that is published over a CDN.

The template is made of two resources: 
- An S3 Bucket
- A CloudFront CDN

## Website Files
The template comes with an example website that consists of two files:
- index.html
- style.css

These files are located in the `public` directory in the project root. 
To change the directory that you wish to upload, modify the bucket resource settings using Altostra. For more information, visit [Altostra's documentation](https://d1nn0ezj50ac1m.cloudfront.net/howto/create-static-website.html#option-b-design-the-architecture) website.

## How to Use this Template
You have several options to get started with this template. Either go to the Altostra Web Console and create a new project. When asked to use a template, select "Static Website".  

Alternatively, you can use the Altostra CLI to initialize a new project from the template by running:
```sh
$ alto init --template static-website
```

You can also apply the template to an existing Altostra project from Visual Studio Code by going to the Altostra view in the main toolbar and clickign on "Static Website" in the templates list.

## Deploying
To deploy the project, run:
```sh
$ alto deploy
```
Or use the `DEPLOY` button in Visual Studio Code in the Altostra view.

To learn more about deploying Altostra projects, visit [Altostra's documentation](https://docs.altostra.com/getting-started/create-simple-api-project.html#deploying) website.

## Uploading Files
You only need to deploy the project once if you don't make any changes to the architecture design, i.e. you don't change the CDN or Bucket settings.

Whenever you wish to upload updated website files, run in the project root directory:
```sh
$ alto sync
```
The `sync` command will upload the files to the bucket and it will clear the CDN cache for you.
