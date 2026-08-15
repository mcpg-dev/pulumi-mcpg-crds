# @mcpg/pulumi-crds

Typed Pulumi resource classes for the `mcpg.dev` custom resources — the
Kubernetes API served by the MCPG operator. Declare an `MCPGGateway`, an
`MCPGPluginSet`, or any other MCPG resource in a Pulumi program with real
TypeScript types, completion, and diffs, instead of pushing untyped YAML through
a generic config group.

The package is generated from the MCPG CRD schemas with crd2pulumi and committed
as generated. Do not edit it by hand: change the CRDs and regenerate.

## Quick start

```ts
import { mcpg } from "@mcpg/pulumi-crds";

new mcpg.v1alpha1.MCPGGateway("orders", {
  metadata: { namespace: "mcpg-system" },
  spec: {
    image: { repository: "ghcr.io/mcpg-dev/source-code/gateway", tag: "<tag>" },
    config: {},
  },
});
```

## Resources

`mcpg.v1alpha1` exports one class per MCPG kind, plus `…List` and `…Patch`
variants of each for reading collections and for server-side-apply patches.

| Class | What it declares |
|---|---|
| `MCPGGateway` | A gateway deployment and the configuration it serves. |
| `MCPGCluster` | The coordination backend a gateway cluster shares. |
| `MCPGRoute` | A tool subset bound into a shared gateway, with its chains. |
| `MCPGTenant` | A tenant boundary: namespaces, plugin allowlist, quotas. |
| `MCPGPlugin` | A plugin artifact and the trust it must satisfy. |
| `MCPGPluginSet` | An ordered plugin list and its capability grants. |
| `MCPGPluginMirror` | An in-cluster mirror for plugin artifacts. |
| `MCPGRevocationList` | Revoked plugin artifacts, by digest. |

## Higher-level components

These classes are the raw resource surface. For components that install the
operator, own the CRD lifecycle, assemble a gateway's configuration, and set up
tenants, use `@mcpg/pulumi`, which is built on this package.

## Licence

Apache-2.0.

## See also

- <https://mcpg.dev/docs/reference/operator-crds> — field-by-field reference for
  every resource above.
- <https://mcpg.dev/docs/self-hosting/pulumi> — deploying MCPG with Pulumi.

## Building and testing

```sh
npm install
npm run build
```
