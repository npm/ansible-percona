# Ansible Role: Percona

Ansible playbook to install Percona XtraDB MySQL Cluster on Debian/Ubuntu servers

## Requirements

None.

## Role Variables

Available variables are listed below with its default values.

	mysql_root_password: reallylongpassword
  percona_package: percona-xtradb-cluster-56

Define the MySQL root password, this password will be used to create a **/root/.my.cnf** to allow root mysql connections without password

	mysql_port: 3306
	mysql_bind_address: 0.0.0.0

Define port and bind address for MySQL connections

	mysql_max_allowed_packet: 16M
	mysql_key_buffer: 16M
	mysql_thread_stack: 192K
	mysql_cache_size: 8

Various other settings are available in defaults/main.yml

## Cluster configuration
If using a cluster define at least `wsrep_cluster_name` and `wsrep_cluster_hosts`(a list of hosts) and optionally other settings:

  wsrep_slave_threads: 2
  wsrep_sst_method: rsync

Additionally one node should be set with `percona_master_node` to true. This is because a percona cluster must be started with the
bootsrap-pxc command on its first start. The percona_master_node will attempt to start with the bootstrap when its package is
installed and should be the first node in a cluster to run.

These are optional variables that default to undefined

  wsrep_node_name
  wsrep_notify_cmd
  wsrep_sst_receive_address
  wsrep_sst_auth

## SSL Configuration

If mysql_ssl_key is defined then ssl is enabled and all of the below ssl variables need to be defined.

- mysql_ssl_ca
- mysql_ssl_cert
- mysql_ssl_key

Optionally to copy in the appropriate certs define these variables

- mysql_ssl_ca_src
- mysql_ssl_cert_src
- mysql_ssl_key_src

## Dependencies

None.

## Example Playbook

	---
	- hosts: all
	  sudo: true
	  roles:
		  - tkuhlman.ansible-percona

## License

MIT / BSD
