# Setting Up NATS Server

```bash
# Download and Extract NATS Server
wget https://github.com/nats-io/nats-server/releases/download/v2.10.5/nats-server-v2.10.5-linux-amd64.zip
unzip nats-server-v2.10.5-linux-amd64.zip
cd nats-server-v2.10.5-linux-amd64
sudo cp nats-server /usr/local/bin

# Obtain SSL Certificate
# If a webserver is not available on your server, generate a standalone SSL certificate using Certbot.
certbot certonly --standalone -d domain.com --staple-ocsp -m email --agree-tos

# Create NATS Configuration File
sudo mkdir /etc/nats
sudo vi /etc/nats/nats.conf
# Add the following configuration to nats.conf:
# (See previous response for the configuration)

# Create NATS Systemd Service
sudo nano /etc/systemd/system/nats.service
# Add the following content to nats.service:
# (See previous response for the content)

# Reload Systemd, Enable, and Start NATS Service
sudo systemctl daemon-reload
sudo systemctl enable nats
sudo systemctl start nats

# Test NATS Server Connection
printf "PING\r\n" | nc 127.0.0.1 4433

# Install NATS CLI
# Choose one of the following methods to install the NATS CLI:
# Way 1:
curl -sf https://binaries.nats.dev/nats-io/natscli/nats@latest | sh

# Way 2:
wget https://github.com/nats-io/natscli/releases/download/v0.1.1/nats-0.1.1-386.deb
sudo dpkg -i nats-0.1.1-386.deb
nats --help

# Add NATS Context
nats context add name_config_name_here --server yourdomain:4433 --description "Give Description Here" --select
