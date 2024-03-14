## 1. PROVISIONING
+ Melakukan Persiapan untuk segala pekerjaan dengan penggunaan ansible sebagai berikut: 
```
Requirements: 
+ ansible
+ Server BiznetGio:
     AWS: 4GB RAM, 2 CPU
     Gateway: 1GB RAM, 1 CPU
```

+ Pada tahap ini terlebih dahulu menyiapkan dua buah server yaitu server dari Aws dan Gateway.
+ memilih sebuah tools ansible sebagai untuk melakukan automation agar bisa menyediakan sarana yang dibutuhkan dalam pengerjaan deploy aplikasi
+ kemudian menyiapkan script yang dibutuhkan seperti instalasi docker, instalasi cerbot dan generate SSL,

+ Script penginstalan docker untuk kedua server

```yaml
- name: Install Docker
  hosts: 13.238.154.16
  become: true
  tasks:
    - name: Update apt package cache and install dependencies
      apt:
        name: "{{ packages }}"
        state: present
        update_cache: yes
      vars:
        packages:
          - apt-transport-https
          - ca-certificates
          - curl
          - gnupg
          - lsb-release
    - name: Add Docker's official GPG key
      apt_key:
        url: https://download.docker.com/linux/ubuntu/gpg
        state: present

    - name: Add Docker repository
      apt_repository:
        repo: "deb [arch=amd64] https://download.docker.com/linux/ubuntu {{ ansible_lsb.codename }} stable"
        state: present

    - name: Install Docker and Docker Compose
      apt:
        name: 
          - docker-ce
          - docker-ce-cli
          - containerd.io
        state: present

    - name: Start and enable Docker service
      service:
        name: docker
        state: started
        enabled: yes

```
+ Script untuk melakukan generate cerbot certifate pada server Gateway 

```yaml

- name: Generate Certbot for SSL
  hosts: 13.238.154.16
  become: true
  
  tasks:
    - name: Install Certbot via snap
      become: true
      become_user: root
      shell: |
       sudo snap install --classic certbot &&
       sudo ln -s /snap/bin/certbot /usr/bin/certbot &&
       sudo snap set certbot trust-plugin-with-root=ok &&
       sudo snap install certbot-dns-cloudflare
      register: certbot_install_result
      changed_when: "certbot_install_result.rc == 0"

    - name: Create Certbot configuration directory
      file:
          path: "/home/ubuntu/.secrets"
          state: directory

    - name: Create Certbot Cloudflare credentials file
      template:
          src: ./credential/cloudflare.ini.j2  
          dest: "/home/ubuntu/.secrets/cloudflare.ini"
          mode: 0400

    - name: Run Certbot to obtain certificates
      command: >
        certbot certonly
        --dns-cloudflare
        --dns-cloudflare-credentials /home/ubuntu/.secrets/cloudflare.ini
        --agree-tos
        --non-interactive
        --email ahmad.munazar18@gmail.com
        --domains *.ahmad.studentdumbways.my.id 
      become: true
      become_user: root

```
```j2
# Cloudflare API credentials used by Certbot
dns_cloudflare_email= "ahmad.munazar18@gmail.com"
dns_cloudflare_api_key= "59c9d37614ceb06075f20e1cf30877d39a2dc"
```

