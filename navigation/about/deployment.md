---
layout: post
title: Deployment Blog
description: Team Frostbyte Deployment Blog
menu: nav/about.html
permalink: /about/deployment
author: Risha, Aranya, Abby, Ava, Elliot, Shriya
comments: true
---
<style>
        .carousel-container {
            display: flex;
            overflow-x: auto;
            gap: 20px;
            padding: 10px;
            white-space: nowrap;
            scroll-snap-type: x mandatory;
        }
        .carousel-item {
            width: 150px;
            height: 150px;
            object-fit: cover;
            cursor: pointer;
            border-radius: 10px;
            scroll-snap-align: center;
        }
        .text-item {
            font-size: 24px;
            font-weight: bold;
            display: flex;
            align-items: center;
            justify-content: center;
            width: 150px;
            height: 150px;
        }
        .fullscreen-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }
        .fullscreen-container img {
            max-width: 90%;
            max-height: 90%;
            border-radius: 10px;
        }
</style>

## Operating Structure of Our Backend Database

<img src="{{ site.baseurl }}/images/deployment_page/AWSDeploy_New.png" alt="Backend Diagram">

<div class="carousel-container">
<div class="text-item">RISHA</div>
<img src="{{ site.baseurl }}/images/deployment_page/risha_frontend.png" class="carousel-item" onclick="openFullscreen(this.src)">
<img src="{{ site.baseurl }}/images/deployment_page/risha_code.png" class="carousel-item" onclick="openFullscreen(this.src)">
<div class="text-item">SHRIYA</div>
<img src="{{ site.baseurl }}/images/deployment_page/shriya_frontend.png" class="carousel-item" onclick="openFullscreen(this.src)">
<img src="{{ site.baseurl }}/images/deployment_page/shriya_code.png" class="carousel-item" onclick="openFullscreen(this.src)">
<div class="text-item">AVA</div>
<img src="{{ site.baseurl }}/images/deployment_page/ava_code.png" class="carousel-item" onclick="openFullscreen(this.src)">
<img src="{{ site.baseurl }}/images/deployment_page/ava_frontend.png" class="carousel-item" onclick="openFullscreen(this.src)">
<div class="text-item">ELLIOT</div>
<img src="{{ site.baseurl }}/images/deployment_page/elliot_code.png" class="carousel-item" onclick="openFullscreen(this.src)">
<img src="{{ site.baseurl }}/images/deployment_page/elliot_frontend.png" class="carousel-item" onclick="openFullscreen(this.src)">
<div class="text-item">ABBY</div>
<img src="{{ site.baseurl }}/images/deployment_page/abby_code.png" class="carousel-item" onclick="openFullscreen(this.src)">
<img src="{{ site.baseurl }}/images/deployment_page/abby_frontend.png" class="carousel-item" onclick="openFullscreen(this.src)">
<div class="text-item">ARANYA</div>
<img src="{{ site.baseurl }}/images/deployment_page/aranya_code.png" class="carousel-item" onclick="openFullscreen(this.src)">
<img src="{{ site.baseurl }}/images/deployment_page/aranya_frontend.png" class="carousel-item" onclick="openFullscreen(this.src)">

</div>

<!-- Fullscreen Image Container -->
<div id="fullscreen-view" class="fullscreen-container" style="display: none;" onclick="closeFullscreen()">
    <img id="fullscreen-img" src="" alt="">
</div>

<script>
    function openFullscreen(src) {
        document.getElementById("fullscreen-img").src = src;
        document.getElementById("fullscreen-view").style.display = "flex";
    }

    function closeFullscreen() {
        document.getElementById("fullscreen-view").style.display = "none";
    }
</script>


Our project is structured to provide a seamless integration between the frontend and backend. Below is an outline of the current repository setup, including subdomains, and frontend/backend port configuration.

**Backend:** Our backend repository is Flask based and runs on the port 8887 which is used for API requests and is the port we use to test it in postman. It is responsible for processing data, interactign with the database, and sending responses to frontend (JSON). The backend contains each of our APIs under the folder .py which all work through our main.py. Each of our APIs has a corresponding model under the model folder.

