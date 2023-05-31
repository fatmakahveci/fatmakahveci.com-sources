---
title: datetime
description: datetime
summary: "Updated by Fatma, Mar 28, 2023."
date: 28-03-2023
categories:
  - "Coding"
tags:
  - "Python"
  - "coding"
  - "algorithms"
  - "data structures"
comments: true
---
```python
from datetime import datetime, date, time, timedelta

dt = datetime.now() # 2022-01-20 09:26:03.478039

dt = date.today() # 2022-01-20

dt = datetime.date(2022, 01, 20) # 2022-01-20

dt = datetime(2022, 01, 20, 20, 30, 21) # dt.day 20 # dt.minute 30

t = time() # 00:00:00 # a.hour 0 # a.minute 0
t = time(11, 34, 56) # 11:34:56
t = time(hour=11, minute=34, second=56) # 11:34:56

# strftime formats a datetime as a string
dt.strftime('%m/%d/%Y %H:%M') # 01/20/2022 20:30

dt.replace(minute=0, second=0) #

t1 = date(year = 2018, month = 7, day = 12)
t2 = date(year = 2017, month = 12, day = 23)
t3 = t1 - t2 # t3 = 201 days, 0:00:00

t4 = datetime(year = 2018, month = 7, day = 12, hour = 7, minute = 9, second = 33)
t5 = datetime(year = 2019, month = 6, day = 10, hour = 5, minute = 55, second = 13)
t6 = t4 - t5 # t6 = -333 days, 1:14:20
```
