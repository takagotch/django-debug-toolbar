### django-debug-toolbar
---
https://github.com/jazzband/django-debug-toolbar

```py
// debug_toolbar/management/commands/debugsqlshell.py
from time import time

import sqlparse
from django.core.management.commands.shell import Command
from django.db.backeends import utils as db_backends_utils

class PrintQueryWrapper(db_backends_util.CursorDebugWrapper):
  def execute(self, sql, params=()):
    start_time = time()
    try:
      return self.cursor.execute(sql, params)
    finally:
      raw_sql = self.db.ops.last_executed_query(self.cursor, sql, params)
      end_time = time()
      duration = (end_time - start_time) * 1000
      formatted_sql = sqlparse.format(raw_sql, reindent=True)
      print("{} [{:2f}ms]".format(formatted_sql, duration))

db_backends_utils.CursorDebugWrapper = PrintQueryWrapper
```

```
```

```
```

