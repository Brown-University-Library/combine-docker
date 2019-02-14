## First Build Notes

### Create MySQL combine database.

internal:
```
mysql -h 10.5.0.4 -u root -pcombine < /tmp/combine.sql
```

docker:
```
docker-compose run combine-django /bin/bash -c "mysql -h 10.5.0.4 -u root -pcombine < /tmp/combine.sql"
```

### Run Migrations

internal:
```
./manage.py makemigrations
./manage.py migrate
echo "from django.contrib.auth.models import User; User.objects.create_superuser('combine'"," 'root@none.com'"," '{{ django_combine_user_password }}')" | python /opt/combine/manage.py shell
```

docker:
```
docker-compose run combine-django /bin/bash -c "/tmp/combine_db_prepare.sh"
```


### ToDo

  * if dockerized, handle not checking supervisor for celery status
  * configure Mongo host
  * configure elasticsearch host