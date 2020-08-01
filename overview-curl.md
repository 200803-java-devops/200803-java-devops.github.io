# Using cURL
## GET
Print a GET request to stdout:
>curl <URL>

Save response from GET to file:
>curl -o <OUTPUT-FILE-NAME> <URL>

Save response from GET while keeping the name of the online file
>curl -O <URL>

## POST
POST HTML form:
>curl -d "key1=value1&key2=value2" -X POST <URL>

POST JSON form:
>curl -d '{"key1":"value1", "key2":"value2"}' -H "Content-Type: application/json" -X POST <URL>

Data can be parsed and sent from a file: 
>curl -d "@<FILE-NAME>" -X POST <URL>
