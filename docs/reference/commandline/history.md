---
title: "history"
description: "The history command description and usage"
keywords: "docker, image, history"
---

# history

```markdown
Usage:  docker history [OPTIONS] IMAGE

Show the history of an image

Aliases:
  docker image history, docker history

Options:
      --format string   Pretty-print images using a Go template
      --help            Print usage
  -H, --human           Print sizes and dates in human readable format (default true)
      --no-trunc        Don't truncate output
  -q, --quiet           Only show image IDs
```


## Examples

To see how the `docker:latest` image was built:

```console
$ docker history docker

IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
3e23a5875458        8 days ago          /bin/sh -c #(nop) ENV LC_ALL=C.UTF-8            0 B
8578938dd170        8 days ago          /bin/sh -c dpkg-reconfigure locales &&    loc   1.245 MB
be51b77efb42        8 days ago          /bin/sh -c apt-get update && apt-get install    338.3 MB
4b137612be55        6 weeks ago         /bin/sh -c #(nop) ADD jessie.tar.xz in /        121 MB
750d58736b4b        6 weeks ago         /bin/sh -c #(nop) MAINTAINER Tianon Gravi <ad   0 B
511136ea3c5a        9 months ago                                                        0 B                 Imported from -
```

To see how the `docker:apache` image was added to a container's base image:

```console
$ docker history docker:scm
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
2ac9d1098bf1        3 months ago        /bin/bash                                       241.4 MB            Added Apache to Fedora base image
88b42ffd1f7c        5 months ago        /bin/sh -c #(nop) ADD file:1fd8d7f9f6557cafc7   373.7 MB
c69cab00d6ef        5 months ago        /bin/sh -c #(nop) MAINTAINER Lokesh Mandvekar   0 B
511136ea3c5a        19 months ago                                                       0 B                 Imported from -
```

### <a name=format></a> Format the output (--format)

The formatting option (`--format`) will pretty-prints history output
using a Go template.

Valid placeholders for the Go template are listed below:

| Placeholder     | Description                                                                                               |
|-----------------|-----------------------------------------------------------------------------------------------------------|
| `.ID`           | Image ID                                                                                                  |
| `.CreatedSince` | Elapsed time since the image was created if `--human=true`, otherwise timestamp of when image was created |
| `.CreatedAt`    | Timestamp of when image was created                                                                       |
| `.CreatedBy`    | Command that was used to create the image                                                                 |
| `.Size`         | Image disk size                                                                                           |
| `.Comment`      | Comment for image                                                                                         |

When using the `--format` option, the `history` command will either
output the data exactly as the template declares or, when using the
`table` directive, will include column headers as well.

The following example uses a template without headers and outputs the
`ID` and `CreatedSince` entries separated by a colon (`:`) for the `busybox`
image:

```console
$ docker history --format "{{.ID}}: {{.CreatedSince}}" busybox

f6e427c148a7: 4 weeks ago
<missing>: 4 weeks ago
```
