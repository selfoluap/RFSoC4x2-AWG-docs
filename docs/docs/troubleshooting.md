# Troubleshooting

During development and some breaks, the device got logged out from tailscale and was not reachable anymore. This is either because the tailscale key got expired or what happened for us was that the date was not updated.

After quick search, we found this command which should fix that issue

```bash
sudo date -s "$(wget -qSO- --max-redirect=0 google.com 2>&1 | grep Date: | cut -d' ' -f5-8)Z"
```
