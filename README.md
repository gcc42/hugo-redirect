# Hugo Redirector
A theme component to enable easy redirection in Hugo sites.

## About

Redirector enables easy redirection: one of the major pieces missing from Hugo's impressive feature set.

Let's say you
* Have an Ugly URLs like `yoursite.com/cv.pdf` and you'd much rather point people to `yoursite.com/cv`
* Wrote an awesome post on `yoursite.com/blog/2019/09/08/how_to_add_clis` and you'd like to share it to people quickly at `yoursite.com/cli`

Redirection comes in very handy in these cases.

Redirector currently supports static meta refresh based redirects and `_redirect` file generation for [Netlify](https://netlify.com). I plan to add `.htaccess` generation (for Apache / Nginx servers) at some point as well. Static meta refreshes should be avoided in favor of `_redirect/.htaccess` whenever possible. 

This is not a standalone theme. It is a [Hugo](https://gohugo.io) theme component (sort of like a plugin) providing easy URL redirect capabilities to Hugo sites. A working demo of this redirection is available on my site at [https://goofy-meninsky-b0d70c.netlify.app/cv](https://goofy-meninsky-b0d70c.netlify.app/cv).

Contributions welcome! Send your pull request.

## Usage
In the root of your site repository:

1. Add the `hugo-redirector` as a submodule to be able to get upstream changes later
	```sh
    $ git submodule add https://github.com/gcc42/hugo-redirector.git themes/hugo-redirector
    ```
2. Add `hugo-redirector` as the left-most element of the `theme` list variable in your site's or theme's configuration file `config.yaml` or `config.toml`. Example, with `config.yaml`:
    ```yaml
    theme: ["hugo-redirector", "other-components", "my-theme"]
    ```
    or, with `config.toml`,
    ```toml
    theme = ["hugo-redirector", "other-components", "my-theme"]
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
4. If you're hosting on Netlify, follow the steps below to enable `_redirects` file generation (recommended)

### Hosting on Netlify
If you're using Netlify, you'll want to generate the native `_redirects` file. Even though `meta` redirects work fine without it, this will potentially improve the speed and help with SEO.

1. Copy `_redirects.md` to your content folder:
    ```sh
    $ cp themes/hugo-redirector/content/_redirects.md content/
    ```
2. Edit the file in your text editor and update the value of `draft` from `true` to `false`

That's it. You're done. Now simply build and deploy your site and any requests to `yoursite.com/cv` should be redirected to `yoursite/cv.pdf`.

## Questions?
Create an issue or email me at `pranjal at prag.io`.

Copyright © 2012 onwards, Pranjal Agrawal pranjal@prag.io.
