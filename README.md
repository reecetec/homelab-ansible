# homelab-ansible

## install ansible
```bash
$ pipx install --include-deps ansible
```

## add k3s
```bash
$ ansible-galaxy collection install git+https://github.com/k3s-io/k3s-ansible.git
```

## setup vault
```bash
ansible-vault create secrets.yml
```
adding:
```yaml
ansible_host: YOUR_SERVER_IP
ansible_user: YOUR_USERNAME
```


```bash
ansible-playbook k3s.orchestration.site \
  -i inventory.yml \
  --extra-vars "@secrets.yml" \
  --ask-vault-pass \
  --ask-become-pass
 ```