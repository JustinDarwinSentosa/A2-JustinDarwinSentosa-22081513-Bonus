# README.md

IMPORTANT: Once you've cloned this to your forked repository, ensure that you continuously update this document as you complete each task to demonstrate your ongoing progress.

Please include your shared repository link here:


Justins shared repository: https://github.com/JustinDarwinSentosa/A2-JustinDarwinSentosa-22081513.git


Make sure for **your case it is in Private**
## Access Database
1 **Plsql Cheat Sheet:**
You can refer to the PostgreSQL cheat sheet [here](https://www.postgresqltutorial.com/postgresql-cheat-sheet/).

2 **Know the Container ID:**
To find out the container ID, execute the following command:
   ```bash
   docker ps
    9958a3a534c9   testsystem-nginx           "/docker-entrypoint.…"   6 minutes ago   Up 6 minutes   0.0.0.0:80->80/tcp   testsystem-nginx-1
    53121618baa4   testsystem-frontend        "docker-entrypoint.s…"   6 minutes ago   Up 6 minutes   3000/tcp             testsystem-frontend-1
    c89e46ac94b0   testsystem-api             "docker-entrypoint.s…"   6 minutes ago   Up 6 minutes   5000/tcp             testsystem-api-1
    9f4aea7cf538   postgres:15.3-alpine3.18   "docker-entrypoint.s…"   6 minutes ago   Up 6 minutes   5432/tcp             testsystem-db-1
   ```
3. Running the application

**docker compose command:**
   ```bash
   docker compose up --build
   ```

4 **Access postgreSQL in the container:**
Once you have the container ID, you can execute the container using the following command:
You will see the example of running the PostgreSQL inside the container.
   ```bash
   docker exec -it testsystem-db-1 psql -U postgres
   choiruzain@MacMarichoy TestSystem % docker exec -it testsystem-db-1 psql -U postgres                                       
   psql (15.3)
   Type "help" for help.
   
   postgres=# \dt
             List of relations
    Schema |   Name   | Type  |  Owner   
   --------+----------+-------+----------
    public | contacts | table | postgres
    public | phones   | table | postgres
   (2 rows)
  
    postgres=# select * from contacts;
    id |  name  |         createdAt         |         updatedAt         
   ----+--------+---------------------------+---------------------------
     1 | Helmut | 2024-08-08 11:57:57.88+00 | 2024-08-08 11:57:57.88+00
    (1 row)
    postgres=# select * from phones;
    id | phone_type |   number    | contactId |         createdAt          |         updatedAt          
   ----+------------+-------------+-----------+----------------------------+----------------------------
     1 | Work       | 081431      |         1 | 2024-08-08 11:59:04.386+00 | 2024-08-08 11:59:04.386+00


postgres=# select * from contacts;
   ```
Replace `container_ID` with the actual ID of the container you want to execute.

## Executing API

### Contact API


1. Add contacts API  (POST)
```bash

curl -X POST http://localhost/api/contacts \                                       
-H "Content-Type: application/json" \
-d '{
  "name": "John Doe",
  "address": "123 Main Street"
}'
{"id":7,"name":"John Doe","updatedAt":"2024-12-07T01:52:59.397Z","createdAt":"2024-12-07T01:52:59.397Z"}% 

```
2 Get contacts API  (GET)

```bash
http get http://localhost/api/contacts

curl -X GET http://localhost/api/contacts                                       
[{"id":6,"name":"John Doe","createdAt":"2024-12-07T01:23:47.234Z","updatedAt":"2024-12-07T01:23:47.234Z"}]%  

```

3. Show/create the API commmand to delete the contacts (DELETE)

```bash

justindarwin@Justins-MBP Assignment2-main % curl -X DELETE http://localhost/api/contacts/6                                  
{"message":"Contact was deleted successfully!"}%  

```

4. Show/create the API command to edit the contacts (PUT)

```bash

justindarwin@Justins-MBP Assignment2-main % curl -X PUT http://localhost/api/contacts/7 \
-H "Content-Type: application/json" \
-d '{
  "name": "John Smith",
  "address": "12 Main Street" 
}'
{"message":"Contact was updated successfully."}%  

```

### Phone API

1. Add contacts API  (POST)
```bash

curl -X POST http://localhost/api/contacts \                                       
-H "Content-Type: application/json" \
-d '{
  "name": "John Doe",
  "address": "123 Main Street"
}'
{"id":7,"name":"John Doe","updatedAt":"2024-12-07T01:52:59.397Z","createdAt":"2024-12-07T01:52:59.397Z"}% 

```
2 Get contacts API  (GET)

```bash
curl -X GET http://localhost/api/contacts/9/phones 
[{"id":14,"phone_type":"","phone_number":"69","contactId":9,"createdAt":"2024-12-07T10:38:51.901Z","updatedAt":"2024-12-07T10:38:51.901Z"}]%

```

3. Show/create the API commmand to delete the contacts (DELETE)

```bash

justindarwin@Justins-MBP Assignment2-main % curl -X DELETE http://localhost/api/contacts/6                                  
{"message":"Contact was deleted successfully!"}%  

```

4. Show/create the API command to edit the contacts (PUT)

```bash

justindarwin@Justins-MBP Assignment2-main % curl -X PUT http://localhost/api/contacts/7 \
-H "Content-Type: application/json" \
-d '{
  "name": "John Smith",
  "address": "12 Main Street" 
}'
{"message":"Contact was updated successfully."}%  

```