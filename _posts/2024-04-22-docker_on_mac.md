# Docker on MacOS - an investigation and eventual surrender
This is a comprehensive documentation of my troubles with docker on MacOS, inspired by an EdStem post I wrote on this topic.

> :warning: **Spoiler Alert:** This blog post does in fact end in *abject failure*.

I started by following Brian's examples in his lecture on Go and setting up devcontainers. One first difference was I was prompted to install Docker Desktop for Mac, which I did. The `Rebuild and reopen in container` then worked. 

{% include info.html text="So far so good!" %}

However, when trying to run the first command Brian shows `docker run --rm -it ubuntu /bin/bash` I am confronted with the followin

    docker: Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?.
See 'docker run --help'.

Should be simple right? Let me just turn my Docker app on. Oh wait... 


