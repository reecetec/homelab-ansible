# homelab-ansible

## install ansible + add deps
```bash
$ pipx install --include-deps ansible
$ pipx inject ansible kubernetes
$ ansible-galaxy collection install git+https://github.com/k3s-io/k3s-ansible.git
```

## setup vault
```bash
ansible-vault create secrets.yml
```

adding:
```yaml
ansible_host: server ip
ansible_user: server user
ansible_become_pass: server user's password
k3s_token: generate with $ openssl rand -base64 64 # this might not have worked, mby debug
```

## setup server
```bash
ansible-playbook setup-homelab.yml \
  --extra-vars "@secrets.yml" \
  --vault-password-file .vault_password
 ```

## add to .zshrc
```bash
export KUBECONFIG=~/.kube/config-homelab
```

## get argo pwd
```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

## access argo gui
add 
```
<server-ip> argocd.homelab.local
```
to /etc/hosts.

then visit https://argocd.homelab.local