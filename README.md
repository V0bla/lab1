# ДЗ 1. Обновление ядра ОС Linux
По условиям ДЗ обновление необходимо выполнить средствами ansible. Для обновления выбрана ОС Centos 7

---
- name: kernel update
  # хост на котором производим обновление
  hosts: 10.0.2.15
  # указываем необходимость овышения привелегий и метод
  become: yes
  become_method: sudo
  tasks:
  # устанавливаем репозиторий elrepo
  - name: install repo
    ansible.builtin.yum:
      name: https://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm
      state: present
  # обновляем ядро
  - name: update kernel
    ansible.builtin.yum:
      name: kernel-ml
      enablerepo: elrepo-kernel
  # перезапускаем ОС после установки обновленного ядра
  - name: post update
    ansible.builtin.reboot:
...
