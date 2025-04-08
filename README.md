# Creating a Private Container Registry on Google Cloud

## Objective
Create a private Docker registry on Google Cloud to store and manage Docker images.

## Steps

### I. Log in to Google Cloud
Open the terminal and log in to Google Cloud using:

```bash
gcloud auth login
```

After logging in successfully, select the project:

```bash
gcloud config set project PROJECT_NAME
```
### II. Enable the Artifact Registry API
Enable the Artifact Registry API:

```bash
gcloud services enable artifactregistry.googleapis.com
```

### III. Create the Private Container Registry
Create the private container registry in Google Cloud:

```bash
gcloud artifacts repositories create calculator-repo --repository-format=docker --location=australia-southeast1 --description="Docker repo for calculator microservice"
```

# 2. Authenticate with Docker Registry

## Objective
Authenticate Docker to access the private Google Cloud container registry.

## Steps

### I. Run the following command to authenticate Docker with the Google Cloud registry:

```bash
gcloud auth configure-docker australia-southeast1-docker.pkg.dev
```

Docker will update the configuration file to use the Google Cloud authentication helper for pushing and pulling images.

# 3. Publish the Docker Image to the Registry

## Objective
Push the Docker image to the private container registry created earlier.

## Steps

### I. Tag the Docker image so that it points to the newly created registry:
```bash
docker tag calculator-microservice australia-southeast1-docker.pkg.dev/PROJECT_NAME/calculator-repo/calculator-microservice:latest
```

### II. Push the tagged image to the private registry:
```bash
docker push australia-southeast1-docker.pkg.dev/PROJECT_NAME/calculator-repo/calculator-microservice:latest
```

# 4. Run the Docker Image from the Registry

## Objective
Verify that the microservice can run from the published image in the registry.

## Steps

### I. Run the Docker container from the image that was just pushed to the registry:
```bash
docker run -d -p 3000:3000 australia-southeast1-docker.pkg.dev/PROJECT_NAME/calculator-repo/calculator-microservice:latest
```
This command runs the microservice and binds it to port 3000 on your local machine.
