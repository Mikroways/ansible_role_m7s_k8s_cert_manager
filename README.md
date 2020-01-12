# mikroways.m7s_k8s_cert_manager

Installs cert-manager using helm and previously applies custom resource
definitions as it's required.

## Requirements

This module requires k8s ansible module

## Role Variables

Role variables are:

* `m7s_k8s_cert_manager_state`: wether this module shall actuate or not.
  Defaults to present. If absent it will uninstall everything.
* `m7s_k8s_cert_manager_namespace`: namespace where all resources will be
  installed. Defaults to cert-manager.
* `m7s_k8s_cert_manager_version`: which version of cert-manager to install.
  Defaults to 0.12.
* `m7s_k8s_cert_manager_helm_repo_name`: helm repo name. Defaults to jetstack.
* `m7s_k8s_cert_manager_helm_repo_url`: helm repo url. Defaults to https://charts.jetstack.io.
* `m7s_k8s_cert_manager_helm_chart_name`: helm chart name. Defaults to cert-manager.
* `m7s_k8s_cert_manager_helm_chart`: name of the chart to install. Defaults to `{{m7s_k8s_cert_manager_helm_repo_name}}/cert-manager`
* `m7s_k8s_cert_manager_helm_config`: any helm values to be set. Defaults to
  empty dict.
* `m7s_k8s_cert_manager_ca_issuer_from_k8s`: this option enables a clustesissuer
  using ca issuer with certificate and key used by apiserver to sign its
  certificates. This will simplify integration with oidc module when using self
  signed certificates.
* `m7s_k8s_cert_manager_ca_issuer_from_k8s_secret_name`: secret name when
  `m7s_k8s_cert_manager_ca_issuer_from_k8s` is true. This secret will be needed
  by the clusterissuer created.
* `m7s_k8s_cert_manager_ca_issuer_from_k8s_cert_file`: path of k8s ca.crt file.
  It defaults to kubespray default `{{ kube_cert_dir }}/ca.crt`
* `m7s_k8s_cert_manager_ca_issuer_from_k8s_key_file`: path of k8s ca.key file.
  It defaults to kubespray default `{{ kube_cert_dir }}/ca.key`
* `m7s_k8s_cert_manager_ca_issuer_from_k8s_cluster_issuer`: name of
  clusterissuer resource with k8s certificate and key for signin. Defualts to 
  `k8s-ca-issuer`

## Dependencies

Depends on the following roles:

* mikroways.m7s_k8s_helm

## Example Playbook

The following example shows how to use this role. It's tight coupled with
kubespray:


```yaml
- hosts: kube-master[0]
  roles:
    - { role: mikroways.m7s_k8s_cert_manager, tags: [ cert-manager ] }
```

## License

GPLv2

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
