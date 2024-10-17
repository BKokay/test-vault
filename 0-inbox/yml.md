---
hosts: all

gather_facts: false

become: true

vars:

deployment:

gitlab_url: https://gitlab.infoware.de/api/v4/projects/web%2Fdemo%2Ffuel-saver-api/jobs/artifacts/main/download?job=maven-package

artifact_jar: target/fuel-saver-api-0.0.1-SNAPSHOT.jar

deployment_jar: /home/fuel-saver-api/fuel-saver-api.jar

authorized_keys_file: maptrip-storage/home/maptripstorage/ssh/authorized_keys

application:

port: 8080

logpath: /var/log/fuel-saver-api

openjdk: openjdk-17-jdk

service:

name: fuel-saver-api

user: fuel-saver-api

group: fuel-saver-api

file: maptrip-storage/etc/systemd/system/maptripstorage.service

database:

version: 16

port: 5432

name: maptripstorage

user: maptripstorage-db

password: lfdi0f436h65gnjm67L46wg4ujc

tasks:

- name: Install Postgres and create database

ansible.builtin.include_role:

name: postgres

vars:

postgres_version: "{{ database.version }}"

postgres_port: "{{ database.port }}"

db_name: "{{ database.name }}"

db_user: "{{ database.user }}"

db_password: "{{ database.password }}"

tags:

- install

- name: Install application and service

ansible.builtin.include_role:

name: runnable-jar-application

vars:

application_port: "{{ application.port }}"

application_logpath: "{{ application.logpath }}"

gitlab_url: "{{ deployment.gitlab_url }}"

artifact_jar: "{{ deployment.artifact_jar }}"

deployment_jar: "{{ deployment.deployment_jar }}"

authorized_keys_file: "{{ deployment.authorized_keys_file }}"

service_name: "{{ service.name }}"

service_user: "{{ service.user }}"

service_group: "{{ service.group }}"

service_file: "{{ service.file }}"

tags:

- install

  

- name: Create backup script

ansible.builtin.copy:

dest: "/home/{{ service.user }}/database_backup.sh"

content: |

#!/bin/bash

db_user={{ database.user }}

db_name={{ database.name }}

backup_dir=/home/{{ service.user }}/backup/{{ service.name }}

backup_file=$backup_dir/{{ service.name }}-$(date +%Y%m%d_%H%M).backup.gz

# Create dir and dump in custom format (pg_restore)

mkdir -p $backup_dir

PGPASSWORD={{ database.password }} pg_dump --clean --create --format=custom -U $db_user $db_name | gzip > $backup_file

owner: "{{ service.user }}"

group: "{{ service.user }}"

mode: u=rwx,g=r,o=r

tags:

- install

- backup

- name: Create cron job for backup

ansible.builtin.cron:

name: "Daily backup database"

hour: "00"

minute: "00"

job: "/home/{{ service.user }}/database_backup.sh"

user: "{{ service.user }}"

tags:

- install

- backup