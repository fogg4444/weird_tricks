# Django
---

### Reset Migrations
https://simpleisbetterthancomplex.com/tutorial/2016/07/26/how-to-reset-migrations.html

```
find . -path "*/migrations/*.py" -not -name "__init__.py" -delete
```
```
find . -path "*/migrations/*.pyc"  -delete
```

Drop database or:
```
rm ./db.sqlite3
```
