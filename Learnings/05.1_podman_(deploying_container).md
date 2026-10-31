# Deploying an Nginx Container Using Podman

## 1. Objective

Learn the fundamentals of containerization by deploying an Nginx web server using Podman on Windows with a WSL2-based Linux virtual machine.

## 2. Environment

- Host OS: Windows
- Container Runtime: Podman
- Virtualization: WSL2
- Container Image: Nginx
- Image Registry: Docker Hub
- Application: Nginx Web Server
- Host Port: 8080
- Container Port: 80

## 3. Understanding the Architecture

Podman on Windows uses a Linux virtual machine to run containers.

Architecture:

Windows Host → Podman CLI → Podman Linux Machine (WSL2) → Nginx Container

The Nginx application runs inside the Linux container, while the Windows machine accesses it through the published port.

## 4. Pull the Nginx Image

Download the official Nginx image from Docker Hub.

```bash
podman pull nginx
```

Verify the downloaded image:

```bash
podman images
```

<img width="955" height="466" alt="image" src="https://github.com/user-attachments/assets/1d129e48-b0dc-4470-928d-3a15d70b4c50" />

## 5. Create and Run the Container

Create and start an Nginx container in detached mode.

```bash
podman run -d --name my-nginx -p 8080:80 nginx
```

### Command Explanation

| Option | Description |
|---|---|
| `run` | Creates and starts a container |
| `-d` | Runs the container in the background |
| `--name my-nginx` | Assigns a name to the container |
| `-p 8080:80` | Maps host port 8080 to container port 80 |
| `nginx` | Specifies the image |

## 6. Verify the Container

Check running containers:

```bash
podman ps
```

Check all containers, including stopped containers:

```bash
podman ps -a
```

Check port mapping:

```bash
podman port my-nginx
```

Expected port mapping:

```text
80/tcp -> 0.0.0.0:8080
```
<img width="955" height="196" alt="image" src="https://github.com/user-attachments/assets/5b42417c-f967-4c5b-9103-efc8671d3087" />

## 7. Access the Nginx Application

Open the following URL in a browser:

```text
http://localhost:8080
```

In my WSL2-based Podman setup, Windows localhost forwarding did not work initially.

I verified the application using the Podman machine IP address instead:

```text
http://192.168.240.45:8080
```
<img width="1890" height="826" alt="Screenshot 2026-10-31 205117" src="https://github.com/user-attachments/assets/c2ef196a-caf1-4920-b072-38524546f50f" />

To test connectivity:

```bash
curl.exe -I http://192.168.240.45:8080
```

Expected response:

```text
HTTP/1.1 200 OK
Server: nginx
```
<img width="797" height="157" alt="image" src="https://github.com/user-attachments/assets/c72f31e9-a572-4d1c-b12c-d2c3989c4532" />

Note: The VM IP address is environment-specific and may change after restarting the Podman machine. Use `podman machine inspect` and check the VM network configuration when troubleshooting connectivity.

## 8. Container Logs

View application logs:

```bash
podman logs my-nginx
```
<img width="903" height="158" alt="image" src="https://github.com/user-attachments/assets/16b2b9a5-d9dc-4526-a208-b00417310bfa" />

The logs confirmed that Nginx completed its configuration and started its worker processes successfully.

## 9. Inspect Container Configuration

View detailed container information:

```bash
podman inspect my-nginx
```

View CPU and memory usage:

```bash
podman stats --no-stream my-nginx
```

View processes running inside the container:

```bash
podman top my-nginx
```
<img width="854" height="203" alt="image" src="https://github.com/user-attachments/assets/35174169-faca-4cc7-8bbd-8fe2b1a78976" />
<img width="950" height="250" alt="image" src="https://github.com/user-attachments/assets/8218cbf0-8a92-495e-9c73-86e808728245" />

## 10. Stop the Container

Stop the running container:

```bash
podman stop my-nginx
```

Verify:

```bash
podman ps
```

The container should no longer appear in the running containers list.
<img width="955" height="168" alt="image" src="https://github.com/user-attachments/assets/486dc0fb-1746-42b1-bf9a-9b832e295d5b" />

## 11. Start the Existing Container Again

Start the previously created container:

```bash
podman start my-nginx
```

Verify:

```bash
podman ps
```

## 12. Restart the Container

```bash
podman restart my-nginx
```

## 13. Remove the Container

Stop the container first:

```bash
podman stop my-nginx
```

Remove it:

```bash
podman rm my-nginx
```

Verify removal:

```bash
podman ps -a
```
<img width="953" height="335" alt="image" src="https://github.com/user-attachments/assets/53f2e783-6a20-4b39-994a-351e88e82f40" />

## 14. Complete Command Reference

| Command | Purpose |
|---|---|
| `podman pull nginx` | Download the Nginx image |
| `podman images` | List downloaded images |
| `podman run` | Create and start a container |
| `podman ps` | List running containers |
| `podman ps -a` | List all containers |
| `podman port` | Display port mappings |
| `podman logs` | View container logs |
| `podman inspect` | Inspect container configuration |
| `podman stats` | Monitor resource usage |
| `podman top` | View container processes |
| `podman stop` | Stop a container |
| `podman start` | Start an existing container |
| `podman restart` | Restart a container |
| `podman rm` | Remove a container |
| `podman rmi` | Remove an image |

## 15. Key Learnings

Through this practical exercise, I learned:

1. What containerization is and why it is used in DevOps.
2. The difference between container images and containers.
3. How to pull images from Docker Hub.
4. How to create and run containers using Podman.
5. How port mapping works between the host and container.
6. How to access containerized applications through a browser.
7. How to inspect containers and troubleshoot application connectivity.
8. How to view container logs and resource utilization.
9. How to manage the container lifecycle using start, stop, restart and remove commands.
10. How Podman uses a Linux virtual machine to run containers on Windows.

## 16. Conclusion

Successfully deployed an Nginx web server using Podman on a Windows machine with WSL2.

Verified that the container was running, confirmed Nginx returned an HTTP 200 response, investigated host-to-VM networking issues, and practiced essential container lifecycle management commands.

**Status: First Podman container deployment completed successfully.**
