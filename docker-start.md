## Getting Started with Docker

#

### Setup and Running

1.  Download docker from docker.com then install and run it.

2.  If everything goes well then you can check the docker version using the following command:

        $ docker version

3.  To test if the docker is running well run the following command in command line:

        $ docker run hello-docker

    This will downlaod the hello-world image from the docker hub and run it.

4.  More tesing using busybox and passing default comman to run as following manner:

        $ docker run <image name> command
        $ docker run busybox echo hello busybox

    This will download the image busybox from the docker hub echo the text 'hello busybox'

    We can test another command using busybox:

        $ docker run busybox ls

    This will print all the directories inside the busybox container. Important part of these test is to remember that `echo` or `ls` command is available in busybox container, so we can run and test it. These command will not work on `hello-world`.

5.  List all docker container

        $ docker ps

6.  List all the docker ever created

        $ docker ps --all

7.  `docker run` is a command combind with 2 commands: `docker create <image-name>` and `docker start <container-id>`. Let's try to create and start a docker image:

        $ docker create hello-world

    This will print an ID, you should copy the ID to run it using the folloing command:

        $ docker start -a <container-id>

    N.B.: `docker start` without the option `-a` will only print the docker container ID

8.  Delete all the docker image

        $ docker system prune

9.  See logs of any stopped logger

        $ docker logs <container-id>

10. Stopping a running container

        $ docker stop <container-id>

    This will stop the docker completing it's current process. If it passed 10 second then the `docker kill <container-id>` to stop the docker.

11. Stop or kill running docker immidiately:

        $ docker kill <container-id>

12. Execute an additional command in a container:

        $ docker exec -it <container-id> <command>

13. Running sheel command inside a docker:

        $ docker exec -it <container-id> sh

    This will let you execute linux command like `ls`, `cd` and so on.

14.
