## セットアップ手順

### 1. Ansible プロジェクトのクローン

```sh
git clone https://github.com/moriyku/ansible-practice.git
cd ansible-practice
```

### 2. SSH キーペアの生成

Ansible がリモートホストに接続するために使用する SSH キーを生成します。以下のコマンドを実行して、新しい SSH キーペアを生成します。

```sh
ssh-keygen -t rsa -b 2048 -f keys/web_server_key -N ''
```

これにより、keys ディレクトリに web_server_key（秘密鍵）と web_server_key.pub（公開鍵）が生成されます。

### 3. 公開鍵の managed node への配置

生成した公開鍵を managed node に配置します。

```sh
ssh-copy-id -i keys/web_server_key.pub user@managed_node_ip
```

### 4. secret_vars.yml.sample の作成

```sh
cp secret_vars.yml.sample secret_vars.yml
```

`secret_vars.yml.sample` をコピーし、`secret_vars.yml` を作成します。

### 5. secret_vars.yml の編集

```sh
ansible-vault edit secret_vars.yml
```

## Ansible の実行

```sh
ansible-playbook -i inventory.yml playbook.yml --ask-vault-pass
```

Vault のパスワードを入力して、Ansible を実行します。
