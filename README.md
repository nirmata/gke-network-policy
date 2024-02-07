# GKE Autopilot/Standard NetworkPolicies

We recommend creating an implicit `default-deny` policy for your Kubernetes pods
ensuring that unwanted traffic is denied by default and only explicitly allowed
communication is flowing between applications on a cluster.

## How to use the supplied policies

Using the defined policies under the `policy` folder, an institution is able to
enhance its security posture by embracing `default-deny` network posture within its
Kubernetes clusters.

The following 3 policies are supplied:
- `generate-net-existing-default-deny` - Generates a `NetworkPolicy` rule that
  will automatically block any egress/ingress traffic for all existing or new
  namespaces in the cluster. Further, it will add a requirement for two boolean
  labels:
  - `ingressAccess` - For `Deployments` requiring ingress access, set to `true`
  - `egressAccess` - For  `Deployments` requiring egress access, set to `true`
  - *NOTE* - this is an example of how one can solve the need for `default-deny`
    it is not the only way.
- `validate-net-exists-for-deploy` - Checks to make sure that at least 1
  `NetworkPolicy` exists in the namespace. It is recommended to increase the
  counter to 2 once a more complete network traffic pattern is established.
- `validate-net-label-exists` - Checks to make sure any new `Deployments` in the
  cluster are defining labels for egress and ingress access. Thus ensuring
  proper enforcement of `default-deny` posture.
