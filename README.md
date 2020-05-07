# Hugo Redirect
A theme component to enable easy redirection in Hugo sites.

## About

Hugo Redirect enables easy redirection: one of the major pieces missing from Hugo's impressive feature set.

Let's say you
* Have an Ugly URLs like `yoursite.com/cv.pdf` and you'd much rather point people to `yoursite.com/cv`
* Wrote an awesome post on `yoursite.com/blog/2019/09/08/how_to_add_clis` and you'd like to share it to people quickly at `yoursite.com/cli`

Redirection comes in very handy in these cases.

Hugo Redirect currently supports static meta refresh based redirects, `_redirect` generation for [Netlify](https://netlify.com) and and `.htaccess` (for Apache / Nginx servers) generation.

This is not a standalone theme. It is a [Hugo](https://gohugo.io) theme component (sort of like a plugin) providing easy URL redirect capabilities to Hugo sites. A working demo of this redirection is available on my site at [https://prag.io/cv](https://prag.io/cv).

Contributions welcome! Send your pull request.

## Usage
In the root of your site repository:

1. Add `hugo-redirect` as a submodule to be able to get upstream changes later
	```sh
    $ git submodule add https://github.com/gcc42/hugo-redirect.git themes/hugo-redirect
    ```
2. Add `hugo-redirect` as the left-most element of the `theme` list variable in your site's or theme's configuration file `config.yaml` or `config.toml`. Example, with `config.yaml`:
    ```yaml
    theme: ["hugo-redirect", "other-components", "my-theme"]
    ```
    or, with `config.toml`,
    ```toml
    theme = ["hugo-redirect", "other-components", "my-theme"]
    ```
3. To add a new redirect rule, simply run (It's not recommended to create
   them manually): 
    ```sh
    $ hugo new redirect/cv.md # Replace cv with a (arbitrary) redirect name
    ```
   Open the newly created file `redirect/cv.md` in your editor and update the
   `url` and `redirect_to` fields in the front matter, like so:
   ```toml
   type = "redirect"
   url = "/cv"
   redirect_to = "/cv.pdf"
   redirect_enabled = true
   ``` 
4. If you're hosting on Netlify or Apache/Nginx/<Service that supports `.htaccess`>, follow the steps below to enable `_redirects` file generation (recommended)

### Hosting on Netlify
If you're using Netlify, you'll want to generate the native `_redirects` file:
1. Copy `_redirects.md` to your content folder:
    ```sh
    $ cp themes/hugo-redirect/content/_redirects.md content/
    ```
2. Edit the file in your text editor and update the value of `draft` from `true` to `false`

### Hosting on Apache / Nginx
Check if your hosting supports the `.htaccess` file configuration. If they do, enable it as:
1. Copy `_htaccess.md` to your content folder:
    ```sh
    $ cp themes/hugo-redirect/content/_htaccess.md content/
    ```
2. Edit the file in your text editor and update the value of `draft` from `true` to `false`

That's it. You're done. Now simply build and deploy your site and any requests to `yoursite.com/cv` should be redirected to `yoursite/cv.pdf`.

## Things to note
1. I'd recommend enabling the appropriate `_redirects`/`.htaccess` based on where you're hosting. (Even though `meta` redirects work fine, this will potentially improve the speed and help with SEO)
2. Avoid mixing `hugo-redirect` with manual redirection, or you could end up creating a nasty redirect loop
3. Make sure you enter the `url` and `redirect_to` parameters *exactly* as you want them. This means that if you want `/cv --> /cv.pdf`, make sure you set `url = /cv` and NOT `url = /cv/` (however because of the way Hugo works currently, both `/cv --> /cv.pdf` and `/cv/ --> /cv.pdf` will be set up)

## Questions?
Create an issue or email me at `pranjal at prag.io`.

Copyright © 2012 onwards, Pranjal Agrawal pranjal@prag.io.
