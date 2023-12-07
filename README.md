# Build

Building the ODA Open API SDK for Golang.

# Tooling

* Install [Golang](https://go.dev/doc/install)
* Install [OpenAPI Generator](https://openapi-generator.tech/docs/installation)

# Generate

Generate a client and server for each ODA Open API.

## TMF634

```bash
$ openapi-generator-cli generate --generator-name go --output tmf634/client --additional-properties packageName=tmf634client -i https://tmf-open-api-table-documents.s3.eu-west-1.amazonaws.com/OpenApiTable/4.1.0/swagger/TMF634-ResourceCatalog-v4.1.0.swagger.json
$ openapi-generator-cli generate --generator-name go-server --output tmf634/server --additional-properties packageName=tmf634server -i https://tmf-open-api-table-documents.s3.eu-west-1.amazonaws.com/OpenApiTable/4.1.0/swagger/TMF634-ResourceCatalog-v4.1.0.swagger.json
```

## TMF639

```bash
$ openapi-generator-cli generate --generator-name go --output tmf639/client --additional-properties packageName=tmf639client -i https://tmf-open-api-table-documents.s3.eu-west-1.amazonaws.com/OpenApiTable/4.0.0/swagger/TMF639-ResourceInventory-v4.0.0.swagger.json
$ openapi-generator-cli generate --generator-name go-server --output tmf639/server --additional-properties packageName=tmf639server -i https://tmf-open-api-table-documents.s3.eu-west-1.amazonaws.com/OpenApiTable/4.0.0/swagger/TMF639-ResourceInventory-v4.0.0.swagger.json
```

## Replacement

Change GIT_USER_ID and GIT_REPO_ID:
```bash
$ sed -i "s/GIT_USER_ID\/GIT_REPO_ID/oda-components\/oda-api-sdk-go/g" tmf*/*/main.go # Replace GIT_USER_ID and GIT_REPO_ID
$ sed -i "s/GIT_USER_ID\/GIT_REPO_ID/oda-components\/oda-api-sdk-go/g" tmf*/*/go.mod  # Replace GIT_USER_ID and GIT_REPO_ID
$ sed -i "s/GIT_USER_ID\/GIT_REPO_ID/oda-components\/oda-api-sdk-go/g" tmf*/*/*/*.md  # Replace GIT_USER_ID and GIT_REPO_ID
$ sed -i '16,17d' tmf*/*/go/api_notification_listeners_client_side.go                 # Delete unused "github.com/gorilla/mux"

```

# Build & Test

## Build TMF 634 server
```bash
$ cd tmf634/server
$ go mod download github.com/gorilla/mux
$ go get github.com/oda-components/oda-api-sdk-go/go
$ go build -o .
$ go run main.go
```

## Test request to TMF 634 server
```bash
$ curl -vs -H 'Accept: application/json' http://localhost:8080/tmf-api/resourceCatalog/v4/resourceSpecification
```
