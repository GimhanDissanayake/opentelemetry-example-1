# Open Telemetry Example using docker and flask app

## Server setup (Ubuntu)
```bash

# install docker
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh ./get-docker.sh

# other tools
sudo apt install unzip
sudo apt install net-tools

## start otel, jaeger, prometheus, grafana
docker compose up --force-recreate --remove-orphans --detach # view logs: docker compose logs -f
```

## [Example Application to send traces](https://opentelemetry.io/docs/languages/python/getting-started/)
```bash
mkdir otel-getting-started
cd otel-getting-started
python3 -m venv venv
source ./venv/bin/activate

pip install flask
pip install opentelemetry-distro
opentelemetry-bootstrap -a install
pip install opentelemetry-exporter-otlp

# Run the application
export OTEL_PYTHON_LOGGING_AUTO_INSTRUMENTATION_ENABLED=true
opentelemetry-instrument --logs_exporter otlp flask run -p 8080

curl http://localhost:8080/rolldice
```

## Check Jaeger UI
```bash
ssh -i private_key.pem -L 16686:localhost:16686 ubuntu@IP_ADDR

curl http://localhost:16686
```