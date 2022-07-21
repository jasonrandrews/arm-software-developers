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
$primary: #11809f;    Arm blue web safe
```

### Fonts

```
$google_font_name: "Lato";
$google_font_family: "Lato:300,300i,400,400i,700,700i";
```

### Disable languages

Edit config.toml and set language to Dnglish content/en is the English content.

Delete other language directories

### Home page

content/en/_index.html

### Front image

content/en/featured-background.jpg

### Translucent bar on homepage

config.toml: 

navbar_translucent_over_cover_disable = true

### Footer

Changes in config.toml to remove some of the links

### Search

Use config.toml to change search engines as shows in the docsy documentation

### Code or shell highlighting

use three backticks (grave) to wrap code or shell commands.
```C
printf("hello world\n);
```

If you are unsure of language use shell.

Look at [prism language choice](https://prismjs.com/index.html#supported-languages) to see what's possible. 

### Remove article from left side menu or bottom listing of a page
Hides from left list:
toc_hide: true

Hides from bottom list:
hide_summary: true
