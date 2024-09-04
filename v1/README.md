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
- **ArgoCD**: Helps update the app with the latest code changes.
- **Machine Learning Pipelines**: User recommendations are processed here for shoutouts and chitchats.
- **Neo4j**: To handle the social level of social connections between users and help in collaborative-based filtering. 
- **Elasticsearch**: Helps to perform geospatial queries to find nearby shoutouts and chitchats.
- **Logstash**: Currently not used. We are still experimenting with this.
- **Kibana**: User Interface for elastic search. Helps us to visually check with data.
- **Redis Master**: Cache data that is frequently queried. Currently, users, shoutouts and chitchats are cached.
- **Qdrant**: Database to perform vector searches. Wherein each shoutout and chitchat will be validated by AI which has knowledge awareness about our privacy and terms. This helps us to maintain platform authenticity.

## Redis Slaves

These help the Redis Master handle lots of requests:

- **Redis Slave 1, 2, and 3**: Copies of Redis Master to share the workload.

## External Services

- **Managed Postgres**: This is our primary database to store all the data.
- **msg91**: Helps in phone number OTP-based authentication.
- **ola krutirm**: Helps us to perform reverse geocoding.
- **OpenAI API** and **Claude AI API**: APIs to integrate AI in our systems.
- **Cloudflare R2**: Alternative to s3 which is cheap and reliable for storing objects.

## CI/CD Pipeline

This is how new code gets from developers to users:

- **GitHub Actions**: Whenever the developer pushes code to fastAPI action is triggered to build, push to dockerhub and make appropriate changes to k8s-config GitHub repo with the latest docker Image.
- **ArgoCD**: Whenever changes are made to the k8s-config repo, this service automates and makes appropriate changes to the Kubernetes cluster.
- **DockerHub**: Premium dockerhub subscription where we store all private Docker Images.
- **k8s-configs Repository**: All the configurations are declared here for our Kubernetes.

## Background Jobs

- **Background Jobs**: Background Jobs are maintained to expire shoutouts when they are done with declared time limit.
