# ansibsible_playbook4
cron job

```
# #confgmgmt3
# #20232305
# #something is done here

  
- name: Install cowsay and schedule cron job
  hosts: linux1
  become: true
  tasks:
    - name: Install cowsay
      apt:
        name: cowsay

    - name: Schedule cron job
      ansible.builtin.cron:
        name: cowsay
        job: "/usr/games/cowsay 'Hi There!'"
        minute: "*/5"
        hour: "*"
        day: "*"
        month: "*"
        user: "{{ ansible_user }}"

    - name: Verify cowsay functionality
      command: "/usr/games/cowsay 'Hello'"
      register: cowsay_output

    - name: Display cowsay output
      debug:
        var: cowsay_output.stdout_lines

```
