# Static Website Template
Use this template to create a static website that is published over a CDN.

The template is made of two resources: 
- An S3 Bucket
- A CloudFront CDN

The static files to be uploaded to the bucket are located in the `public` directory in the project root. You can change this at any time by modifying the bucket resource.

## Content
The template comes with an example website that consists of two files:
- index.html
- style.css

## Installing
Either go to the Altostra Web Console and create a new project. When asked to use a template, select "Static Website".  
Alternatively, you can use the Altostra CLI by running `alto init --template static-website`.
Or, you can apply the template to an existing Altostr project from Visutal Studio Code by going to the Altostra view in the main toolbar and clickign on "Static Website" in the templates list.

## Deploying
To deploy the resources, run `alto deploy`, or use the 'DEPLOY' button in Visual Studio Code in the Altostra view.
To learn more about deploying, visit [Altostra's documentation](https://docs.altostra.com/getting-started/create-simple-api-project.html#deploying) website.

## Uploading Files
You only need to deploy the project once if you don't make any changes to the architecture design, i.e. you don't change the CDN or Bucket settings.
Whenever you wish to upload the website files run `alto sync` in the project directory - it will also clear the CDN cache for you.
