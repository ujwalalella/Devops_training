# Custom Nginx Container Using Podman

## Project Overview

This project demonstrates how to build a custom container image using a Dockerfile and deploy a simple HTML website using Nginx.

I used **Podman** as the container engine to understand containerization concepts and practice building and running custom images.

## Technologies Used

- Podman
- Nginx
- Dockerfile
- HTML
- Windows CMD
- WSL2 (Linux virtual machine)

## Project Structure

```text
container-project/
│
├── Dockerfile
├── index.html
└── README.md
```

## Step 1: Create the HTML Application

Created a simple HTML webpage named `index.html`.

```html
<!DOCTYPE html>
<html>
<head>
    <title>My First Container</title>
</head>
<body>
    <h1>Hello from my custom container!</h1>
    <p>I built this image using Podman and a Dockerfile.</p>
    <p>This is my first custom Nginx deployment.</p>
</body>
</html>
```

## Step 2: Create the Dockerfile

Created a Dockerfile to define the instructions for building the custom Nginx image.

```dockerfile
FROM nginx:latest

WORKDIR /usr/share/nginx/html

COPY index.html .

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```
Make sure it is named `Dockerfile`.

### Dockerfile Explanation

| Instruction | Description |
|---|---|
| FROM | Specifies the base Nginx image |
| WORKDIR | Sets the working directory inside the image |
| COPY | Copies the HTML file into the Nginx web directory |
| EXPOSE | Documents the port used by Nginx |
| CMD | Starts Nginx in the foreground |

## Step 3: Build the Custom Image

```bash
podman build -t my-custom-nginx:v1 .
```
<img width="925" height="373" alt="image" src="https://github.com/user-attachments/assets/e5f9511c-9aa4-47be-be6d-3f158bea0434" />

This command builds a custom image using the Dockerfile in the current directory.

## Step 4: Verify the Image

```bash
podman images
```

Expected image:

```text
my-custom-nginx    v1
```

## Step 5: Run the Custom Container

Run the custom container:

```bash
podman run -d --name custom-nginx -p 8081:80 my-custom-nginx:v1
```

## Step 6: Verify the Running Container

```bash
podman ps
```

Check container logs:

```bash
podman logs custom-nginx
```

<img width="951" height="257" alt="image" src="https://github.com/user-attachments/assets/3b04066e-950c-4e1a-bf49-231df47ee646" />

## Step 7: Access the Website

Open the following URL in a browser:

```text
http://<PODMAN-VM-IP>:8081
```

For my current setup, the Podman VM IP was `192.168.240.45`.

<img width="1919" height="815" alt="Screenshot 2026-10-31 220231" src="https://github.com/user-attachments/assets/4ef2b53a-c393-4327-ad89-58aa07752e95" />

The application is served by Nginx inside the custom container.

## Concepts Learned

- Understanding container images and containers.
- Writing and understanding Dockerfiles.
- Using base images.
- Copying application files into container images.
- Building custom images using Podman.
- Understanding image tags and versions.
- Running containers in detached mode.
- Mapping host ports to container ports.
- Inspecting running containers and application logs.
- Understanding container networking between Windows and WSL2.

## Useful Podman Commands

| Command | Purpose |
|---|---|
| `podman pull nginx` | Download an image |
| `podman images` | List local images |
| `podman build -t my-custom-nginx:v1 .` | Build a custom image |
| `podman run -d --name custom-nginx -p 8081:80 my-custom-nginx:v1` | Run a container |
| `podman ps` | List running containers |
| `podman ps -a` | List all containers |
| `podman logs custom-nginx` | View container logs |
| `podman stop custom-nginx` | Stop a container |
| `podman start custom-nginx` | Start an existing container |
| `podman rm custom-nginx` | Remove a container |

## Learning Outcome

Successfully created a custom Nginx container image using a Dockerfile and deployed a simple HTML website using Podman.

This project is part of my DevOps learning journey, focusing on containerization and practical container management.
