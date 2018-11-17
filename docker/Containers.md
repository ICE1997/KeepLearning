# What is Dockerfile?

> Defines what goes on in the environment inside your container.

Access to resources like networking interfaces and disk drives is virtualized inside this environment, which is isolated from the rest of your system, so you need to map ports to the outside world, and ***be specific about what files you wanna to "copy in" to that environment***.However,after doing that, you can expect that the build of your app defined in this `Dockerfile` behaves exactly the same wherever it runs.



# Create a Dockrfile

1. #### Create an empty directory

2. #### Change directories into the new directory

3. #### Create a file called `Dockerfile`

4. #### Do what you wanna do in the `Dockerfile`

5. #### The example of `Dockerfile`:

```dockerfile
# Use an official Python runtime as a parent image
FROM python:2.7-slim

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install --trusted-host pypi.python.org -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```

6. #### Completes the app:

   - Create `requirements.txt`:

     ```txt
     Flask
     Redis
     ```

   - Create `app.py`:

     ```python
     from flask import Flask
     from redis import Redis, RedisError
     import os
     import socket
     
     # Connect to Redis
     redis = Redis(host="redis", db=0, socket_connect_timeout=2, socket_timeout=2)
     
     app = Flask(__name__)
     
     @app.route("/")
     def hello():
         try:
             visits = redis.incr("counter")
         except RedisError:
             visits = "<i>cannot connect to Redis, counter disabled</i>"
     
         html = "<h3>Hello {name}!</h3>" \
                "<b>Hostname:</b> {hostname}<br/>" \
                "<b>Visits:</b> {visits}"
         return html.format(name=os.getenv("NAME", "world"), hostname=socket.gethostname(), visits=visits)
     
     if __name__ == "__main__":
         app.run(host='0.0.0.0', port=80)
     ```

     PS: the first dns address is yours,the second one is Google's.

# Build an app

1. #### Build:

   ```bash
   docker build -t friendlyhello .
   ```

2. #### Show:

   ```bash
   $ docker image ls
   
   REPOSITORY            TAG                 IMAGE ID
   friendlyhello         latest              326387cea398
   ```



# Set Proxy and DNS

1. #### Proxy server settings:

   > Add the following lines tTroubleshooting for Linux userso the `Dockerfile`(replace the host and port)

   ```dockerfile
   # Set proxy server, replace host:port with values for your servers
   ENV http_proxy host:port
   ENV https_proxy host:port
   ```

2. #### DNS settings:

   > Add the following lines to the `/etc/docker/daemon.json` 

   ```json
   {
     "dns": ["your_dns_address", "8.8.8.8"]
   }
   ```

    *PS: the first dns address is yours,the second one is Google's.*



# Run the app

1. Run the app, mapping(映射) your machine’s port 4000 to the container’s published port 80 using `-p`:

   ```bash
   docker run -p 4000:80 friendlyhello
   ```


2. Go to that URL in a web browser to see the display content served up on a web page.

   > You should see a message that Python is serving your app at `http://0.0.0.0:80`. But that message is coming from inside the container, which doesn’t know you mapped port 80 of that container to 4000, making the correct URL`http://localhost:4000`.

   Go to`http://localhost:4000`



   > PS:You can also use the `curl` command in a shell to view the same content.
   >
   > ```bash
   > $ curl http://localhost:4000
   > 
   > <h3>Hello World!</h3><b>Hostname:</b> 8fc990912a14<br/><b>Visits:</b> <i>cannot connect to Redis, counter disabled</i>
   > ```


3. #### Run in background

   - Start:

     ```bash
     docker run -d -p 4000:80 friendlyhello
     ```

   - Stop:

     ```bash
     docker container stop [container ID]
     ```
