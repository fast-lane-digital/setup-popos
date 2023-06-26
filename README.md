# Setup Pop!Os

Instructions, scripts and to set up Pop!Os 22.04 LTS installations.

## Setup steps

1. Install Ansible
   ```shell
   sudo apt install python3-pip \
   && sudo pip install ansible
   ```
2. Download repository containing playbook
   ```shell
   mkdir ~/Repositories/fast-lane-digital \
   && cd ~/Repositories/fast-lane-digital \
   && git clone https://github.com/fast-lane-digital/setup-popos.git
   ```
3. Setup system
   ```shell
   ansible-playbook \
    --user "$USER" \
    --inventory ~/Repositories/fast-lane-digital/setup-popos/inventory \
    --connection=local \
    --ask-become-pass \
    ~/Repositories/fast-lane-digital/setup-popos/setup.yaml
   ```
4. Add user bin path
   ```shell
   echo 'export PATH="/home/$USER/.local/bin:$PATH"' >> ~/.bashrc
   ```
5. Enable extended keyboard layouts
   ```shell
   gsettings set org.gnome.desktop.input-sources show-all-sources true
   ```
6. Select the `English (US)` > `German, Swedish and Finnish (US)`
7. Enable signin with fingerprint
   ```shell
   sudo apt install libpam-fprintd
   ```

## Troubleshooting

### Stuck on "Gathering Facts"

This issue may happen when alternative PAM authentication methods are installed.
The best workaround for this issue is to use SSH connection instead of local connection.

Use the following command instead.

```shell
ansible-playbook \
  --inventory ~/Repositories/fast-lane-digital/setup-popos/inventory \
  --ask-become-pass \
  ~/Repositories/fast-lane-digital/setup-popos/setup.yaml
```
