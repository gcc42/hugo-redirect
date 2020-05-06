# Hugo Redirector
A theme component to enable easy redirection in Hugo sites.

## About

This is not a standalone theme. It is a [Hugo](https://gohugo.io) theme component providing easy URL redirection facilities.

Redirector currently supports static meta refresh based redirects and `_redirect` file generation for [Netlify](https://netlify.com). I plan to add `.htaccess` generation (for apache / Nginx) at some point as well. Contributions welcome! Send your pull request.

A working demo of this redirection is available on my site at [https://prag.io/cv](https://prag.io/cv).

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
3. If you wish to generate `_redirects` file for Netlify native redirection, copy [\_redirects.md]() to your `content/` directory (at the root) and enable it.
    ```sh
    $ cp themes/hugo-redirector/content/_redirects.md content/
    ```

4. To add a new redirection rule, simply run
    ```sh
    $ hugo new redirect/cv.md # Replace cv with a (arbitrary) redirect name
    ```
   Open the file `redirect/cv.md` in your editor and update the `url` and `redirect_to` fields in the front matter. Example:
   ```toml
   +++
   type = "redirect"
   url = "/cv"
   redirect_to = "/cv.pdf"
   redirect_enabled = true
   +++
   ```

That's it. You're done. Now simply build and deploy your site and any requests to `yoursite.com/cv` should be redirected to `yoursite/cv.pdf`.

## Questions?
Create an issue or email me at `pranjal at prag.io`.

Copyright © 2012 onwards, Pranjal Agrawal pranjal@prag.io.
