# 🚀 PI-EDGE: HIGH-PERFORMANCE GO CORE

**The Lightning-Fast Hand of Sovereign Intelligence.**

---

## 🎯 Why Pi-Edge?

Pi-Edge is a standalone reconnaissance engine built in **Go**. It is designed for edge-computing, micro-servers, and low-power environments where speed is absolute.

### Performance Metrics

| Platform | Binary Size | RAM Usage | Speed |
|----------|-------------|-----------|-------|
| **Linux x64** | ~2MB | < 5MB | Instant |
| **ARM / Pi** | ~1.8MB | < 5MB | Instant |
| **Windows** | ~2MB | < 8MB | Instant |

---

## 📦 Installation

### Quick Install (3 Seconds)

```bash
# Download the optimized binary for your OS:
# https://github.com/Pi-Swarm/pi-edge-sovereign/releases

# Linux/macOS
chmod +x pi-edge-linux-amd64 && ./pi-edge-linux-amd64

# Or build from source
go build -o pi-edge main.go
```

### Build from Source

```bash
# Prerequisites
go version  # Requires Go 1.21+

# Clone
git clone https://github.com/Pi-Swarm/pi-edge-sovereign.git
cd pi-edge-sovereign

# Build
go build -ldflags="-s -w" -o pi-edge main.go

# Run
./pi-edge --help
```

---

## 🎮 How to Run

### 1. Basic Commands

```bash
# Check status
./pi-edge status

# Quick scan
./pi-edge scan 192.168.1.1

# Network discovery
./pi-edge discover 192.168.1.0/24

# Port scan
./pi-edge ports scanme.nmap.org

# Service detection
./pi-edge services 192.168.1.1
```

### 2. Advanced Usage

```bash
# Stealth scan
./pi-edge scan 192.168.1.1 --stealth --timeout 30s

# Output to file
./pi-edge scan 192.168.1.0/24 -o results.json

# Specific ports
./pi-edge scan 192.168.1.1 -p 22,80,443,8080

# Fast mode
./pi-edge scan 192.168.1.0/24 --fast

# Verbose
./pi-edge scan 192.168.1.1 -v
```

### 3. Server Mode

```bash
# Start API server
./pi-edge server --port 8080

# With authentication
./pi-edge server --port 8080 --auth-key secret123

# Daemon mode
./pi-edge server --daemon --port 8080
```

---

## 🔧 Configuration

### Environment Variables
```bash
# Server settings
export PI_EDGE_PORT=8080
export PI_EDGE_HOST=0.0.0.0

# Scan settings
export PI_EDGE_TIMEOUT=30
export PI_EDGE_THREADS=100

# Output
export PI_EDGE_OUTPUT=json
export PI_EDGE_LOG_LEVEL=info
```

### Config File
Create `~/.pi-edge/config.yaml`:
```yaml
server:
  port: 8080
  host: 0.0.0.0
  auth:
    enabled: false
    key: ""

scan:
  timeout: 30
  threads: 100
  default_ports: "1-1000"

output:
  format: "json"  # json, yaml, table
  color: true
```

---

## 📊 Output Examples

### Console Output
```
🚀 Pi-Edge Scan Report
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Target: 192.168.1.1
Started: 2026-02-26 14:30:00
Duration: 2.34s

OPEN PORTS:
  22/tcp   SSH      OpenSSH 8.2
  80/tcp   HTTP     nginx 1.18
  443/tcp  HTTPS    nginx 1.18

OS Detection: Linux 5.4
Risk Score: 3/10
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### JSON Output
```json
{
  "scan_id": "pe-20260226-001",
  "target": "192.168.1.1",
  "timestamp": "2026-02-26T14:30:00Z",
  "duration": "2.34s",
  "ports": [
    {"port": 22, "protocol": "tcp", "service": "SSH", "version": "OpenSSH 8.2"},
    {"port": 80, "protocol": "tcp", "service": "HTTP", "version": "nginx 1.18"}
  ],
  "os": "Linux 5.4",
  "risk_score": 3
}
```

---

## 🔄 API Usage

### REST API
```bash
# Start server
./pi-edge server --port 8080

# Scan endpoint
curl -X POST http://localhost:8080/scan \
  -H "Content-Type: application/json" \
  -d '{"target": "192.168.1.1", "ports": "1-1000"}'

# Status endpoint
curl http://localhost:8080/status
```

### WebSocket
```bash
# Real-time scan updates
wscat -c ws://localhost:8080/ws

# Subscribe to events
curl http://localhost:8080/subscribe?channel=scans
```

---

## 🐛 Troubleshooting

### Permission Denied
```bash
# Fix permissions
chmod +x pi-edge

# Run with sudo (for raw sockets)
sudo ./pi-edge scan 192.168.1.1
```

### Connection Issues
```bash
# Check firewall
sudo ufw allow 8080

# Test connectivity
./pi-edge status --verbose
```

### Performance
```bash
# Optimize for speed
./pi-edge scan 192.168.1.0/24 --threads 200 --timeout 10

# Reduce memory
./pi-edge scan 192.168.1.0/24 --batch-size 50
```

---

## 🚀 Deployment

### Docker
```dockerfile
FROM alpine:latest
COPY pi-edge /usr/local/bin/
EXPOSE 8080
CMD ["pi-edge", "server", "--port", "8080"]
```

### Systemd
```bash
# /etc/systemd/system/pi-edge.service
sudo tee /etc/systemd/system/pi-edge.service > /dev/null <<EOF
[Unit]
Description=Pi-Edge Sovereign Engine
After=network.target

[Service]
ExecStart=/usr/local/bin/pi-edge server --port 8080
Restart=always

[Install]
WantedBy=multi-user.target
EOF

sudo systemctl enable pi-edge
sudo systemctl start pi-edge
```

### Kubernetes
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: pi-edge
spec:
  replicas: 3
  selector:
    matchLabels:
      app: pi-edge
  template:
    spec:
      containers:
      - name: pi-edge
        image: pi-swarm/pi-edge:latest
        ports:
        - containerPort: 8080
```

---

## 📞 Support

- **Issues**: https://github.com/Pi-Swarm/pi-edge-sovereign/issues
- **Releases**: https://github.com/Pi-Swarm/pi-edge-sovereign/releases
- **Documentation**: See docs/ folder

---

**⚡ Pi-Edge: Precision. Speed. Sovereignty.**
