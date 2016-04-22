Role Name
=========

Ansible role to install and manage sshguard
Requirements
------------

Need to add an iptables rule to enforce blocking the IPs added into the sshguard table, eg.

    # iptables -N sshguard
    # iptables -A INPUT -p tcp --dport 22 -j sshguard
    # ip6tables -N sshguard
    # ip6tables -A INPUT -p tcp --dport 22 -j sshguard

Role Variables
--------------

    sshguard_pkgs_state: installed
    sshguard_opts: "-b 60:/var/db/sshguard/blacklist.db -w {{ sshguard_whitelist_path }}"
    sshguard_journalctl_opts: '-u sshd'
    sshguard_service_state: started
    sshguard_service_enabled: yes
    sshguard_whitelist:
      - value: 127.0.0.0/8
        comment: IPv4 Localhost
      - value: ::1
        comment: IPv6 Localhost


Dependencies
------------

Using the RPM created from the spec here: https://gitlab.alcf.anl.gov/jlse/rpm-sshguard

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: sshguard }

License
-------

BSD

Author Information
------------------

Ben Allen <bsallen@alcf.anl.gov>