**Frontend:** Our frontend communicates the backend through RESTful APIs. The frontend runs on 4887 and sends HTTP requests to the backend. Our frontend is configured to fetch data from backend, process user data, then display it. The frontend 4887 sends API requests to the backend 8887. The backend processes the request, and interacts with the database. The frontend then updates the user interface based on the request.

### **How our Features Interact with the Frontend and Backend**
- REVIEW FEATURE: The backend API handles CRUD operations for the Review model, allowing users to create, read, update, and delete reviews through routes like /api/review. The frontend interacts with these endpoints by sending HTTP requests, such as POST for creating reviews and GET for fetching them, often passing a JWT token for authentication. The backend processes these requests, interacting with the database via SQLAlchemy and returning relevant data to the frontend.

- GEMINI API: The Gemini API integrates with Google Generative AI to provide a chatbot that generates camping-related advice based on user inputs. When a user sends a message, the backend uses the AI model to generate a response, updates the conversation history, and stores both the user input and AI response in the database. The backend supports CRUD operations, allowing users to interact with the chatbot, update messages, and delete them via HTTP requests, while maintaining a persistent chat session.

- QUIZ API: This Flask API handles quiz result submissions, retrieval, updates, and deletions for users, storing the data in the quiz_results table linked to the Frostbyte user model. The frontend sends requests to the /api/quiz endpoints (via HTTP methods like POST, GET, PUT, DELETE) to interact with quiz results, while the backend processes these requests, assigning national parks based on the user's quiz score and managing the results in the database. The frontend can display the assigned national park and allow users to view, update, or delete their quiz results based on their interaction with the API.

- LOCATION API: The Location API allows the frontend to manage user-specific location data, including storing, retrieving, and deleting location information linked to users and channels. It provides endpoints for creating and updating locations, fetching a user's location by their ID and channel, and deleting specific location records by ID. The backend uses SQLAlchemy to interact with the Location model, which stores location data in the database and ensures that each user's location is properly tracked, while utilizing JWT token-based authentication.

- ANALYTICS API: The Analytics API allows the frontend to send and retrieve analytics data related to user reviews, such as star ratings for specific channels. Users can submit individual or bulk analytics entries, which are stored in the database, while the frontend can also request an overall summary of average ratings and review counts for each channel. The backend ensures proper validation and error handling for all requests, and provides CRUD operations for managing analytics data, which is stored in the Analytics model and can be queried for reporting purposes.

- POST API: The Post API allows the frontend to create, update, retrieve, and delete posts associated with specific channels and users. The backend handles these requests by interacting with the Post model, which is stored in a SQL database using SQLAlchemy, ensuring each post has a title, comment, content, and references to the user and channel. Through CRUD operations, the frontend can send requests to create posts, view individual or multiple posts, or delete posts, with responses being returned in JSON format for seamless integration with the frontend interface.


**Subdomain** To ensure that the frontend can communicate with the backend during development, we configure Cross-Origin Resource Sharing (CORS). Since the frontend and backend are running on different ports, we need to explicitly allow the frontend to make requests to the backend. CORS Configuration in Flask: The Flask backend is configured to allow requests from the frontend port (127.0.0.1:4887). This ensures that the browser doesn’t block the API requests due to cross-origin restrictions.



### **Ideal final project**

<<<<<<< HEAD
-> Host both the Flask backend and frontend on an AWS EC2 instance, ensuring communication between the two. The deployment should support:  
  
Scalability: Handling Multiple Users Efficiently

    Using multiple workers in gunicorn helps process several requests at the same time, preventing slowdowns.
    Running background tasks with Celery and Redis keeps the main app responsive by handling time-consuming jobs separately.
    Scaling the backend horizontally (adding more instances) using Docker or Kubernetes helps handle more users without overloading a single server.
    Optimizing database performance with connection pooling and caching makes sure queries run quickly, even with many users.

