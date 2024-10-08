# Docker Flask Ngrok Proxy

A simple example of a Dockerized Flask application using Ngrok to expose the local server to the internet, with a proxy integration to help mitigate potential Ngrok connection issues.

## Features

* **Flask Application**: Run a simple Flask server inside Docker.
* **Ngrok Tunnel**: Automatically expose your local Flask server using Ngrok.
* **WProxy Proxy**: Proxy the Ngrok URL via WProxy.net to prevent connection issues (e.g., access limitations from specific networks).

## Prerequisites

* Docker and Docker Compose installed.
* A valid Ngrok authtoken (can be generated by creating an account on Ngrok).

## Project Structure

* `.env`: Contains environment variables for the Ngrok authtoken.
* `app.py`: The main Flask application.
* `docker-compose.yml`: Docker Compose configuration to define services and environment.
* `Dockerfile`: Builds a Docker image with Python, Flask, and Ngrok installed.
* `requirements.txt`: Python package requirements.
* `start.sh`: A script that starts the Flask server, Ngrok, and retrieves the public Ngrok URL.

## Getting Started

### Step 1: Clone the Repository

```sh
git clone <https://github.com/mdeacey/docker-flask-ngrok-proxy.git>
cd docker-flask-ngrok-proxy
```

### Step 2: Set up Environment Variables

Create a `.env` file in the root of your project, or use the existing one, and set your Ngrok authtoken:

```env
NGROK_AUTHTOKEN=your_ngrok_auth_token_here
```

Replace `your_ngrok_auth_token_here` with your actual Ngrok authtoken.

### Step 3: Run Docker Compose

Use Docker Compose to build and run the Flask application:

```sh
docker-compose up --build
```

This will:
* Build the Docker image.
* Run the Flask application.
* Start an Ngrok tunnel and output the accessible URL.

### Step 4: Access the Application

The application is exposed to the internet through a proxied Ngrok URL. You'll see an output like:

```sh
Ngrok is now exposing your Flask app via WProxy.net. Access it at: https://sv1.wproxy.info/proxy.php/<ngrok_url>
```

You can access the Flask application by copying and pasting the given URL into your browser.

## Use of Proxy

Ngrok can sometimes be blocked by certain networks, or connections might be limited. By using WProxy.net, the Ngrok URL is proxied, making it more accessible, even if the original Ngrok URL has issues.

For example, if you can only access Ngrok via mobile networks, this proxy provides an alternative way to access your application across devices and network types.

## Notes

* **Ports**: The Flask application runs on port `5000`, and Ngrok on port `4040` for inspecting tunnel details. Ensure these ports are available on your local machine.
* **Customizing Flask App**: You can modify `app.py` to extend your application.
* **Ngrok Dashboard**: Visit `http://localhost:4040` to view Ngrok's web interface for more information on the tunnel.

## Stopping the Application

To stop the Flask server and Ngrok tunnel:

```sh
docker-compose down
```

## Troubleshooting

* If you are unable to access the Ngrok URL, try using the proxied URL as mentioned above.
* Ensure your Ngrok authtoken is correctly set in the `.env` file.
* Check the Ngrok logs for details (`docker-compose logs`).

## License

This project is licensed under the MIT License.