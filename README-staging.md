# The staging version of this site

Is hosted on cbhcloud (kthcloud) by packaging the built site files as a Docker
container and pushing it to cbhcloud (tahaa@kth.se).

The Docker container includes a bare-bones NGINX server configured with
basic authentication (username/password shared among the research data team).

I have configured a CNAME record `workspace.datahub.kth.chepec.se` in the cbhcloud
web admin interface.

To publish the staging site run the `build-staging.sh` script.


## Links and notes

### Setting the .htpasswd file

The `.htpasswd` file contains just a single username/password, which I created interactively:
```
htpasswd -c .htpasswd kthb
```

This basic auth by a shared username/password is good enough for now.

In the near future, we may use kthcloud's Private Auth proxy instead.
Their Auth Proxy is built on Keycloak, and the developers have indicated to me
that it could be tweaked to allow either *any* authenticated user or a predefined
list of KTH accounts.


### Which Markdown generator is MkDocs using?

> The application uses the **Python-Markdown** Markdown processor.
> You can enable additional extensions.
> https://www.markdownguide.org/tools/mkdocs


#### Python-Markdown

+ https://python-markdown.github.io

> [Python-Markdown] is not a CommonMark implementation; nor is it trying to be!
> Python-Markdown was developed long before the CommonMark specification was
> released and has always (mostly) followed the syntax rules and behavior of
> the original reference implementation. No accommodations have been made to
> address the changes which CommonMark has suggested. It is recommended that
> you look elsewhere if you want an implementation which follows the CommonMark specification.

+ https://python-markdown.github.io/extensions - list of official extensions.
  Although I am not yet sure how to enable an extension for use with MkDocs.

In any case, I cannot find any mention that it supports **caption** or **cross-reference**.
Too bad.
