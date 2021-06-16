# REANA: reproducible research data analysis platform.

## Chart Prefix

This Helm automatically prefixes all names using the release name to avoid collisions.

## Configuration

| Parameter                                                | Description                                                                          | Default value                                   |
|----------------------------------------------------------|--------------------------------------------------------------------------------------|-------------------------------------------------|
| `components.reana_db.enabled`                            | Instantiate a PostgreSQL database inside the cluster                                 | true                                            |
| `components.reana_job_controller.image`                  | [REANA-Job-Controller image](https://hub.docker.com/r/reanahub/reana-job-controller) to use  | `reanahub/reana-job-controller:<chart-release-version>` |
| `components.reana_message_broker.image`                  | [REANA-Message-Broker image](https://hub.docker.com/r/reanahub/reana-message-broker) to use | `reanahub/reana-message-broker:<chart-release-version>` |
| `components.reana_message_broker.imagePullPolicy`        | REANA-Message-Broker image pull policy                                               | IfNotPresent                                    |
| `components.reana_server.environment`                    | REANA-Server environment variables                                                   | {REANA_MAX_CONCURRENT_BATCH_WORKFLOWS: 30, REANA_USER_EMAIL_CONFIRMATION: true}      |
| `components.reana_server.image`                          | [REANA-Server image](https://hub.docker.com/r/reanahub/reana-server) to use          | `reanahub/reana-server:<chart-release-version>` |
| `components.reana_server.imagePullPolicy`                | REANA-Server image pull policy                                                       | IfNotPresent                                    |
| `components.reana_server.uwsgi.processes`                | Number of uWSGI processes                                                            | 6                                               |
| `components.reana_server.uwsgi.threads`                  | Number of uWSGI threads                                                              | 4                                               |
| `components.reana_ui.announcement`                       | Announcement message displayed in site top banner                                    | None                                            |
| `components.reana_ui.enabled`                            | Instantiate the [REANA-UI](https://github.com/reanahub/reana-ui)                     | true                                            |
| `components.reana_ui.image`                              | [REANA-UI image](https://hub.docker.com/r/reanahub/reana-ui) to use                  | `reanahub/reana-ui:<chart-release-version>`     |
| `components.reana_ui.imagePullPolicy`                    | REANA-UI image pull policy                                                           | IfNotPresent                                    |
| `components.reana_ui.polling_secs`                       | Frequency of workflow list page reload in seconds                                    | 15                                              |
| `components.reana_ui.client_pyvenv`                      | REANA-Client python environment to source in the welcome example.                    | None                                            |
| `components.reana_ui.docs_url`                           | URL of documentation site (footer icon)                                              | None                                            |
| `components.reana_ui.forum_url`                          | URL of forum site (footer icon)                                                      | None                                            |
| `components.reana_ui.chat_url`                           | URL of chat channel (footer icon)                                                    | None                                            |
| `components.reana_ui.cern_sso`                           | Enable CERN SSO sign in                                                              | false                                           |
| `components.reana_ui.cern_ropo`                          | Display CERN RoPO privacy policy page                                                | false                                           |
| `components.reana_ui.local_users`                        | Enable local users sign in/up                                                        | true                                            |
| `components.reana_ui.hide_signup`                        | Hide users sign up form                                                              | false                                           |
| `components.reana_workflow_controller.environment`       | REANA-Workflow-Controller environment variables                                      | `{SHARED_VOLUME_PATH: /var/reana}`              |
| `components.reana_workflow_controller.image`             | [REANA-Workflow-Controller image](https://hub.docker.com/r/reanahub/reana-workflow-controller) to use | `reanahub/reana-workflow-controller:<chart-release-version>` |
| `components.reana_workflow_controller.imagePullPolicy`   | REANA-Workflow-Controller image pull policy                                          | IfNotPresent                                    |
| `components.reana_workflow_controller.environment.REANA_JOB_HOSTPATH_MOUNTS`   | JSON list of optional hostPath mounts, for all user jobs. Each mount object has a key `name` (name of the mount), `hostPath` (path to the directory to be mounted from the Kubernetes nodes) and `mountPath` (path inside the job containers where the `hostPath` will be mounted)            | None                                            |
| `components.reana_workflow_controller.environment.REANA_RUNTIME_KUBERNETES_KEEP_ALIVE_JOBS_WITH_STATUSES` | Keep alive Kubernetes user runtime jobs depending on status (`finished` and/or `failed`). | None |
| `components.reana_workflow_engine_cwl.image`             | [REANA-Workflow-Engine-CWL image](https://hub.docker.com/r/reanahub/reana-workflow-engine-cwl) to use | `reanahub/reana-workflow-engine-cwl:<chart-release-version>` |
| `components.reana_workflow_engine_serial.image`          | [REANA-Workflow-Engine-Serial image](https://hub.docker.com/r/reanahub/reana-workflow-engine-serial) to use | `reanahub/reana-workflow-engine-serial:<chart-release-version>` |
| `components.reana_workflow_engine_yadage.image`          | [REANA-Workflow-Engine-Yadage image](https://hub.docker.com/r/reanahub/reana-workflow-engine-yadage) to use | `reanahub/reana-workflow-engine-yadage:<chart-release-version>` |
| `db_env_config.REANA_DB_HOST`                            | Environment variable to connect to external databases                                | `<chart-release-name>-db`                       |
| `db_env_config.REANA_DB_NAME`                            | Environment variable to connect to external databases                                | reana                                           |
| `db_env_config.REANA_DB_PORT`                            | Environment variable to connect to external databases                                | "5432"                                          |
| `debug.enabled`                                          | Instantiate a [wdb](https://github.com/Kozea/wdb) remote debugger inside the cluster, accessible in port `31984` | false               |
| `eos.enabled`                                            | **[CERN only]** Enable EOS support inside the cluster                                | false                                           |
| `fullnameOverride`                                       | Name to override the `reana.prefix`                                                  | None                                            |
| `ingress.annotations.ingress.kubernetes.io/ssl-redirect` | Redirect all traffic to HTTPS                                                        | true                                            |
| `ingress.annotations.kubernetes.io/ingress.class`        | Type of ingress controller                                                           | traefik                                         |
| `ingress.annotations.traefik.frontend.entryPoints`       | Entrypoints allowed by the ingress controller                                        | "http,https"                                    |
| `ingress.enabled`                                        | Create an ingress resource to access the REANA instance from outside the cluster     | true                                            |
| `ingress.tls.enabled`                                    | Enable TLS for the ingress resource                                                  | false                                           |
| `ingress.tls.secretName`                                 | Secret containing the certificate/key for https on the ingress controller            | none                                            |
| `kubernetes_jobs_memory_limit`                           | Maximum default memory limit for user job containers. Exceeding this limit will terminate the container. Please see the following URL for possible values https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#meaning-of-memory. | 4Gi |
| `kubernetes_jobs_max_user_memory_limit`                  | Maximum custom memory limit that users can assign to their job containers via
`kubernetes_memory_limit` hint in `reana.yaml`. Exceeding this limit will terminate the container. Please see the following URL for possible values https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#meaning-of-memory. | None |
| `limited_privs`                                          | Grant pods a limited subset of privileges compatible with OpenShift defaults (specifically, do not grant rights to read node information | false |
| `node_label_infrastructure`                              | Define the label which identifies the nodes where the infrastructure pods should run, e.g. `reana.io/system=infrastructure`. If you are setting this configuration variable, please also set `.traefik.nodeSelector.reana.io/system=infrastructure` so the ingress controller is also deployed on the infrastructure node. By default infrastructure pods can be scheduled to any available node in the cluster. | None |
| `node_label_runtimebatch`                                | Define the label which identifies the nodes where the runtime workflow pods should run, e.g. `reana.io/system=runtimebatch`. By default runtime workflow pods can be scheduled to any available node in the cluster. | None |
| `node_label_runtimejobs`                                 | Define the label which identifies the nodes where the runtime job pods should run, e.g. `reana.io/system=runtimejobs`. By default runtime job pods can be scheduled to any available node in the cluster. | None |
| `node_label_runtimesessions`                             | Define the label which identifies the nodes where the runtime session pods should run, e.g. `reana.io/system=runtimesessions`. By default runtime session pods can be scheduled to any available node in the cluster. | None |
| `notifications.email_config.login`                       | Login for the sender email address                                                   | None                                            |
| `notifications.email_config.password`                    | Password for the sender email address                                                | None                                            |
| `notifications.email_config.receiver`                    | Email address which will be receiving the notifications                              | None                                            |
| `notifications.email_config.sender`                      | Email address which will be sending the notifications                                | None                                            |
| `notifications.email_config.smtp_server`                 | SMTP email server host                                                               | None                                            |
| `notifications.email_config.smtp_port`                   | SMTP email server port                                                               | None                                            |
| `notifications.enabled`                                  | Enable REANA system events notifications                                             | false                                           |
| `notifications.system_status`                            | Cronjob pattern representing how often the system status notification should be sent. Leave it empty to deactivate it | "0 0 * * *"    |
| `reana_hostname`                                         | REANA hostname (e.g. reana.example.org)                                              | None                                            |
| `namespace_runtime`                                      | Namespace in which the REANA runtime pods (workflow engines, jobs etc...) will run   | `.Release.Namespace`                            |
| `naming_scheme`                                          | REANA component naming scheme                                                        | None                                            |
| `secrets.cern.sso.CERN_CONSUMER_KEY`                     | CERN SSO consumer key                                                                | None                                            |
| `secrets.cern.sso.CERN_CONSUMER_SECRET`                  | **[Do not use in production, use secrets instead]** CERN SSO consumer secret         | None                                            |
| `secrets.database.password`                              | **[Do not use in production, use secrets instead]** PostgreSQL database password     | None                                            |
| `secrets.database.user`                                  | PostgreSQL database username                                                         | None                                            |
| `secrets.gitlab.REANA_GITLAB_HOST`                       | Hostname of the GitLab instance                                                      | None                                            |
| `secrets.gitlab.REANA_GITLAB_OAUTH_APP_ID`               | GitLab OAuth application id                                                          | None                                            |
| `secrets.gitlab.REANA_GITLAB_OAUTH_APP_SECRET`           | **[Do not use in production, use secrets instead]** GitLab OAuth application secret  | None                                            |
| `secrets.reana.REANA_SECRET_KEY`                         | **[Do not use in production, use secrets instead]** REANA encryption secret key      | None                                            |
| `serviceAccount.create`                                  | Create a service account for the REANA system user                                   | true                                            |
| `serviceAccount.name`                                    | Service account name                                                                 | reana                                           |
| `shared_storage.access_modes`                            | Shared volume access mode                                                            | ReadWriteMany                                   |
| `shared_storage.backend`                                 | Shared volume storage backend                                                        | hostpath                                        |
| `shared_storage.cephfs.availability_zone`                | **[CERN only]** OpenStack Availability zone                                          | nova                                            |
| `shared_storage.cephfs.cephfs_os_share_access_id`        | **[CERN only]** CephFS share access ID                                               | None                                            |
| `shared_storage.cephfs.cephfs_os_share_id`               | **[CERN only]** CephFS share id                                                      | None                                            |
| `shared_storage.cephfs.os_secret_name`                   | **[CERN only]** Name of the Secret object containing OpenStack credentials           | os-trustee                                      |
| `shared_storage.cephfs.os_secret_namespace`              | **[CERN only]** Namespace of the OpenStack credentials Secret object                 | kube-system                                     |
| `shared_storage.cephfs.provisioner`                      | **[CERN only]** CephFS provisioner                                                   | manila-provisioner                              |
| `shared_storage.cephfs.type`                             | **[CERN only]** CephFS availability zone                                             | "Geneva CephFS Testing"                         |
| `shared_storage.custom_class`                            | Shared volume storage class (if backend == "custom")                                 | none                                            |
| `shared_storage.volume_size`                             | Shared volume size                                                                   | 200                                             |
| `shared_storage.shared_volume_mount_path`                | Path inside the REANA components where the shared volume will be mounted             | /var/reana                                      |
| `shared_storage.hostpath.root_path`                      | Path to the REANA directory inside the underlying storage volume                     | /var/reana                                      |
| `traefik.*`                                              | Pass any value from [Traefik Helm chart values](https://github.com/helm/charts/tree/master/stable/traefik#configuration) here, e.g. `traefik.rbac.enabled=true` | - |
| `traefik.enabled`                                        | Install Traefik in the cluster when installing REANA                                 | true                                            |
| `volume_paths.root_path`                                 | Path to the REANA directory inside the underlying storage volume                     | /var/reana                                      |
| `volume_paths.shared_volume_path`                        | Path inside the REANA components where the shared volume will be mounted             | /var/reana                                      |
| `quota.disk_update`                                      | Cronjob pattern representing how often the users disk quota usage should be updated. Leave it empty to deactivate it | "0 3 * * *"     |
| `quota.default_disk_limit`                               | Default users disk quota limit in bytes.                                             | None                                            |
| `quota.default_cpu_limit`                                | Default users CPU quota limit in milliseconds.                                       | None                                            |
| `use_security_context`                                   | Use Kubernetes security contexts for pods (set to false for OpenShift) | true
