# source of oli.works website

Built with [Hugo](https://gohugo.io/), deployed to [oli.works](https://oli.works).

## .htaccess

Since I wanted to **redirect** the root of the website to /sometimes the site has an .htaccess file to do the redirection and to deliver the HTML file without extension.

```
RewriteEngine on

RewriteRule ^$ /sometimes [L,R=301]

RewriteCond %{THE_REQUEST} /([^.]+)\.html [NC]
RewriteRule ^ /%1 [NC,L,R]

RewriteCond %{REQUEST_FILENAME}.html -f
RewriteRule ^ %{REQUEST_URI}.html [NC,L]
```

## Deployment

Deployment is automatically done using Github Actions triggered by a push to the main branch of the repository.

I want the final page to be /sometimes (**not** /sometimes/). Hugo builds for every single page a separate subdirectory (sometimes.md gets /sometimes/index.html).

So on deployment I copy the built `/sometimes/index.html` file to `sometimes.html`.

## Hosting

Note: The website is hosted by [Opalstack](https://www.opalstack.com/). You have to create an **PHP+Apache** application if you want to use an .htaccess file.
