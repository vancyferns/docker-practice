# docker-practice

## Overview

This project demonstrates how to use Docker Compose to set up a local MongoDB database and a Mongo Express web-based admin interface. It is designed for easy startup and teardown, and includes all configuration in a single `compose.yaml` file.

## What Has Been Done

- **Created a Docker Compose file** (`internspirit-docker-tutorial/compose.yaml`) that defines two services:
	- `mongo`: Runs the official MongoDB image, exposes port 27017, and sets up an admin user.
	- `mongo-express`: Runs the official Mongo Express image, exposes port 8081, and connects to the `mongo` service using the admin credentials.
- **Configured environment variables** for both services to ensure secure and correct communication.
- **Mapped ports** so you can access MongoDB from your host at `localhost:27017` and Mongo Express at `localhost:8081` (or via the Codespaces/GitHub Codespaces port forwarding URL).

## How to Use

1. **Start the services:**
	 ```bash
	 cd internspirit-docker-tutorial
	 docker compose -f compose.yaml up -d
	 ```

2. **Access Mongo Express:**
	 - Open your browser and go to `http://localhost:8081` (or use the forwarded port URL if in Codespaces).
	 - Login with the credentials set in the compose file (`amith` / `password`).

3. **Stop and remove the services:**
	 ```bash
	 docker compose -f compose.yaml down
	 ```

## Configuration Details

- **MongoDB**
	- Username: `amith`
	- Password: `password`
	- Port: `27017`
- **Mongo Express**
	- Username: `amith`
	- Password: `password`
	- Port: `8081`
	- Connects to MongoDB using the URI: `mongodb://amith:password@mongo:27017/`

## Troubleshooting

- If Mongo Express shows a 502 error or cannot connect:
	- Make sure both containers are running: `docker ps`
	- Check logs for errors:
		- MongoDB: `docker logs mongo_container`
		- Mongo Express: `docker logs mongo_express_container`
	- Sometimes, Mongo Express may start before MongoDB is ready. Restart both services:
		```bash
		docker compose -f compose.yaml down
		docker compose -f compose.yaml up -d
		```
- If you change credentials, update them in both the `mongo` and `mongo-express` service definitions.

## File Structure

- `internspirit-docker-tutorial/compose.yaml` — Docker Compose file for MongoDB and Mongo Express
- `README.md` — This documentation

---

If you revisit this project after a long time, just follow the steps above to get MongoDB and Mongo Express running locally with Docker Compose!