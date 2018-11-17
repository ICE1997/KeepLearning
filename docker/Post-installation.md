# Manage Docker as a non-root user

The Docker daemon binds to a Unix socket instead of a TCP port.By default that Unix socket owned by the user `root` and other users can only access it using `sudo`.The Docker daemon always runs as the `root` user.

If you dont want to *preface*(加前缀) the `docker` command *with* `sudo`, create a Unix group called `docker` and add users to it.When the Docker daemon starts, it creates a Unix socket accessible by members of the `docker` group.

> #### Warning
>
> The `docker` group grants privileges equivalent to the `root` user.



To create the `docker` group and add your user:

1. Create the `docker` group.

   ```bash
   $ sudo groupadd docker
   ```

2. Add your user to the `docker` group.

   ```bash
   $ sudo usermod -aG docker $USER
   ```

3. Log out and log back in so that your group membership is re-evaluated.

   If testing on a virtual machine, it may be necessary to restart the virtual machine for changes to take effect.On a desktop Linux environment such as X Windows,log out of your session completely and then log back in.

4. Verify that you can run `docker` commands without `sudo`.

   ```bash
   $ docker run hello-world
   ```

