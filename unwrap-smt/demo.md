# Setup Kafka Connectors
``` bash
curl -i -X POST -H "Accept:application/json" -H  "Content-Type:application/json" http://localhost:8083/connectors/ -d @es-sink.json
curl -i -X POST -H "Accept:application/json" -H  "Content-Type:application/json" http://localhost:8083/connectors/ -d @source.json
curl -i -X POST -H "Accept:application/json" -H  "Content-Type:application/json" http://localhost:8083/connectors/ -d @jdbc-sink.json
```

# Initial State of the data
``` bash
docker-compose -f docker-compose.yaml exec mysql bash -c 'mysql -u $MYSQL_USER  -p$MYSQL_PASSWORD inventory -e "select * from customers"'

docker-compose -f docker-compose.yaml  exec postgres bash -c 'psql -U $POSTGRES_USER $POSTGRES_DB -c "select * from customers"'

```

# Test Data
```bash
docker-compose -f docker-compose.yaml exec mysql bash -c 'mysql -u $MYSQL_USER  -p$MYSQL_PASSWORD inventory'


insert into customers values(default, 'John', 'Doe', 'john.doe@example.com');
update customers set first_name='Jane', last_name='Roe' where last_name='Doe';
delete from customers where email='john.doe@example.com';
```