[Install Vault | Vault | HashiCorp Developer](https://developer.hashicorp.com/vault/docs/install#package-manager)

[Install Vault | Vault | HashiCorp Developer](https://developer.hashicorp.com/vault/tutorials/getting-started/getting-started-install)

<aside>
💡 **Vault is an identity-based secret and encryption management system.**

</aside>

> **Use Cases**
> 
- **Secrets Management**
    
    Centrally store, access, and deploy secrets across applications, systems, and infrastructure.
    
- **Encryption Services**
    
    Securely handle data such as social security numbers, credit card numbers, and other types of compliance-regulated information.
    
- **Secrets engines**
    
    Secrets engines are components which store, generate, or encrypt data.
    
    Secrets engines are enabled at a **path** in Vault. When a request comes to Vault, the router automatically routes anything with the route prefix to the secrets engine. 
    

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/f020007f-666a-401f-b7a3-4c1d3d9787c0/23249c79-1ff2-444f-b8cd-acda0ab4e1f8/Untitled.png)

- **Policies**
    
    Everything in Vault is path-based, and policies are no exception. Policies provide a declarative way to grant or forbid access to certain paths and operations in Vault.
    
    Policies are **deny by default**, so an empty policy grants no permission in the system.
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/f020007f-666a-401f-b7a3-4c1d3d9787c0/dc761f1f-cf7b-4a1d-86c6-5d36a54eec1f/Untitled.png)
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/f020007f-666a-401f-b7a3-4c1d3d9787c0/7d65116f-5d57-4561-bb65-5cea1dc5f639/Untitled.png)
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/f020007f-666a-401f-b7a3-4c1d3d9787c0/54e14256-69c6-4ab3-ad32-ea47cc408de8/Untitled.png)
    

### Install Vault

```yaml
sudo apt update && sudo apt install gpg wget
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
gpg --no-default-keyring --keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg --fingerprint
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install vault
vagrant@istio-cluster:~$ vault version
Vault v1.15.5 (0d8b67ef63815f20421c11fe9152d435af3403e6), built 2024-01-26T14:53:40Z
```

### **Start Vault using Development Mode**

