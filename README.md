#reference
https://github.com/vbezgachev/maxctrl_exporter?tab=readme-ov-file

# Step install maxscale exporter
## Create user for exporter
sudo useradd --no-create-home --shell /sbin/nologin maxscale-exporter

## move exporter
mv maxscale_exporter /usr/local/bin/

## Create exporter run by systemd
sudo vi /etc/systemd/system/maxscale_exporter.service

```
[Unit]
Description=MaxScale Prometheus Exporter
After=network.target

[Service]
User=maxscale-exporter
Group=maxscale-exporter
Type=simple
ExecStart=/usr/local/bin/maxscale_exporter

Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target
```

## Add permission
sudo chown maxscale-exporter:maxscale-exporter /usr/local/bin/maxscale_exporter

sudo chmod 755 /usr/local/bin/maxscale_exporter

## Start service
sudo systemctl daemon-reload

sudo systemctl start --now maxscale_exporter

##check status
sudo systemctl status maxscale_exporter

