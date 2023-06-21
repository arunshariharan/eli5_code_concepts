# eli5_code_concepts
My space to write code blocks, concepts or blog on things I learn, so I can come back to it later when I need them.

# Installing Dependencies

Before running local server for the first time, go to the root directory of your site and run:
```bash
$ bundle
```

# Running Local Server

To preview the site contents before publishing, so just run it by:

```bash
$ bundle exec jekyll s
```

Or run the site on Docker with the following command:
	
```bash
$ docker run -it --rm \
    --volume="$PWD:/srv/jekyll" \
    -p 4000:4000 jekyll/jekyll \
    jekyll serve
```

After a few seconds, the local service will be published at http://127.0.0.1:4000.

# Additional information
For additional information or debugging, check out [Getting started](https://chirpy.cotes.page/posts/getting-started/) from the theme's author