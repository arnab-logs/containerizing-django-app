# containerizing-django-app
My hands-on journey of learning how to containerize a Django app using Docker — from writing a Dockerfile to running the app on localhost, with real mistakes and fixes along the way.

---

# Containerizing a Django Web App Using Docker

This project demonstrates how to containerize a Django application from scratch using Docker. It’s not just a working container — it's an educational deep dive into how Docker works under the hood when packaging a real-world Python web application.

Whether we're exploring DevOps, backend engineering, or full-stack development, this repository showcases key concepts like:

- Writing a clean, production-ready `Dockerfile`
- Installing and managing Python dependencies securely
- Understanding Docker image layers and virtual environments
- Running containers with proper networking and port mapping
- Avoiding common pitfalls (like missing ports or system-wide installs)

---

## Project Overview

This is a basic Django app — already set up and functional. The focus of this repo is **containerization**, not Django development.

### Key Features:

- Simple Django app with a view that returns an HTML page
- URL path routed via `/demo/`
- Custom `requirements.txt` for dependency management
- Virtual environment created inside the Docker container
- Clean `Dockerfile` with Bash shell configuration
- Exposed port and run commands clearly defined

---

##  Technologies Used

-  Python 3
-  Django
-  pip (Python Package Manager)
-  Docker
-  Ubuntu (as base image)

---

## File Structure

```

devops/
├── manage.py
├── devops/
│   ├── settings.py
│   ├── urls.py
├── demo/
│   ├── views.py
│   ├── urls.py
│   └── templates/
│       └── demo\_site.html
requirements.txt
Dockerfile

````

---

## How to Run the Project Locally Using Docker

### 1. Clone the Repo

```bash
git clone https://github.com/arnab-logs/containerizing-django-app.git
cd containerizing-django-app
````

### 2. Build the Docker Image

```bash
docker build -t django-container .
```

> This step uses the `Dockerfile` to create a custom image with Python, Django, and all dependencies installed in a virtual environment inside the container.

### 3. Run the Container

```bash
docker run -p 8000:8000 django-container
```

> The `-p` flag maps container port 8000 to your localhost port 8000, making the app accessible via your browser.

### 4. Open in Browser

Visit: [http://localhost:8000/demo](http://localhost:8000/demo)

> You’ll see a simple HTML page with LinkedIn and blog links, and a message that says:
>
> *“Learning to Containerize Django App Using Docker”*

---

## What I Learned

This project wasn’t just about getting a Django app to work — it was about learning *why* certain things matter in containerization. Here are a few key takeaways:

* Why system Python installs can fail in Docker (PEP 668 errors)
* How virtual environments solve system dependency issues
* The importance of switching to `bash` shell inside Docker for `source` to work
* Why port forwarding is essential (`-p 8000:8000`)
* How to interpret Django URL routing inside containers (`/demo/` path)

Check the blog for detailed explanations and lessons learned!

---

## Dockerfile Highlights

```Dockerfile
FROM ubuntu
WORKDIR /app

COPY requirements.txt /app/
COPY devops /app/

RUN apt-get update && apt-get install -y python3 python3-pip python3-venv

SHELL ["/bin/bash", "-c"]

RUN python3 -m venv venv1 && \
    source venv1/bin/activate && \
    pip install --no-cache-dir -r requirements.txt

EXPOSE 8000

CMD source venv1/bin/activate && python3 manage.py runserver 0.0.0.0:8000
```

This `Dockerfile` is intentionally built from the ground up using a base `ubuntu` image to showcase what it takes to install and configure Python and Django manually — rather than relying on prebuilt `python` base images.

<!-- 
---
## Related Blog Post

📖 [Full Blog Walkthrough](https://your-blog-link.com) — includes breakdowns, code snippets, screenshots, mistakes I made, and why each Docker command matters.

---
-->

## About Me

* [LinkedIn](www.linkedin.com/in/arnab-nandi-55232a236) 
* [Blog](https://learning-out-loud-my-devops-journey.hashnode.dev/)

---

```


