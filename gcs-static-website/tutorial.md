# Google Cloud Storage Hosting a static website 

## Let's get started!

This tutorial describes how to configure a Cloud Storage bucket to host a static website. Static web pages can contain client-side technologies such as HTML, CSS, and JavaScript. For more information on static web pages, such as examples, tips and troubleshooting, see the Static Website page.

### Objectives

In this tutorial you will:

* Point your domain to Cloud Storage by using a CNAME record.
* Create a bucket that is linked to your domain.
* Upload and share your site's files.
* Test the website.


## Before you begin

### Register a domain name

This tutorial assumes that you own a top-level domain name which you want to use for your static website. If you don't have one you can register one at [domains.google.com](https://domains.google.com).

### Setup project and billing

`walkthrough project-billing-setup`

## Creating a CNAME record

A CNAME record is a type of DNS record. It directs traffic that requests a URL from your domain to the resources you want to serve, in this case objects in your Cloud Storage buckets. For www.example.com, the CNAME record might contain the following information:

```
NAME                  TYPE     DATA
www.example.com       CNAME    c.storage.googleapis.com.
```

For more information about CNAME redirects, see [URI for CNAME aliasing](https://cloud.google.com/storage/docs/request-endpoints#cname).

## Define a helper environment variable

Let's define your domain name as an environment variable as it will be used in subsequent steps.

Replace `www.example.com` with the subdomain of your domain used when setting up your CNAME record.

```bash
export CLOUD_STORAGE_BUCKET=www.example.com
```

## Creating a bucket

Create a bucket whose name matches the CNAME you created for your domain.

For example, if you added a CNAME record pointing www.example.com to c.storage.googleapis.com., then create a bucket with the name "www.example.com".

To create a bucket:

```bash
gsutil mb gs://$CLOUD_STORAGE_BUCKET
```

## Uploading your site's files

Now you can copy your files up to the GCS bucket and for your convenience you can the following boilerplate website sample:

```bash
gsutil cp gs://cloud-samples-data/storage/*html gs://$CLOUD_STORAGE_BUCKET
```

## Sharing your files

To share publicly the files that you want to serve:

```bash
gsutil acl ch -u AllUsers:R gs://$CLOUD_STORAGE_BUCKET/*.html
```

## Optional: Assigning index and error pages

In the following example, we can define an index and custom error page. For the boilerplate example provided above you can use the following command:

```
gsutil web set -m index.html -e notfound.html gs://$CLOUD_STORAGE_BUCKET
```

## Testing the website

Verify that content is served from the bucket by requesting the domain name in a browser. Alternatively, you can use curl:

```bash
curl $CLOUD_STORAGE_BUCKET
```

## Cleaning up

After you've finished the Hosting a Static Website tutorial, you can clean up the resources you created on Google Cloud Platform so you won't be billed for them in the future. The following sections describe how to delete or turn off these resources.

## Congratulations!

You have completed this tutorial!

