## Docsy template customization notes

### AWS S3 useful info:
https://www.noorix.com.au/blog/how-to/hosting-static-website-with-aws-s3-cloudfront/

### Deploy:
```
hugo --gc --minify
hugo deploy
```

### AWS Config info:

bucketname and cloudfront ID is in config.toml

aws configure must work to access s3

## Site configuration info

### To set the Title:

Edit config.toml

### To add the Logo:

assets/icons/logo.svg

Made width and height 50 

### Favicons

static/favicons

### Colors

assets/scss/_variables_project.scss
```
$primary: #002B49;   Arm dark blue
$primary: #333E48;    Arm black
$primary: #0091BD;    Arm blue
```

### Fonts

```
$google_font_name: "Lato";
$google_font_family: "Lato:300,300i,400,400i,700,700i";
```

### Disable languages

Edit config.toml and move en/ directory to content/ 

Delete other language directories

### Home page

content/_index.html

### Front image

content/featured-background.jpg

### Translucent bar on homepage

config.toml: 

navbar_translucent_over_cover_disable = true

### Footer

Changes in config.toml to remove some of the links

### Search

Use config.toml to change search engines as shows in the docsy documentation

