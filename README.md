# Microsercies-based-weather-app

Microservices-based application. The implementation involves creating two microservices: one for fetching weather data and another for displaying it. The primary objectives include containerizing these microservices using Docker, deploying them to a Kubernetes cluster, and accessing them through Nginx.

---

## Hypothetical use case

We are developing a simple static website (HTML and CSS) for a company's landing page. The goal is to containerize this application using Docker, deploy it to a Kubernetes cluster, and access it through Nginx.

---

## Features

- Provides real-time weather updates.
- Built with a microservices architecture.
- Containerized with Docker for portability.
- Deployed in a Kubernetes cluster using Kind.

---

## Prerequisites

- Docker
- Kubernetes (Kind for local development)
- kubectl

---

## Tasks

### Task 1: Setup your project

- Lets create a project folder called microservices based app  
- `mkdir microservices-based-app`
- Next inside the directory, create `index.html file`, `style.css file` and if you would like to add some interactivity to your app, you can add a `script.js file`

---

### HTML

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Gbenga and Sons</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <header>
    <div class="logo">Gbenga & Sons</div>
    <nav>
      <ul>
        <li><a href="#home">Home</a></li>
        <li><a href="#services">Services</a></li>
        <li><a href="#about">About</a></li>
        <li><a href="#contact">Contact</a></li>
      </ul>
    </nav>
  </header>

  <section id="home" class="section">
    <h1>Welcome to Gbenga & Sons</h1>
    <p>Your trusted partner in excellence!</p>
  </section>

  <section id="services" class="section">
    <h2>Our Services</h2>
    <div class="service-list">
      <div class="service-item">Consulting</div>
      <div class="service-item">Project Management</div>
      <div class="service-item">Product Design</div>
    </div>
  </section>

  <section id="about" class="section">
    <h2>About Us</h2>
    <p>At Gbenga & Sons, we pride ourselves on delivering top-notch services tailored to meet your needs. With a team of experienced professionals, we guarantee excellence in every aspect of our work.</p>
  </section>

  <section id="contact" class="section">
    <h2>Contact Us</h2>
    <form id="contact-form">
      <label for="name">Name</label>
      <input type="text" id="name" placeholder="Your Name" required>
      
      <label for="email">Email</label>
      <input type="email" id="email" placeholder="Your Email" required>
      
      <label for="message">Message</label>
      <textarea id="message" placeholder="Your Message" required></textarea>
      
      <button type="submit">Send</button>
    </form>
  </section>

  <footer>
    <p>&copy; 2024 Gbenga and Sons. All rights reserved.</p>
  </footer>

  <script src="script.js"></script>
</body>
</html>

```

---

### CSS

```css
/* General Reset */
body, h1, h2, p, ul, li, input, textarea, button {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Arial, sans-serif;
}

body {
  background-color: #000;
  color: #fff;
  line-height: 1.6;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 20px;
  background: #222;
  position: sticky;
  top: 0;
}

header .logo {
  font-size: 24px;
  font-weight: bold;
  color: #f90;
}

header nav ul {
  list-style: none;
  display: flex;
  gap: 15px;
}

header nav ul li a {
  color: #f90;
  text-decoration: none;
}

header nav ul li a:hover {
  text-decoration: underline;
}

.section {
  padding: 20px;
  text-align: center;
}

#home {
  background: #111;
  padding: 50px;
}

#services {
  background: #222;
}

#about {
  background: #111;
}

#contact {
  background: #222;
}

.service-list {
  display: flex;
  justify-content: center;
  gap: 15px;
}

.service-item {
  background: #333;
  padding: 10px 20px;
  border-radius: 5px;
  color: #f90;
}

form {
  display: flex;
  flex-direction: column;
  gap: 10px;
  max-width: 400px;
  margin: 0 auto;
}

input, textarea, button {
  padding: 10px;
  border: none;
  border-radius: 5px;
}

input, textarea {
  width: 100%;
  background: #333;
  color: #fff;
}

button {
  background: #f90;
  color: #000;
  cursor: pointer;
}

button:hover {
  background: #ffa500;
}

footer {
  text-align: center;
  padding: 10px;
  background: #111;
}

```

---

### JS

```js
// Basic Form Submission
document.getElementById('contact-form').addEventListener('submit', function (e) {
  e.preventDefault();
  alert('Thank you for contacting Gbenga & Sons. We will get back to you soon!');
});

