# Around Me Social Networking App Architecture Explanation

## Client Side

- **React Native App**: The main app users interact with on their phones.
- **Mapbox SDK**: Helps show maps and location info in the app.
- **APN**: Sends notifications to iPhones.
- **FCM**: Sends notifications to Android phones.

## Networking

- **LoadBalancer**: Spreads out incoming traffic to keep the app running smoothly.
- **cert-manager**: Keeps the app's security certificates up to date.
- **Ingress Controller**: Directs incoming traffic to the right places in the app.

## Kubernetes Cluster

This is where most of the app's behind-the-scenes work happens:

- **FastAPI Services**: The main entry point for handling requests from the app.
- **ArgoCD**: Helps keep the app updated with the latest code changes.
- **Machine Learning Pipelines**: Does smart calculations to improve user experience.
- **Neo4j**: A special database that's good at handling connections between users.
- **Elasticsearch**: Helps find information quickly.
- **Logstash**: Collects and organizes app logs.
- **Kibana**: Shows pretty charts and graphs of app data.
- **Redis Master**: A fast database for temporary information.
- **Qdrant**: Another database for specific types of searches.

## Redis Slaves

These help the Redis Master handle lots of requests:

- **Redis Slave 1, 2, and 3**: Copies of Redis Master to share the workload.

## External Services

- **Managed Postgres**: A reliable database for storing important app data.
- **msg91**: Helps send text messages to users.
- **ola krutirm**: Provides location-based services.
- **OpenAI API** and **Claude AI API**: Add smart features to the app.
- **Cloudflare R2**: Stores and serves files like photos and videos.

## CI/CD Pipeline

This is how new code gets from developers to users:

- **Developer**: The person writing new code.
- **GitHub Actions**: Automatically checks and prepares new code.
- **DockerHub**: Stores packaged versions of the app.
- **k8s-configs Repository**: Holds instructions for setting up the app.

## Background Jobs

- **Background Jobs**: Does important tasks when the app isn't busy.

## Main User Flow

1. User opens the app and sees a map.
2. App sends a request through the LoadBalancer and Ingress Controller.
3. FastAPI Services handle the request, using Elasticsearch and Machine Learning Pipelines.
4. Neo4j database provides user connection info.
5. App sends back the results to show the user.
6. If needed, notifications are sent to the user's phone.

## Other Important Connections

- Kibana connects to Elasticsearch to show data visualizations.
- ArgoCD keeps the Kubernetes Cluster updated.
- FastAPI Services can store and retrieve files from Cloudflare R2.

This setup helps the Around Me app run smoothly, handle lots of users, and provide a great experience with maps, social connections, and smart features.
