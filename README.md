# LocalAI setup
This instance of [LocalAI](https://localai.io/) has an nginx gateway running in front to perform TLS termination


## Setup

### Create credentials
Prepare a `.env` file. `API_KEY` is used to secure the LocalAI endpoint

The `.env` file should look like this
```toml
API_KEY=<RANDOM_ALPHANUMERIC_STRING>
```

### Generate self-signed certificates
You can use this command to generate self-signed certificates in [nginx/ssl](./nginx/ssl)

Replace the Common Name(CN) and Subject Alternate Name (SAN) as necessary)
```bash
openssl req -x509 -newkey rsa:4096 -sha256 -days 3650 \
  -nodes -keyout nginx/ssl/ca.key -out nginx/ssl/ca.crt -subj "/CN=example.com" \
  -addext "subjectAltName=DNS:example.com,DNS:*.example.com,IP:10.0.0.1"
```

Install the certificate using these commands for Ubuntu
```bash
sudo apt-get install -y ca-certificates
sudo cp nginx/ssl/ca.crt /usr/local/share/ca-certificates
sudo update-ca-certificates
```

### Start 'er up
Start the LocalAI container in detached mode
```bash
docker compose up --detach
```

### Set credentials
If you set `API_KEY` in [docker-compose.yaml](./docker-compose.yaml), to connect to the endpoint, you must set the same for `OPENAI_API_KEY`
```bash
export OPENAI_API_KEY="<API_KEY>"
```

### Connect to HTTP endpoint
The server HTTP endpoint will be available at `http://localhost:9998/`

Get list of models
```bash
curl --header "X-API-Key: $OPENAI_API_KEY" http://localhost:9998/models
```

### Connect to the HTTPS endpoint
The server HTTP endpoint will be available at `http://localhost:9999/`

Get list of models
```bash
curl --header "X-API-Key: $OPENAI_API_KEY" http://localhost:9999/models
```

## Tear down
```bash
docker compose down
```