Security: Protecting Data and Access

    Setting up firewall rules blocks unwanted traffic and restricts access to only necessary services.
    Enabling SSL/TLS encryption ensures data sent between users and the server is secure.
    Using JWT tokens, API keys, or OAuth controls who can access different parts of the app.
    Running the app in a secure Docker container with limited permissions reduces security risks.

Reliability: Keeping the Backend Running Smoothly

    Automated deployment with tools like GitHub Actions ensures updates happen without breaking the app.
    Setting up logging and monitoring with tools like Prometheus or Logstash helps track errors and performance issues in real time.
    Using backup strategies and automatic rollbacks prevents downtime in case of failures.

Domain Integration: Routing Traffic Properly

    Setting up a subdomain (e.g., flask2025.nighthawkcodingsociety.com) makes the backend easier to access and keeps it organized.
    Using a reverse proxy (like Nginx) can help direct traffic efficiently while improving security.
    Configuring DNS settings correctly ensures that users can reach the backend without connection issues.


### Deployment Process

Deployment Process Using Docker & Cockpit for a GitHub Pages Frontend & Backend Site

    Prepare the Backend (Flask + Docker)
        Create a Dockerfile in the backend directory to containerize the Flask app.
        Ensure gunicorn is set up to serve the app on a specified port (e.g., 8087).
        Build and test the Docker image locally:

        docker build -t my-backend .
        docker run -p 8087:8087 my-backend

        Push the image to a container registry (e.g., Docker Hub or GitHub Container Registry).

    Deploy the Backend with Cockpit
        Access Cockpit on the server (Cockpit is a web-based Linux server manager).
        Use Podman (or Docker) inside Cockpit to pull and run the backend container.
        Set up the container to restart automatically and expose the correct port.
        Use Nginx or Apache as a reverse proxy to route traffic properly to the backend.

    Set Up the Frontend on GitHub Pages
        Ensure the frontend (static files) is inside the docs/ folder or a separate repo.
        Configure the repository’s GitHub Pages settings to serve from docs/ or the main branch.
        Update frontend API requests to use the correct backend URL (e.g., https://flask2025.nighthawkcodingsociety.com).

    Domain & Traffic Management
        Set up DNS records to point your custom domain and subdomain to GitHub Pages (frontend) and Cockpit (backend).
        Configure HTTPS (SSL/TLS) for both frontend and backend using GitHub’s built-in SSL for Pages and Let's Encrypt for the backend.

    Monitoring & Updates
        Use Cockpit’s logs and performance metrics to monitor the backend.
        Automate deployment with GitHub Actions to update the backend when pushing new changes.

This setup ensures a smooth deployment process, with GitHub Pages serving the frontend and Docker + Cockpit managing the backend efficiently. 🚀


# Deployment Process

### Frontend and Backend Setup: Port 8102

We have set the following configuration in config.yml in frontend: 

<code>```yml
Server: https://frostbyte.stu.nighthawkcodingsociety.com/
Domain: nighthawkcodingsociety.com
Subdomain: frostbyte.stu
```</code>

In assets/api/config.js, we set: 

<code>
  export var pythonURI;
  if (location.hostname === "localhost" || location.hostname === "127.0.0.1") {
      pythonURI = "http://localhost:8102";  // Same URI for localhost or 127.0.0.1
  } else {
      pythonURI = "https://frostbyte.stu.nighthawkcodingsociety.com";
  }
</code>

In the backend, we set these configurations: 

- main.py

    <code>
      if __name__ == "__main__":
          # change name for testing
          app.run(debug=True, host="0.0.0.0", port="8102")
    </code>

- Dockerfile

      <code> 
      FROM docker.io/python:3.11

      WORKDIR /
      RUN apt-get update && apt-get upgrade -y && \
          apt-get install -y python3 python3-pip git
      COPY . /

      RUN pip install --no-cache-dir -r requirements.txt
      RUN pip install gunicorn

      ENV GUNICORN_CMD_ARGS="--workers=1 --bind=0.0.0.0:8102"

      EXPOSE 8102
      ENV FLASK_ENV=production

      CMD [ "gunicorn", "main:app" ] 
      </code>

- docker-compose.yml

    <code>      
          version: '3'
          services:
                  web:
                          image: frostbyte
                          build: .
                          env_file:
                                  - .env
                          ports:
                                  - "8102:8102"
                          volumes:
                                  - ./instance:/instance
                          restart: unless-stopped
    </code>

- nginx_file 

    <code>
      server {
          listen 80;
          listen [::]:80;
          server_name frostbyte.stu.nighthawkcodingsociety.com;

          location / {
              proxy_pass http://localhost:8102;

              # Preflighted requests
              if ($request_method = OPTIONS) {
                  add_header "Access-Control-Allow-Credentials" "true" always;
                  add_header "Access-Control-Allow-Origin"  "https://nighthawkcoders.github.io" always;
                  add_header "Access-Control-Allow-Methods" "GET, POST, PUT, DELETE, OPTIONS, HEAD" always;
                  add_header "Access-Control-Allow-MaxAge" 600 always;
                  add_header "Access-Control-Allow-Headers" "Authorization, Origin, X-Origin, X-Requested-With, Content-Type, Accept" always;
                  return 204;
              }
          }
      }
    </code>



### How We Will Set UP AWS: 

1. Login with provided credentials
2. Clone our backend repo: (blackstar3092/frostbyte_backend)
3. Our .env file will contain our passwords and Gemini API key, and we will initialize our database with ./scripts/db_init.py
4. To build the docker environment: docker-compose build & docker-compose up -d
5. Finally, we will test our server with curl
        docker ps # looking for port 8102
        curl localhost:8102

Next, we will set up our domain on Route53 (domain will be frostbyte.flask.nighthawkscsp.com) and test DNS through WSL.

Finally, we have already set up Nginx on our backend; we will work on setting it up on the AWS server to function with our backend database, as well as setting up Certbot for authentication. 


### Notes from Deployment Tech Talk

#### AWS EC2 Instance:

- In hosted zones: domains are listed (the ones under stu.nighthawkcodingsociety.com is the place to create)
- A-type DNS records: Map record name directly to an IP address
- NS: maps to a name service (DNS Lookup sites) --> Database of names to IPs
- IP address needed: 3.129.120.200
- Nginx configuration file: listener for internet
- We need a .env file (with passwords and our gemini key)
- consider creating another user
- Instance is kept outside of virtual machine so the database doesn't clear upon every restart of the virtual machine




**CollegeBoard Main Ideas**


Understanding Computing Systems

Components of a Computing System: A computing system is made up of hardware and software 

components that work together to perform tasks.

Hardware: Physical devices such as processors (CPU), memory (RAM), 

storage, input/output devices, etc.

Software: Programs and applications that tell the hardware what to do, 

such as operating systems, applications, and system software.

Operating Systems: Understand how the operating system manages hardware 

resources and provides an interface for users and other programs. Key tasks

 include memory management, process scheduling, file management, etc.



2. Computer Networks

Basic Network Types:

Local Area Network (LAN): A network that connects devices in a limited area, 

like a home or office.
Wide Area Network (WAN): A network that spans a larger geographical area, such as the internet.

Wireless Networks: Networks that allow devices to connect without physical cables, 

such as Wi-Fi and cellular networks.

Network Communication:

Data Transmission: Understanding how data is sent across networks in the form

 of packets and how devices communicate over these networks.
Protocols: Rules or standards that define how devices communicate. Examples include:
TCP/IP (Transmission Control Protocol/Internet Protocol) is fundamental for communication on the Internet.
HTTP/HTTPS for web browsing and communication between servers and clients.
DNS (Domain Name System) for translating domain names to IP addresses.
Wi-Fi, Bluetooth for local wireless communication.
3. Data Transmission and Networking Models
Packet Switching: Data is broken into smaller packets that are sent across the network independently and reassembled at the destination. This approach allows for efficient and flexible use of network resources.
Client-Server Model: In this model, clients (devices) send requests to servers (computers providing services) and receive responses.
Peer-to-Peer Networks (P2P): Devices act as both clients and servers, sharing resources directly without a central server.
Bandwidth and Latency:
Bandwidth refers to the amount of data that can be transmitted in a given time frame.
Latency refers to the delay before a transfer of data begins following an instruction.
Transmission Medium: The physical or wireless medium through which data travels, such as fiber optics, coaxial cables, or radio waves for wireless communication.
4. Internet and Its Impact
The Internet: A vast network of networks that connects millions of computing devices worldwide. The Internet is built on top of TCP/IP protocols and is essential for web browsing, email, and many modern applications.
The Web and Websites: The web is a collection of websites accessible over the internet, utilizing protocols like HTTP/HTTPS for communication.
Cloud Computing: A model where data and applications are stored on remote servers (the cloud) and accessed via the internet, offering flexibility and scalability.
5. Security and Privacy in Networks
Security Threats: Networks and computing systems are vulnerable to various security threats, such as:
Malware: Software designed to harm or exploit systems (viruses, worms, ransomware).
Phishing: Scams that trick individuals into revealing sensitive information.
Denial of Service (DoS) attacks: Attacks aimed at overwhelming a network or system to make it unavailable to users.
Encryption: Protecting data by converting it into an unreadable format using cryptography, ensuring privacy and security in communication.
SSL/TLS: Protocols for securing data transfer over the web (HTTPS).
Firewalls: Systems that monitor and control incoming and outgoing network traffic based on predetermined security rules.
6. Impact of Networks and Computing Systems
Global Connectivity: The internet connects the world, enabling global communication, collaboration, and access to resources.
Distributed Computing: Computing tasks are shared across multiple computers in a network (e.g., cloud computing, distributed databases).
Internet of Things (IoT): Refers to the interconnection of everyday physical devices (such as smart thermostats, wearables, etc.) via the internet, allowing them to collect and exchange data.
Ethical Considerations: The use of computing systems and networks raises important ethical questions regarding:
Privacy: Protecting users’ personal data.
Accessibility: Ensuring equitable access to technology and networks.
Digital Divide: Addressing inequalities in access to computing and network resources.
Key Concepts to Remember:
IP Address: A unique identifier for a device on a network.
HTTP vs HTTPS: HTTP is unencrypted, while HTTPS ensures encrypted communication over the web.
Network Topology: The physical or logical arrangement of devices in a network (e.g., star, bus, mesh).
Cloud Computing: A computing model where services are delivered over the internet, often in a scalable, on-demand way.
DNS: A system for translating human-readable domain names into machine-readable IP addresses.

### Updating our Site

In order to make changes to our site, we will follow the following process:

1. Make changes in our VSCode to the repository. Each change (to either the frontend or backend) will be tested thoroughly using `make` or `docker-compose up`
2. Each change will be documented by Elliot and Abby to the respective running documents for frontend-backend integration. This way, we will be able to track and find potential errors in previous commits.
3. Finally, we will commit to the deployed site. Through the cockpit terminal, we will first shut down our server, git pull, then restart the server to ensure changes are deployed. 

### Certbot Config

We are able to make the site secure with https using certbot.
in the terminal, run this command: <code>sudo certbot --nginx</code>
if the command is successful, then our site will be https.
otherwise, we must follow the prompt given.



NATM COLLEGEBOARD REQUIREMENTS

The project we created is linked to College Board's Big Idea 4 in a few key ways.  

Big Idea 4 which is computing systems and networks, focuses on using computing to innovate and create solutions to problems.

By building our various APIs, we have created a platform that encourages user interaction and feedback. Our site is 

innovative because it allows visitors to contribute their experiences, which can help future visitors make informed decisions about which park to visit along 

with taking a quiz to find out which park is right for you.

Our project involves the design and development of multiple components, including the interface, user experience (UX), and backend logic for the apis 

including post, analytics, our quiz, reviews, stars, location, and google gemini. Each of these have a database table that display dynamic content  

demonstrating knowledge of algorithms and data structures. Deploying our project using AWS EC2 aligns with College Board's Big Idea 4 (Creating and 

Innovating) by demonstrating how our site is accessible in the real world, allowing users to interact with and benefit from our 

application.
