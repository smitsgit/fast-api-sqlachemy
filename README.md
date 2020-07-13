#### Alembic Database Migration

Working Dir 
- /Users/smital/PycharmProjects/fast-api-sqlachemy/sql_app

#### Initialize the alembic
```.shell script
cd /Users/smital/PycharmProjects/fast-api-sqlachemy/sql_app
alembic init alembic
```

#### Without the PYTHONPATH
```shell script
 File "/Users/smital/PycharmProjects/fast-api-sqlachemy/.venv/lib/python3.7/site-packages/alembic/util/compat.py", line 184, in load_module_py
    spec.loader.exec_module(module)
  File "<frozen importlib._bootstrap_external>", line 728, in exec_module
  File "<frozen importlib._bootstrap>", line 219, in _call_with_frames_removed
  File "alembic/env.py", line 27, in <module>
    from sql_app.models import Base
ModuleNotFoundError: No module named 'sql_app'
```
#### Changes in the alembic/env.py

```python
# add your model's MetaData object here
# for 'autogenerate' support
# from myapp import mymodel
# target_metadata = mymodel.Base.metadata
from sql_app.models import Base
target_metadata = Base.metadata
```

#### changes to the alembic.ini
wihtout the single or double quotes
```ini
sqlalchemy.url = sqlite:///..sql_app.db
```

#### Create the migrations
```shell script
export PYTHONPATH=export PYTHONPATH=/Users/smital/PycharmProjects/fast-api-sqlachemy
alembic stamp head
alembic revision -m "Add the inital schema"
```

## Change the model schema 
```shell script 
alembic revision --autogenerate -m "Add new columns" 
alembic upgrade head  # Without this the change wont take place 
