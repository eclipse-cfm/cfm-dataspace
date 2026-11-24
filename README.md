# cfm-dataspace

The CFM Dataspace repo contains dataspace-specific resources, such as the Tenant Manager and specific agent
implementations for the Connector Fabric Manager.

These components were moved here from [eclipse-cfm/cfm](https://github.com/eclipse-cfm/cfm) after its
`v0.0.10` release. They build on the generic engine (Provision Manager, `common`, `assembly`) published as the Go
module `github.com/eclipse-cfm/cfm`.

## Layout

| Path | Contents |
|---|---|
| `tmanager/` | Tenant Manager |
| `agent/orchestration/` | orchestration agents (EDC-V, IdentityHub, registration, onboarding, JWTlet, Siglet, Certo) |
| `agent/lifecycle/` | lifecycle agents (key management) |
| `agent/common/` | clients and the VPA adapter shared by the agents |
| `dataspace/` | dataspace model shared by the Tenant Manager and the agents (was `common/dataspace` in `cfm`) |
| `e2e/` | end-to-end tests running the Provision Manager, the Tenant Manager and a test agent |
| `docker/` | Dockerfiles for the Tenant Manager and the agents |

## Migrating from `github.com/eclipse-cfm/cfm`

| Old import path | New import path |
|---|---|
| `github.com/eclipse-cfm/cfm/tmanager/...` | `github.com/eclipse-cfm/cfm-dataspace/tmanager/...` |
| `github.com/eclipse-cfm/cfm/agent/...` | `github.com/eclipse-cfm/cfm-dataspace/agent/...` |
| `github.com/eclipse-cfm/cfm/common/dataspace` | `github.com/eclipse-cfm/cfm-dataspace/dataspace` |

All other `github.com/eclipse-cfm/cfm/...` packages are unchanged.

## Building and testing

```sh
make build
make test   # needs Docker for the Postgres and NATS test containers
make lint
```

To work on `cfm` and `cfm-dataspace` together, use a Go workspace (`go.work` is gitignored):

```sh
go work init . ../cfm
```
