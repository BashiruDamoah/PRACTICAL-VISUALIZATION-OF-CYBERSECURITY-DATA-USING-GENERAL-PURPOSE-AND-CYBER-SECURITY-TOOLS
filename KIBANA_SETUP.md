# Elasticsearch and Kibana Setup Guide

This guide walks through installing, starting, and accessing Elasticsearch and Kibana on Ubuntu (Linux).

---

## Prerequisites

- Ubuntu 20.04 or later
- At least 4GB RAM recommended
- `sudo` privileges
- Internet connection

---

## Step 1 — Install Java (if not already installed)

Elasticsearch requires Java. Check if it is installed first:

```bash
java -version
```

If not installed:

```bash
sudo apt update
sudo apt install default-jdk -y
java -version
```

---

## Step 2 — Add the Elastic APT Repository

```bash
# Install required tools
sudo apt install apt-transport-https curl -y

# Import the Elastic GPG key
curl -fsSL https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elastic.gpg

# Add the Elastic repository
echo "deb [signed-by=/usr/share/keyrings/elastic.gpg] https://artifacts.elastic.co/packages/8.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-8.x.list

# Update package list
sudo apt update
```

---

## Step 3 — Install Elasticsearch

```bash
sudo apt install elasticsearch -y
```

---

## Step 4 — Install Kibana

```bash
sudo apt install kibana -y
```

---

## Step 5 — Configure Elasticsearch

Open the Elasticsearch configuration file:

```bash
sudo nano /etc/elasticsearch/elasticsearch.yml
```

Find and update (or uncomment) the following lines:

```yaml
network.host: localhost
http.port: 9200
```

Save and close the file (`Ctrl + O`, then `Ctrl + X`).

---

## Step 6 — Configure Kibana

Open the Kibana configuration file:

```bash
sudo nano /etc/kibana/kibana.yml
```

Find and update the following lines:

```yaml
server.port: 5601
server.host: "localhost"
elasticsearch.hosts: ["http://localhost:9200"]
```

Save and close the file.

---

## Step 7 — Start and Enable Services

Start Elasticsearch:

```bash
sudo systemctl start elasticsearch
sudo systemctl enable elasticsearch
```

Start Kibana:

```bash
sudo systemctl start kibana
sudo systemctl enable kibana
```

---

## Step 8 — Verify Services Are Running

Check Elasticsearch status:

```bash
sudo systemctl status elasticsearch
```

Check Kibana status:

```bash
sudo systemctl status kibana
```

Both should show `active (running)`.

You can also test Elasticsearch directly:

```bash
curl -X GET "http://localhost:9200"
```

Expected output:

```json
{
  "name" : "your-hostname",
  "cluster_name" : "elasticsearch",
  "version" : { ... },
  "tagline" : "You Know, for Search"
}
```

---

## Step 9 — Access Kibana in the Browser

Open your browser and navigate to:

```
http://localhost:5601
```

You should see the Kibana welcome screen.

> Note: Kibana can take 1–2 minutes to fully load after starting the service. If the page does not load immediately, wait and then refresh.

---

## Step 10 — Upload a Dataset to Kibana

1. On the Kibana home screen, click **"Integrations"** in the left sidebar.
2. Click **"Upload a file"** at the top of the page.
3. Click **"Select or drag and drop a file"** and choose your CSV file (e.g. `cybersecurity_attacks.csv`).
4. Kibana will automatically detect the file structure and show a preview.
5. Click **"Import"**.
6. Set an index name (e.g. `cybersecurity_attacks`) and click **"Import"** again.
7. Once complete, click **"View index in Discover"** to explore your data.

---

## Step 11 — Create Visualizations in Kibana

1. In the left sidebar, click **"Visualize Library"**.
2. Click **"Create visualization"**.
3. Choose a chart type (Bar, Line, Heatmap, Pie, etc.).
4. Select your index (e.g. `cybersecurity_attacks`) as the data source.
5. Configure the horizontal axis (e.g. `@timestamp`) and vertical axis (e.g. `Count of records`).
6. Add a breakdown field if needed (e.g. `Attack Type`).
7. Click **"Save"** to save the visualization to your library.

---

## Stopping the Services

To stop Elasticsearch and Kibana when not in use:

```bash
sudo systemctl stop kibana
sudo systemctl stop elasticsearch
```

---

## Troubleshooting

| Issue | Fix |
|---|---|
| Kibana not loading | Wait 1–2 minutes and refresh; check status with `sudo systemctl status kibana` |
| Elasticsearch not starting | Check logs with `sudo journalctl -u elasticsearch` |
| Port 9200 not reachable | Confirm `network.host: localhost` is set in `elasticsearch.yml` |
| Out of memory error | Increase heap size in `/etc/elasticsearch/jvm.options` or add more RAM |
| Permission denied errors | Ensure you are using `sudo` for all service commands |

---

## Quick Reference

| Action | Command |
|---|---|
| Start Elasticsearch | `sudo systemctl start elasticsearch` |
| Start Kibana | `sudo systemctl start kibana` |
| Stop Elasticsearch | `sudo systemctl stop elasticsearch` |
| Stop Kibana | `sudo systemctl stop kibana` |
| Check Elasticsearch | `curl http://localhost:9200` |
| Access Kibana | `http://localhost:5601` |
