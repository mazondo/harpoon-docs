# Configuration
Running `harpoon init` will generic a basic configuration for your static site.  The following options can be further defined:
## Example
We'll go through what these options mean below

```json
{
  "name" : "appName",
  "hosting" : "s3",
  "auth_namespace" : "main",
  "hosting_options" : {
    "region" : "us-west-2"
  },
  "domain" : {
    "primary" : "www.domain.com",
    "forwarded" : ["domain.com"]
  },
  "directory" : "public"
}

```

## directory
Specifies a relative directory within the project to use for deploys.  A great example of when this is useful is when your project has a `public` folder that contains the generated app code.

```json
{
  "directory" : "public"
}
```

## domain
This is an object that includes primary and forwarded domain information.  Forwarded domains will be redirected to the primary.

```json
{
  "domain" : {
    "primary" : "your-domain.com",
    "forwarded" : ["www.your-domain.com"]
  }
}
```

## hosting
This is the hosting that will be used to deploy your code.  Right now we only have support for amazon s3, but it's pretty easy to [add your own services](/extending-harpoon).

```json
{
  "hosting" : "s3"
}
```

## hosting_options
These are hosting options in an object that will be passed to the hosting service when setting your system up.  They'll be specific to each service. For amazon s3, the following options are supported:

```json
{
  "hosting_options" : {
    "region" : "us-west-1"
  }
}
```

## auth_namespace
The auth namespace lets you determine which access credentials get utilized for pushing your site.  For example, if you use set the `auth_namespace` to `main` and then set a different site to use `auth_namespace` of `work`, those two apps will be deployed using different keys (and therefore can use different amazon accounts, for example).

```json
{
  "auth_namespace" : "main"
}
```
