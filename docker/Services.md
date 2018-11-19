# Install Docker compose

> You can run Compose on macOS,Windows,and 64-bit Linux

## Prerequisites

Docker Compose relies on Docker Engine for any meaningful work, so make sure you have Docker Engine installed either locally or remote, depending on your setup.

- On desktop systems like Docker for Mac and windows, Docker Compose is included as part of those desktop installs.
- On Linux systems,first install the Docker for your OS,then install Compose on Linux systems.
- To run Compose as a non-root user,you should [manage Docker as a non-root user.](https://docs.docker.com/install/linux/linux-postinstall/)



## Install Compose

Follow the instructions below to install Compose on Mac,Windows, Windows Server 2016, or Linux systems, or find out about alternatives like using the `pip` Python package manager or installing Compose as a container.

### Install Compose on macOS

**Docker for Mac** and **Docker Toolbox** already include Compose along with other Docker apps,so Mac users do not need to install Compose separately.

#### Upgrading

If you're upgrading from Compose 1.2 or earlier, remove or migrate your existing containers after upgrading Compose.This is because, as of version 1.3, Compose uses Docker labels to keep track of containers, and your containers need to be recreated to add the labels.

If Compose detects containers that were created without labels, it refuses to run so that you dont end up with two sets of them.If you want to keep using your existing containers(for example, because the have data volumes you want to preserve),you can user Compose 1.5.x to migrate them with the following command:

```bash
docker-compose migrate-to-labels
```

 Alternatively,if you're not worried about keeping them, you can remove them.Compose just create new ones.

```
docker container rm -f -v myapp_web_1 myapp_db_1 ...
```



#### Unistallation

To uninstall Docker Compose if you installed using `curl`:

```bash
sudo rm /usr/local/bin/docker-compose
```

To unistall Docker Compose if you installed using `pip`:

```bash
pip uninstall docker-compose
```

### Install Compose on Windows

**Docker for Windows** and **Docker Toolbox** already include Compose along with other Docker apps, so most Windows users do not need to install Compose separately.



**If you  are running the Docker daemon and client directly on Microsoft Windows Server 2016**, you do need to install Docker Compose.To do so,follow these step:

1. Start an "elevated" PowerShell(run it as administrator).Search for PowerShell,right-click, and choose **Run as adminstrator.** 

   In Powershell, since Github now requires TLS1.2,run the following:

   ```powershell
   [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
   ```

   The run the following command o download Docker Compose, replacing `$dockerComposeVersion` with   the specific version of Compose you want to use:

   ```powershell
   Invoke-WebRequest "https://github.com/docker/compose/releases/download/$dockerComposeVersion/docker-compose-Windows-x86_64.exe" -UseBasicParsing -OutFile $Env:ProgramFiles\docker\docker-compose.exe
   ```

   For example, to download Compose version 1.23.1,the command is:

   ```powershell
   Invoke-WebRequest "https://github.com/docker/compose/releases/download/1.23.1/docker-compose-Windows-x86_64.exe" -UseBasicParsing -OutFile $Env:ProgramFiles\docker\docker-compose.exe
   ```


#### Upgrading

If you’re upgrading from Compose 1.2 or earlier, remove or migrate your existing containers after upgrading Compose. This is because, as of version 1.3, Compose uses Docker labels to keep track of containers, and your containers need to be recreated to add the labels.

If Compose detects containers that were created without labels, it refuses to run so that you don’t end up with two sets of them. If you want to keep using your existing containers (for example, because they have data volumes you want to preserve), you can use Compose 1.5.x to migrate them with the following command:

```
docker-compose migrate-to-labels
```

Alternatively, if you’re not worried about keeping them, you can remove them. Compose just creates new ones.

```
docker container rm -f -v myapp_web_1 myapp_db_1 ...
```

#### Uninstallation

To uninstall Docker Compose if you installed using `curl`:

```
sudo rm /usr/local/bin/docker-compose
```

To uninstall Docker Compose if you installed using `pip`:

```
pip uninstall docker-compose
```

> Got a “Permission denied” error?
>
> If you get a “Permission denied” error using either of the above methods, you probably do not have the proper permissions to remove `docker-compose`. To force the removal, prepend `sudo` to either of the above commands and run again.



### Install Compose on Linux systems

On **Linux**, you can download the Docker Compose binary  from the  [Compose repository release page on GitHub](https://github.com/docker/compose/releases). Follow the instructions from the link, which involve runing the `curl` command in your terminal to download the binaries.These step by step instructions are also included below.

1. Run this command to download the latest version of Docker Compose:

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.23.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

> Use the latest Compose release number in the download command.The above command is an *example*, and it may become out-of-date. To ensure you have the latest version, check the [Compose repository release page on GitHub](https://github.com/docker/compose/releases).

2. Apply executable permissions to the binary:

   ```bash
   sudo chmod +x /usr/local/bin/docker-compose
   ```

3. Optionally, install  [command completion](https://docs.docker.com/compose/completion/) for the `bash` and `zsh` shell.

4. Test the installation.

   ```bash
   $ docker-compose --version
   docker-compose version 1.23.1, build 1719ceb
   ```

#### Upgrading

If you’re upgrading from Compose 1.2 or earlier, remove or migrate your existing containers after upgrading Compose. This is because, as of version 1.3, Compose uses Docker labels to keep track of containers, and your containers need to be recreated to add the labels.

If Compose detects containers that were created without labels, it refuses to run so that you don’t end up with two sets of them. If you want to keep using your existing containers (for example, because they have data volumes you want to preserve), you can use Compose 1.5.x to migrate them with the following command:

```
docker-compose migrate-to-labels
```

Alternatively, if you’re not worried about keeping them, you can remove them. Compose just creates new ones.

```
docker container rm -f -v myapp_web_1 myapp_db_1 ...
```

#### Unistallation

To uninstall Docker Compose if you installed using `curl`:

```
sudo rm /usr/local/bin/docker-compose
```

To uninstall Docker Compose if you installed using `pip`:

```
pip uninstall docker-compose
```

> Got a “Permission denied” error?
>
> If you get a “Permission denied” error using either of the above methods, you probably do not have the proper permissions to remove `docker-compose`. To force the removal, prepend `sudo` to either of the above commands and run again.

# About services

In a distributed application, different pieces of the app are called "services".For example, if you imagine a video sharing site, it probably includes **a service for storing application data in a database**, **a service for video transcoding in the background **after a user uploads something, a service for the front-end, and so on.

Services are really just "containers in production". A services only runs one image, but **it codifiles the way that image runs-what ports it should use, how many replicas(副本) of the container should run so the service has the capacity it needs**, and so on.Scaling a service changes the number of container instances runing that piece of software, assigning more computing resources to the service in the process.

Luckily it's very easy to define, run, and scale services with the Docker platform-just write a `docker-compose.yml` file.

# Your first `docker-compose.yml` file

A `docker-compose.yml` file is a YAML file that  defines **how Docker containers should bahave in producion.** 

`docker-compose.yml` 

Save this files as `docker-compose.yml` wherever you want.Be sure you have  [pushed the image](https://docs.docker.com/get-started/part2/#share-your-image) you created in Part 2 to a registry, and update this `.yml` by replacing `username/repo:tag` with your image details.

```yaml
version: "3"
services:
  web:
    # replace username/repo:tag with your name and image details
    image: username/repo:tag
    deploy:
      replicas: 5
      resources:
        limits:
          cpus: "0.1"
          memory: 50M
      restart_policy:
        condition: on-failure
    ports:
      - "4000:80"
    networks:
      - webnet
networks:
  webnet:
```

This `docker-compose.yml` file tells Docker to do the following:

- Pull [the image we uploaded in step 2](https://docs.docker.com/get-started/part2/) from the registry.
- Run 5 instances of that image as a service called `web`, limiting each one to use, at most, 10% of the CPU(across all cores), and 50MB of RAM.
- Immediately restart containers if one fails.
- Map port 4000 on the host to `web` 's port 80.
- Instruct `web`'s containers to share port 80 via a load-balanced network called `webnet`.(Internally(内部地),the containers themselves publish to `web`'s port  at an ephemetal (短暂的)port.)
- Define the `webnet` network with the default settings(which is a load-balanced overlay(覆盖) network).

# Run your new load-balanced app

Before we can use the `docker stack deploy` command we first run:

```bash
docker swarm init
```

> **Note**: We get into the meaning of that command in [part 4](https://docs.docker.com/get-started/part4/). If you don’t run `docker swarm init` you get an error that “this node is not a swarm manager.”

Now let's run it.You need to give your app a name.Here, it is set to `getstaredlab`:

```
docker stack deploy -c docker-compose.yml getstartedlab
```

Our single service stack is running 5 containers instances of our deployed(部署) image on one host.Let's investigate.Get the service ID for the one service in our application:

```
docker service ls
```

Look for output for the `web` service, prepended(附加) with your app name.If you named it the same as shown in this example, the name is `getstaredlab_web`. This service ID is listed as well, along with the number of replicas(副本),image name, and exposed ports.

A single container running in a service is called a `task`. Task are given unique IDs that numerically increment,up to the number of `replicas` you defined in `docker-compose.yml`. List the tasks for your service:

```
docker service ps getstartedlab_web
```

Task also show up if you just list all the containers on your system,though that is not filtered by service:

```
docker container ls -q
```

You can run `curl -4 http://localhost:4000` several times in a row, or go to that URL in your browser and hit refresh a few times.

Either way,the container ID changes,demonstrating the load-balancing; with each request, one of the 5 tasks is chosen, in a round-robin fashion, to respond. The container IDs match your output from the previous command(`docker container ls -q`).

> Running Windows 10?
>
> Windows 10 PowerShell should already have `curl` available, but if not you can grab a Linux terminal emulator like [Git BASH](https://git-for-windows.github.io/), or download [wget for Windows](http://gnuwin32.sourceforge.net/packages/wget.htm) which is very similar.

> Slow response times?
>
> Depending on your environment’s networking configuration, it may take up to 30 seconds for the containers to respond to HTTP requests. This is not indicative of Docker or swarm performance, but rather an unmet Redis dependency that we address later in the tutorial. For now, the visitor counter isn’t working for the same reason; we haven’t yet added a service to persist data.



# Scale the app

You can scale the app by changing the `replicas` value in `docker-compose.yml`, saving the change, and re-running the `docker stack deploy`command:

```bash
docker stack deploy -c docker-compose.yml getstartedlab
```

Docker performs an in-place update(就地更新), no need to tear the stack down first or kill any containers.

Now,re-run `docker container ls -q` to see the deployed instances reconfigured.If you scaled up the replicas, more tasks, and hence(于是), more containers, are  started.

# Take down the app and the swarm

- Take the app down with `docker stack rm`:

  ```
  docker stack rm getstartedlab
  ```

- Take down the swarm.

  ```
  docker swarm leave --force
  ```

It's as easy as that to stand up and scale your app with Docker. You've taken a huge step towards learning how to run containers in production. Up next, you learn how to run this app as a bonafide swarm on a cluster of Docker machines.

> **Note**: Compose files like this are used to define applications with Docker, and can be uploaded to cloud providers using [Docker Cloud](https://docs.docker.com/docker-cloud/), or on any hardware or cloud provider you choose with [Docker Enterprise Edition](https://www.docker.com/enterprise-edition).