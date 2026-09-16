# Tool Catalog

Full list of MCP tools exposed by the server, grouped by domain.
`R` = read-only · `W` = mutating (dry-run by default) · `D` = destructive (requires human approval)

### Cluster & node operations
| Tool | Type | Description |
|---|---|---|
| `list_clusters` | R | List clusters this server manages |
| `get_cluster_info` | R | Version, capacity, health summary |
| `list_nodes` / `get_node` | R | Node inventory and detail |
| `get_node_metrics` (`top_nodes`) | R | CPU/memory usage per node |
| `cordon_node` / `uncordon_node` | W | Mark a node (un)schedulable |
| `drain_node` | D (async) | Evict all pods from a node |

### Namespace & governance
| Tool | Type | Description |
|---|---|---|
| `list_namespaces` / `get_namespace` | R | Namespace inventory and detail |
| `create_namespace` | W | Create a namespace |
| `delete_namespace` | D | Delete a namespace and its contents |
| `get_resource_quota` / `get_limit_range` | R | Quota and default limits |

### Workloads
| Tool | Type | Description |
|---|---|---|
| `list_pods` / `get_pod` | R | Pod inventory and detail |
| `delete_pod` | W | Delete a pod (controller recreates it) |
| `list_deployments` / `get_deployment` | R | Deployment inventory and detail |
| `create_deployment` / `update_deployment` | W | Create or patch a Deployment |
| `delete_deployment` | D | Delete a Deployment |
| `scale_deployment` / `scale_statefulset` | W | Change replica count |
| `list_statefulsets` / `list_daemonsets` | R | Stateful/daemon workload inventory |
| `list_jobs` / `create_job` | R/W | Batch Job inventory and creation |
| `list_cronjobs` / `create_cronjob` / `trigger_cronjob` | R/W | Scheduled job management |

### Rollouts
| Tool | Type | Description |
|---|---|---|
| `get_rollout_status` / `get_rollout_history` | R | Current and historical rollout state |
| `restart_rollout` | W | Trigger a rolling restart |
| `pause_rollout` / `resume_rollout` | W | Pause/resume an in-progress rollout |
| `rollout_undo` | D | Roll back to a previous revision |

### Autoscaling
| Tool | Type | Description |
|---|---|---|
| `get_hpa` / `list_hpas` | R | HPA status |
| `create_hpa` / `update_hpa` | W | Configure autoscaling policy |
| `delete_hpa` | W | Remove an autoscaler |
| `get_vpa` | R | VPA recommendations |

### Networking
| Tool | Type | Description |
|---|---|---|
| `list_services` / `get_service` | R | Service inventory and detail |
| `create_service` / `update_service` | W | Create or patch a Service |
| `list_ingresses` / `get_ingress` | R | Ingress inventory and detail |
| `list_network_policies` | R | NetworkPolicy inventory |
| `get_endpoints` | R | Resolved endpoints behind a Service |

### Configuration & secrets
| Tool | Type | Description |
|---|---|---|
| `list_configmaps` / `get_configmap` | R | ConfigMap inventory and detail |
| `create_configmap` / `update_configmap` | W | Create or patch a ConfigMap |
| `list_secrets` / `get_secret` | R | Secret metadata; **values redacted** |
| `create_secret` / `rotate_secret` | W | Create/rotate a Secret via secure channel |

### Storage
| Tool | Type | Description |
|---|---|---|
| `list_pvs` / `list_pvcs` / `get_pvc` | R | Persistent volume(claim) inventory |
| `list_storage_classes` | R | Available storage classes |
| `expand_pvc` | W | Request a volume size increase |

### RBAC & identity
| Tool | Type | Description |
|---|---|---|
| `whoami` | R | Caller's effective Kubernetes identity |
| `can_i` | R | Check verb/resource permission |
| `list_roles` / `list_rolebindings` | R | RBAC object inventory |
| `list_service_accounts` | R | ServiceAccount inventory |

### Observability & troubleshooting
| Tool | Type | Description |
|---|---|---|
| `get_pod_logs` (`--follow`) | R | Tail container logs |
| `get_events` | R | Time-ordered cluster/object events |
| `describe_resource` | R | `kubectl describe`-equivalent detail |
| `diagnose_crashloop` | R | Correlate restarts/events/logs into root cause |
| `top_pods` | R | Per-pod CPU/memory usage |
| `exec_in_pod` | D | Interactive/one-shot exec into a container |
| `port_forward` | D | Open a local forward to a pod/service port |

### Manifests & GitOps
| Tool | Type | Description |
|---|---|---|
| `validate_manifest` | R | Schema/policy validation, no cluster call |
| `diff_manifest` | R | Server-side diff against the live object |
| `apply_manifest` | W | Apply a manifest (`dryRun=true` by default) |
| `get_applied_manifest` | R | Last-applied configuration of a live object |

### Helm
| Tool | Type | Description |
|---|---|---|
| `list_releases` / `get_release` | R | Helm release inventory and detail |
| `install_chart` | W | Install a new release |
| `upgrade_release` | W (async) | Upgrade an existing release |
| `rollback_release` | D (async) | Roll back to a previous revision |
| `uninstall_release` | D | Remove a release |

### Custom resources
| Tool | Type | Description |
|---|---|---|
| `list_crds` / `get_crd` | R | Installed CustomResourceDefinitions |
| `list_custom_resources` / `get_custom_resource` | R | Instances of a given CRD |

### Multi-cluster & context
| Tool | Type | Description |
|---|---|---|
| `list_contexts` | R | Clusters/contexts available to the caller |
| `switch_context` | W | Set active cluster for the session |
| `get_current_context` | R | Report the cluster currently in scope |

### Async job & approval management
| Tool | Type | Description |
|---|---|---|
| `get_job_status` | R | Poll status of a long-running operation |
| `cancel_job` | W | Cancel a pending/in-progress job |
| `list_pending_approvals` | R | Actions awaiting human confirmation |
| `approve_action` / `reject_action` | W | Confirm or deny a gated destructive action |
