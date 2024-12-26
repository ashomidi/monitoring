Let’s get started with installing Prometheus and Grafana on your **Ubuntu system**, building dashboards, and integrating with your infrastructure. Here’s a step-by-step guide:

***

### **Step 1: Install Prometheus**

1. **Download Prometheus**:
   
   ```bash
   wget https://github.com/prometheus/prometheus/releases/download/v2.47.0/prometheus-2.47.0.linux-amd64.tar.gz
   ```

2. **Extract the Archive**:
   
   ```bash
   tar -xvf prometheus-2.47.0.linux-amd64.tar.gz
   cd prometheus-2.47.0.linux-amd64
   ```

3. **Run Prometheus**:
   
   ```bash
   ./prometheus --config.file=prometheus.yml
   ```
   
   Open your browser at `http://localhost:9090` to access the Prometheus UI.

4. **(Optional) Create a Systemd Service for Prometheus**:
   
   Create a service file:
   
   ```bash
   sudo nano /etc/systemd/system/prometheus.service
   ```
   
   Add the following:
   
   ```ini
   [Unit]
   Description=Prometheus
   After=network.target
   
   [Service]
   User=root
   ExecStart=/path-to-your-prometheus/prometheus --config.file=/path-to-your-prometheus/prometheus.yml
   Restart=always
   
   [Install]
   WantedBy=multi-user.target
   ```
   
   Reload and start the service:
   
   ```bash
   sudo systemctl daemon-reload
   sudo systemctl start prometheus
   sudo systemctl enable prometheus
   ```

***

### **Step 2: Install Grafana**

```bash
sudo apt-get install -y software-properties-common
```

1. **Download the GPG Key for Grafana**: Run the following command to manually add the Grafana GPG key:

```bash
wget -q -O - https://packages.grafana.com/gpg.key | sudo gpg --dearmor -o /usr/share/keyrings/grafana-archive-keyring.gpg
```

2. **Update the Repository Configuration**: Add the Grafana repository using the new GPG keyring:

```bash
echo "deb [signed-by=/usr/share/keyrings/grafana-archive-keyring.gpg] https://packages.grafana.com/oss/deb stable main" | sudo tee /etc/apt/sources.list.d/grafana.list > /dev/null
```

3. **Update the Package Cache**: Refresh the package list to include Grafana packages:

```bash
sudo apt-get update
```

4. **Install Grafana**: Proceed with the installation:

```bash
sudo apt-get install grafana
```

Open your browser at `http://localhost:3000` to access the Grafana UI.
