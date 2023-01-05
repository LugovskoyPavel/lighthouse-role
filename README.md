Role Name
=========

Install_lighthouse

Requirements
------------

For use Role " Install_lighthouse" You neeed to install and configure git and NGINX.

Role Variables
--------------

| vars	| Description	| Value	 | Location |
| -------------|:------------:|:---------------:|:------------:|
|lighthouse_dir	| Where to store Lighthouse files	| "/home/{{ ansible_user_id }}/lighthouse"	| vars/main.yml |
|lighthouse_url	| URL of Clickhouse repo	| "https://github.com/VKCOM/lighthouse.git"	| vars/main.yml |


Example Playbook
----------------
```
- name: Install lighthouse
  hosts: lighthouse1  
  pre_tasks:
    - name: Lighthouse | Install git
      become: true
      ansible.builtin.yum:
        name: git
        state: present
    - name: install EPEL repo
      become: yes
      yum: name=epel-release state=present
    - name: Lighhouse | Install nginx
      become: true
      ansible.builtin.yum:
        name: nginx
        state: present
    - name: Lighthouse | Apply nginx config
      become: true
      ansible.builtin.template:
        src: nginx.conf.j2
        dest: /etc/nginx/nginx.conf
        mode: 0644
   role:
     -lighthouse  
```

License
-------

BSD

Author Information
------------------

Lugovskoy Pavel
