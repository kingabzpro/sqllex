# SQLite3x.executemany

```python
def executemany(
        self,
        script: AnyStr = None,
        values: Tuple[Tuple] = None,
        request: SQLRequest = None
) -> Union[List, None]:
    """
    Execute any SQL-script for many values sets, or execute SQLRequest
    Parameters
    ----------
    script : AnyStr
        single or multiple SQLite script(s), might contains placeholders
    values : Tuple[Tuple]
        Values for placeholders if script contains it
    request : SQLRequest
        Instead of script and values might execute full request
    Returns
    ----------
    Union[List, None]
        Database answer if it has
    """
```


## Examples

```python

from sqllex import *
from sqllex.types import SQLRequest

db = SQLite3x(path='database.db')

db.execute(
    script="""
    CREATE TABLE users (
        id INTEGER PRIMARY KEY UNIQUE,
        name TEXT
    )
    """
)

db.executemany(
    script="""
    INSERT INTO users (id, text) VALUES (?, ?)
    """,
    values=((1, 'Alex'), (2, 'Bob'))
)


request = SQLRequest(
    script="""
    INSERT INTO users (id, text) VALUES (?, ?)
    """,
    values=((3, 'Cate'), (4, 'Dex'))
)

db.executemany(request=request)

```


### [Back to home](README.md)