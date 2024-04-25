# Docker on MacOS - an investigation and eventual surrender
This is a comprehensive documentation of my troubles with docker on MacOS, inspired by an EdStem post I wrote on this topic.

> 🚨: **Spoiler Alert:** This blog post does in fact end in *abject failure*.

I started by following Brian's examples in his lecture on Go and setting up devcontainers. One first difference was I was prompted to install Docker Desktop for Mac, which I did. The `Rebuild and reopen in container` then worked. 

{% include info.html text="So far so good!" %}

However, when trying to run the first command Brian shows `docker run --rm -it ubuntu /bin/bash` I am confronted with the followin

    docker: Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?.
    See 'docker run --help'.

Should be simple right? Let me just turn my Docker app on. Oh wait... 

![](/images/image.png "docker is on")

Weird huh? Still haven't been able to figure that one out. I think maybe the commands are simply different and I'm misinterpreting what Brian is doing, accessing docker inside his docker container. 

Anyway, I continued to follow the examples, but docker was not working as expected, and neither were his Go examples. For example, after running step3 in the lecture code and renaming the hostname in the container, the original containers hostname also changes, while Brian's does not. 

{% include alert.html text="Why Docker (and Go) do you do this!" %}

I also never get any child printing running, for example in step5, and never get the shell inside the container i.e. root@container. Generally just distressing. The below screenshot shows these outputs.

![](/images/image-1.png "docker is broken")

Anywho, at this point I gave up trying to get these inner workings of docker going. Luckily, using cpufrozen and gpufrozen in Brian's course22 notebook for example works well. So maybe not *abject* failure, more just giving up and moving on to stuff that actually works. Now take this ASCII thumbs up because at least something works!

 ( ((
  \ =\
 __\_ `-\ 
(____))(  \----   
(____)) _  
(____))
(____))____/----


> 😞: **Nevermind** The ASCII art did not in fact work.


                                        
