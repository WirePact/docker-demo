# Application Demo for WirePact

This repository contains a demo application setup for WirePact, supported
by Docker. The idea is to show the use-case of WirePact and have it
runnable in a few minutes.

The demo application consists of two services, a frontend and a backend.
The frontend will call the backend application with an API request
and the backend will respond with a JSON response.

To run the demo application, please follow these steps:

- Start Docker
- Use `docker-compose up` to start all containers
- Go to http://localhost:8080 to see the frontend for the APP
- Go to http://localhost:9090 to see the frontend for the "Contract Repository"

Now, when pressing the "Send Request" button, the call will fail. The reason
being that the API has another PKI than the frontend. To create a successful
connection between APP and API, we need a contract.

Go to the "Contract Repository" frontend and create a new contract.
You may add the PKI CA certificates by hand or via API call. To add
them by hand, get the public certificates from your file system (that were
created when starting the containers) and copy them into the text field.
To add them via API call, use the according button and use the following
urls to fetch the ca certificates via API: `http_proxy/pki-alice:8080` and
`http_proxy/pki-bob:8080`.

When both parties (PKIs) are in the contract, you can give it a name and
save the contract. Note that the contract will be created in the file system.

When reloading the envoy app instance and the contract provider for the
app (`docker-compose restart envoy-app provider-app`) the
new certificate chain will be loaded by envoy and the call will be successful.
