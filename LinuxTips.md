vie 29 ago 2025 01:22:32 CEST
# how to install nvidia container
## Instal nvidia drivers
```bash
sudo apt update && sudo apt upgrade -y
sudo ubuntu-drivers autoinstall
sudo reboot
```
After rebot, verify:


```bash
nvidia-smi
```

Install nvidia container toolkit
```bash
curl -s -L https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit.gpg
curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit.gpg] https://#' | sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
sudo apt update
sudo apt install -y nvidia-container-toolkit
sudo nvidia-ctk runtime configure --runtime=docker --set-as-default
sudo systemctl restart docker
```

Configure CDI
```bash
sudo nvidia-ctk cdi generate --output=/etc/cdi/nvidia.yaml
sudo systemctl restart docker
```

Test
```bash
docker run --rm --device nvidia.com/gpu=all nvidia/cuda:12.5.1-base-ubuntu22.04 nvidia-smi
```

# Fix locale
```bash
sudo update-locale LC_TIME=es_ES.UTF-8
sudo update-locale LANG=en_US.UTF-8
source /etc/default/locale
```