```

## Task 2: Initialize Git

- cd /path/to/your/project
- `git init`

## Task 3: Git commit

To commit our work we would first do:

- `git add .` This means adding all of the files to the staging area of git
- Next we would run `git commit -m "Initial commit`
- To push the code to a remote repository, we would need to open our github account
- Log into github
- Click on your repository
- Clicke on new repository
- Give the repository a descriptive name and a brief description
- Create the repository and copy the the repository git url
- Then you can push the local repository to the remote repository using the `git push` command

## Task 4: Dockerize the application

to dockerize our application, we would need to first add a dockerfile, while is essentially the blue-print for our docker image
our Dockerfile would look like this:

```yaml
# Use a lightweight Nginx image
FROM nginx:alpine

# Set the working directory
WORKDIR /usr/share/nginx/html

# Remove default Nginx static files
RUN rm -rf ./*

# Copy application files to the container
COPY . .

# Expose port 80 for the container
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]

```

---

- To oprimize our docker image , we can create a .dockerignore file to exclude unneccesary files

node_modules
*.log
Dockerfile
.dockerignore

## Building the docker image

We would build  the docker image by running.
`docker build -t gbenga-and-sons .`

- At this point the application has been built into an image named  "gbenga-and-sons"

## Task 5: Pushing the image to dockerhub

To push the image to dockerhub:

- Log in to Docker Hub
Before pushing images to Docker Hub, you need to log in using your Docker Hub credentials. Run the following command:
`docker login`
- Build Your Docker Image
Make sure you are in the project folder where the Dockerfile is located and run
`docker build -t <your-dockerhub-username>/<image-name>:<tag> .`
- For example `docker build -t kelomo2502/gbenga-and-sons:v1 .`
- Let's verify the image locally by running
  `docker images`
- After confirming the image is available on our local machine, we can push it to dockerhub by runnin `docker push <your-dockerhub-username>/<image-name>:<tag>`
- for example `docker push kelomo2502/gbenga-and-sons:v1`
We have successfully push our docker image to dockerhub
![Dokcer image pushed to dockerhub](/docke-image.png)

## Task 6: Setup Kubernetes cluster using kind

To setup a kubernetes cluster using kind, we need to first install kind

### Windows

You can install kind by running
`choco install kind` note: you need to chocolatey installed already
check the version by running `kind version`

### Macos and Linux

You can install kind by running `brew install kind` Note: you need to have homebrew installed already

## Task 7: Setting up a kubernetes cluster

After insyall kind, we would setup a kubernets cluster by running
`kind create cluster`

## Task 8: Depploying cluster

We would be deploying our kubernetes cluster using kind as follows:

- Firstyly, we would create a kubernetes manifest using yaml syntax
The first file will be deployment.yaml with the following configuration

### deployment.yaml

```yaml
  apiVersion: apps/v1

kind: Deployment
metadata:
  name: gbenga-and-sons-deployment
  labels:
    app: gbenga-and-sons
spec:
  replicas: 2
  selector:
    matchLabels:
      app: gbenga-and-sons
  template:
    metadata:
      labels:
        app: gbenga-and-sons
    spec:
      containers:
      - name: gbenga-and-sons-container
        image: kelomo2502/gbenga-and-sons:v1 # Replace with your Docker Hub image
        ports:
        - containerPort: 80 # Update with the port your app listens on

  ```

### service.yaml

```yaml
apiVersion: v1
kind: Service
metadata:
  name: gbenga-and-sons-service
spec:
  selector:
    app: gbenga-and-sons
  ports:
  - protocol: TCP
    port: 80       # Exposed port
    targetPort: 80 # The port your app listens on
  type: LoadBalancer

apiVersion: v1
kind: Service
metadata:
  name: gbenga-and-sons-service
spec:
  selector:
    app: gbenga-and-sons
  ports:
  - protocol: TCP
    port: 80       # Service port
    targetPort: 80 # Container port
  type: ClusterIP # Default type for internal services
```

```yaml
kubectl apply -f deployment.yaml

kubectl apply -f service.yaml

  ```

These two commands apply the configurations in our deployment and service manifest

- We can verify that the pod and service are running bu using:
  `kubectl get pods`
  `kubectl get service`
At this point our app has been sucessfully deployed to kubernetes cluster using kind
![Running pods](/pods.png)
![Running services](/services.png)

## Task 9: Acessing the website

Since our deployment is of type ClusterIP, the website will only be accessible internally within the pods but lets use port forwarding, so we can access the website pn our local machine by running:
`kubectl port-forward service/gbenga-and-sons-service 8080:80`
Then we can access on <http://localhost:8080>

## Author Information

👤 Author: Gbenga
GitHub: <https://github.com/kelomo2502>
LinkedIn: <https://www.linkedin.com/in/oyewunmi-gbenga/>
Email: <kelvinoye@gmail.com>