```yaml
vagrant@istio-cluster:~$ vault server -dev
==> Vault server configuration:

Administrative Namespace:
             Api Address: http://127.0.0.1:8200
                     Cgo: disabled
         Cluster Address: https://127.0.0.1:8201
   Environment Variables: DBUS_SESSION_BUS_ADDRESS, GODEBUG, GOTRACEBACK, HOME, LANG, LESSCLOSE, LESSOPEN, LOGNAME, LS_COLORS, MOTD_SHOWN, PATH, PWD, SHELL, SHLVL, SSH_CLIENT, SSH_CONNECTION, SSH_TTY, TERM, USER, XDG_DATA_DIRS, XDG_RUNTIME_DIR, XDG_SESSION_CLASS, XDG_SESSION_ID, XDG_SESSION_TYPE, _
              Go Version: go1.21.5
              Listener 1: tcp (addr: "127.0.0.1:8200", cluster address: "127.0.0.1:8201", max_request_duration: "1m30s", max_request_size: "33554432", tls: "disabled")
               Log Level:
                   Mlock: supported: true, enabled: false
           Recovery Mode: false
                 Storage: inmem
                 Version: Vault v1.15.5, built 2024-01-26T14:53:40Z
             Version Sha: 0d8b67ef63815f20421c11fe9152d435af3403e6

==> Vault server started! Log data will stream in below:

2024-02-27T07:39:52.895Z [INFO]  proxy environment: http_proxy="" https_proxy="" no_proxy=""
2024-02-27T07:39:52.896Z [INFO]  incrementing seal generation: generation=1
2024-02-27T07:39:52.896Z [WARN]  no `api_addr` value specified in config or in VAULT_API_ADDR; falling back to detection if possible, but this value should be manually set      
2024-02-27T07:39:52.897Z [INFO]  core: Initializing version history cache for core
2024-02-27T07:39:52.897Z [INFO]  events: Starting event system
2024-02-27T07:39:52.899Z [INFO]  core: security barrier not initialized
2024-02-27T07:39:52.899Z [INFO]  core: security barrier initialized: stored=1 shares=1 threshold=1
2024-02-27T07:39:52.901Z [INFO]  core: post-unseal setup starting
2024-02-27T07:39:52.915Z [INFO]  core: loaded wrapping token key
2024-02-27T07:39:52.915Z [INFO]  core: successfully setup plugin runtime catalog
2024-02-27T07:39:52.915Z [INFO]  core: successfully setup plugin catalog: plugin-directory=""
2024-02-27T07:39:52.915Z [INFO]  core: no mounts; adding default mount table
2024-02-27T07:39:52.924Z [INFO]  core: successfully mounted: type=cubbyhole version="v1.15.5+builtin.vault" path=cubbyhole/ namespace="ID: root. Path: "
2024-02-27T07:39:52.927Z [INFO]  core: successfully mounted: type=system version="v1.15.5+builtin.vault" path=sys/ namespace="ID: root. Path: "
2024-02-27T07:39:52.928Z [INFO]  core: successfully mounted: type=identity version="v1.15.5+builtin.vault" path=identity/ namespace="ID: root. Path: "
2024-02-27T07:39:52.937Z [INFO]  core: successfully mounted: type=token version="v1.15.5+builtin.vault" path=token/ namespace="ID: root. Path: "
2024-02-27T07:39:52.937Z [INFO]  rollback: Starting the rollback manager with 256 workers
2024-02-27T07:39:52.938Z [INFO]  rollback: starting rollback manager
2024-02-27T07:39:52.941Z [INFO]  core: restoring leases
2024-02-27T07:39:52.941Z [INFO]  expiration: lease restore complete
2024-02-27T07:39:52.946Z [INFO]  identity: entities restored
2024-02-27T07:39:52.946Z [INFO]  identity: groups restored
2024-02-27T07:39:52.946Z [INFO]  core: Recorded vault version: vault version=1.15.5 upgrade time="2024-02-27 07:39:52.946600202 +0000 UTC" build date=2024-01-26T14:53:40Z       
2024-02-27T07:39:52.947Z [INFO]  core: post-unseal setup complete
2024-02-27T07:39:52.950Z [INFO]  core: root token generated
2024-02-27T07:39:52.950Z [INFO]  core: pre-seal teardown starting
2024-02-27T07:39:52.950Z [INFO]  rollback: stopping rollback manager
2024-02-27T07:39:52.951Z [INFO]  core: pre-seal teardown complete
2024-02-27T07:39:52.951Z [INFO]  core.cluster-listener.tcp: starting listener: listener_address=127.0.0.1:8201
2024-02-27T07:39:52.951Z [INFO]  core.cluster-listener: serving cluster requests: cluster_listen_address=127.0.0.1:8201
2024-02-27T07:39:52.951Z [INFO]  core: post-unseal setup starting
2024-02-27T07:39:52.951Z [INFO]  core: loaded wrapping token key
2024-02-27T07:39:52.951Z [INFO]  core: successfully setup plugin runtime catalog
2024-02-27T07:39:52.951Z [INFO]  core: successfully setup plugin catalog: plugin-directory=""
2024-02-27T07:39:52.954Z [INFO]  core: successfully mounted: type=system version="v1.15.5+builtin.vault" path=sys/ namespace="ID: root. Path: "
2024-02-27T07:39:52.955Z [INFO]  core: successfully mounted: type=identity version="v1.15.5+builtin.vault" path=identity/ namespace="ID: root. Path: "
2024-02-27T07:39:52.955Z [INFO]  core: successfully mounted: type=cubbyhole version="v1.15.5+builtin.vault" path=cubbyhole/ namespace="ID: root. Path: "
2024-02-27T07:39:52.957Z [INFO]  core: successfully mounted: type=token version="v1.15.5+builtin.vault" path=token/ namespace="ID: root. Path: "
2024-02-27T07:39:52.957Z [INFO]  rollback: Starting the rollback manager with 256 workers
2024-02-27T07:39:52.958Z [INFO]  rollback: starting rollback manager
2024-02-27T07:39:52.958Z [INFO]  core: restoring leases
2024-02-27T07:39:52.958Z [INFO]  expiration: lease restore complete
2024-02-27T07:39:52.959Z [INFO]  identity: entities restored
2024-02-27T07:39:52.959Z [INFO]  identity: groups restored
2024-02-27T07:39:52.960Z [INFO]  core: post-unseal setup complete
2024-02-27T07:39:52.960Z [INFO]  core: vault is unsealed
2024-02-27T07:39:52.976Z [INFO]  core: successful mount: namespace="" path=secret/ type=kv version=""
WARNING! dev mode is enabled! In this mode, Vault runs entirely in-memory
and starts unsealed with a single unseal key. The root token is already
authenticated to the CLI, so you can immediately begin using Vault.

You may need to set the following environment variables:

    $ export VAULT_ADDR='http://127.0.0.1:8200'

The unseal key and root token are displayed below in case you want to
seal/unseal the Vault or re-authenticate.

Unseal Key: Z8FC2y3vUex2ozBxC+Yy8w3zkqSwpRq7y99NXyHYE4Q=
Root Token: hvs.etHK5dKRax3NecHIgcq5clyz
.
.
```

