ansible-playbook -i inventory/hosts.yml playbooks/fuel-saver-api.yml
-l ih-fuelsaver-01 --tags "install"

[[Connect to postgres from fuelsaver]]
then to remove tables: 
`DROP TABLE fuel_saver.driver`

to see contents of db: 
`\dt *.*`

