# LocalAI setup

## Setup

###
Prepare a `.env` file. `API_KEY` is used to secure the LocalAI endpoint

The `.env` file should look like this
```toml
API_KEY=<RANDOM_ALPHANUMERIC_STRING>
```

### Start 'er up
Start the LocalAI container in detached mode
```bash
docker compose up --detach
```

The server will be available at `http://localhost:9999/`

Test the endpoint
```bash
curl http://localhost:9999/models
```

## Tear down
```bash
docker compose down
```


