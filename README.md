<br>

## Oracle Linux PostgreSQL Cluster
<br>

- Тестовые ВМ создаются с использованием `Vagrant`.

  ```bash
  ~ $ vagrant up
  ```

- Оркестратор `Ansible`. 

  ```bash
  ~ $ ansible-playbook playbook.yml
  ```

- Точки подключения.

  ```yml
  ssh_port: 22
  consul: 192.168.100.10:8500, 192.168.100.20:8500, 192.168.100.30:8500
  pg_cluster_virtual_ip: 192.168.100.100
  pg_cluster_ports: 5432, 8008
  ```

- Используемые версии ПО.
  ```yml
  Oracle Linux: 8
  PostgreSQL: 12
  Patroni: 1.6.5
  Ansible: 2.11.4
  Python: 3.9.7
  ```

- Архитектура.

  ```bash
  pg cluster virtual ip
      |
  PostgreSQL Cluster [pg01, pg02]
      |
  Consul Cluster [consul01, consul02, consul03]



  192.168.100.10  - consul01 [consul]
  192.168.100.20  - consul02 [consul]
  192.168.100.30  - consul03 [consul]
  192.168.100.40  - mon01 [monitoring]
  192.168.100.50  - pg01 [patroni, vip-manager, postgresql]
  192.168.100.60  - pg02 [patroni, vip-manager, postgresql]
  192.168.100.100 - pg_cluster_virtual_ip
  ```


<br><br>

## ToDo
<br>

```yml
- [ ] ssl
- [ ] consul user / pass
- [ ] pgbouncer with automate config change through consul
- [ ] global vars
- [ ] vault
- [ ] postgresql config
- [ ] pg_probackup by ssh through vip-manager
- [ ] monitoring vm + postgresql (prometheus+grafana)
- [ ] install patroni through pip
- [ ] choose postgresql version
- [ ] choose additional components to install
- [ ] set hostname in common
- [ ] 
- [ ] 
```




 