<aside>
💡 **WARNING! dev mode is enabled! In this mode, Vault runs entirely in-memory
and starts unsealed with a single unseal key. The root token is already
authenticated to the CLI, so you can immediately begin using Vault.**

</aside>

<aside>
💡 **Development mode should NOT be used in production installations!**

</aside>

```yaml
vagrant@istio-cluster:~$ vault status
Error checking seal status: Get "https://127.0.0.1:8200/v1/sys/seal-status": http: server gave HTTP response to HTTPS client

vagrant@istio-cluster:~$ export VAULT_ADDR='http://127.0.0.1:8200'

vagrant@istio-cluster:~$ vault status
Key             Value
---             -----
Seal Type       shamir
Initialized     true
Sealed          false
Total Shares    1
Threshold       1
Version         1.15.5
Build Date      2024-01-26T14:53:40Z
Storage Type    inmem
Cluster Name    vault-cluster-d3b67e2b
Cluster ID      8866ed1c-3cbf-61aa-72cb-20d51320fd5e
HA Enabled      false
vagrant@istio-cluster:~$ 
```

### Vault can be accessed using UI.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/f020007f-666a-401f-b7a3-4c1d3d9787c0/b3031be6-4ad0-468c-9985-a80a16ab0ce8/Untitled.png)

### Vault can be accessed using HTTP API.

[HTTP API | Vault | HashiCorp Developer](https://developer.hashicorp.com/vault/api-docs)

**Vault has an HTTP API that can be used to control every aspect of Vault.**

**The Vault HTTP API gives you full access to Vault using [REST like HTTP verbs](https://en.wikipedia.org/wiki/Representational_state_transfer). Every aspect of Vault can be controlled using the APIs. The Vault CLI uses the HTTP API to access Vault similar to all other consumers.**

**All API routes are prefixed with `/v1/`.**

```yaml
$ curl     http://127.0.0.1:8200/v1/sys/health | jq
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   295  100   295    0     0   373k      0 --:--:-- --:--:-- --:--:--  288k
{
  "initialized": true,
  "sealed": false,
  "standby": false,
  "performance_standby": false,
  "replication_performance_mode": "disabled",
  "replication_dr_mode": "disabled",
  "server_time_utc": 1709042298,
  "version": "1.15.5",
  "cluster_name": "vault-cluster-5a023278",
  "cluster_id": "bf76b06f-857a-32fb-7df9-7de31147ef12"
}
```

```yaml
$ curl     http://127.0.0.1:8200/v1/sys/seal-status | jq
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   298  100   298    0     0   363k      0 --:--:-- --:--:-- --:--:--  291k
{
  "type": "shamir",
  "initialized": true,
  "sealed": false,
  "t": 1,
  "n": 1,
  "progress": 0,
  "nonce": "",
  "version": "1.15.5",
  "build_date": "2024-01-26T14:53:40Z",
  "migration": false,
  "cluster_name": "vault-cluster-5a023278",
  "cluster_id": "bf76b06f-857a-32fb-7df9-7de31147ef12",
  "recovery_seal": false,
  "storage_type": "inmem"
}
```

### **Vault can be accessed using CLI.**

```yaml
$ vault auth list
Path      Type     Accessor               Description                Version
----      ----     --------               -----------                -------
token/    token    auth_token_bdb3a880    token based credentials    n/a

$ vault secrets list
Path           Type          Accessor               Description
----           ----          --------               -----------
cubbyhole/     cubbyhole     cubbyhole_63a670bf     per-token private secret storage
identity/      identity      identity_bb56535d      identity store
kubernetes/    kubernetes    kubernetes_f4ebe7fa    n/a
secret/        kv            kv_966419c8            key/value secret storage
sys/           system        system_59797446        system endpoints used for control, policy and debugging
```
