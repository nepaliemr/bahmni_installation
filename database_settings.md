- Stopping services
  ```
  service openmrs stop && service odoo stop && service bahmni-lab stop && service atomfeed-console stop && service bahmni-erp-connect stop
  ```
- Restarting services
```
service openmrs restart && service odoo restart && service bahmni-lab restart && service atomfeed-console restart && service bahmni-erp-connect restart 
```
- Starting services
```
service openmrs start && service odoo start && service bahmni-lab start && service atomfeed-console start && service bahmni-erp-connect start 
```

- Database backup
    - openMRS
```
mysql -u root -p openmrs > openmrs.sql
```
    - Odoo
```
psql -U odoo > odoo.sql
```
    - Lab
```
psql -U clinlims > clinlims.sql
```

- Database restore
 - openMRS
 ```
mysql -u root -p
drop database openmrs;
create database openmrs;
\q
mysql -u root -p openmrs < openmrs.sql
```
 - Lab
 ```
su postges
psql
drop database clinlims;
create databae clinlims;
\q
cntrl+d
psql -U clinlims < clinlims.sql
 ```
 - Odoo
 ```
su postges
psql
drop database odoo;
create databae odoo;
\q
cntrl+d
psql -U odoo < odoo.sql
su postges
psql
 alter database odoo owner to odoo;
 ```
