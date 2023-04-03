---
title: Concurrency
description: Concurrency
summary: "Updated by Fatma, Mar 28, 2023."
date: 28-03-2023
categories:
  - "Coding"
tags:
  - "Python"
  - "coding"
  - "algorithms"
  - "data structures"
---

## Concurrency in Python

### asyncio's _Hello World!_

```python
import asyncio

async def main():
  await asyncio.sleep(2)
  print('Hello World!')


asyncio.run(main())
```

### Awaitable

- An object that can be used in an `await` expression.

### Coroutine

- A coroutine can be thought of as executing a lightweight thread.
- It is a special Python function that behaves as a generator and yields control back to the event loop when it blocks.
- It is a specialized version of a Python `generator` function.
- It is like a regular function with the superpower that can be paused when we have a potentially long-running task and then resumed when that task is finished.
  - When a long-running operation is complete, we can "wake up" our paused coroutine and finish executing any other code in that coroutine.
  - While a paused coroutine is waiting for the operation it paused for to finish, we can run other code.

![subroutine_vs_coroutine](/img/subroutine_vs_coroutine.png)

#### 1. Creating coroutines with the `async` keyword

- Coroutines aren't executed when we call them directly. Instead, we create a coroutine object that can be run later.

```python
def add_one(number: int) -> int:
  return number + 1

async def coroutine_add_one(number: int) -> int:
  return number + 1

function_result = add_one(1)
coroutine_result = asyncio.run(coroutine_add_one(1))

print(f'Function result is {function_result} and the type is {type(function_result)}')
print(f'Coroutine result is {coroutine_result} and the type is {type(coroutine_result)}')
```

##### 1.1. `asyncio.run` steps

- It creates a brand-new event.
- It takes the coroutine we pass into it and runs it until it completes, returning the result.
- It cleans anything left running after the main coroutine finishes.
- Once everything has finished, it shuts down and closes the event loop.

#### 2. Pausing execution with the `await` keyword

- `await` is usually followed by a call to a coroutine.
- When we hit an `await` expression, we pause our parent coroutine and run the coroutine in the await expression. Once it is finished, we resume the parent coroutine and assign the return value.
- `awaitable` is the object that can be used in `await` expressions.

```python
import asyncio

async def add_one(number: int) -> int:
  return number + 1

async def main() -> None:
  one_plus_one = await add_one(1) # pause and wait for the result of add_one(1)
  two_plus_one = await add_one(2) # pause and wait for the result of add_one(2)

  print(one_plus_one)
  print(two_plus_one)

asyncio.run(main())
```

#### Long-running coroutines with sleep

##### `asyncio.sleep`

- It makes a coroutine sleep for a given number of seconds.
- It is a coroutine so we must use it with the `await` keyword.

```python
import asyncio
from util import delay # our module

async def add_one(number: int) -> int:
  return number + 1

async def hello_world_message() -> str:
  await delay(1)
  return 'Hello world!'

async def main() -> None:
  message = await hello_world_message()
  one_plus_one = await add_one(1) 
  print(one_plus_one)
  print(message)

asyncio.run(main())
```

### Event Loop

- The event loop is the core of every asyncio application.
- Event loops run asynchronous tasks and callbacks, perform network IO operations, and run subprocesses.

### Future

- `Future` is an awaitable object. Coroutines can await on Future objects until they either have a result or an exception set or until they are cancelled.

- A `future` is an awaitable object that contains a single value that you expect to get at some point or time in the future but may not have yet.
- Futures can also be used in `await` expressions so we're saying "pause" until the future has a value set that I can work with, and once I have a value, wake up and let me process it.
- We call `set_exception` to set an exception on the `future`.
- In the world of `asyncio`, you should rarely need to deal with `future`s.

```python
from asyncio import Future
import asyncio

def make_request() -> Future:
  future = Future()
  asyncio.create_task(set_future_value(future)) # create a task asynchronously set the value of the future
  return future

async def set_future_value(future) -> None:
  await asyncio.sleep(1) # wait 1 sec before setting the value of future
  future.set_result(42)

async def main():
  future = make_request()
  print(f'Is the future done? {future.done()}')
  value = await future # pause main until the future is set
  print(f'Is the future done? {future.done()}')
  print(value)

asyncio.run(main())
```

- `async for` and `async with`

### Task

- A `Future-like` object that runs a Python `coroutine`.
- `task` directly inherits from `future`.
- It is a combination of both a `coroutine` and `future`.
- When we create a `task`, we create an empty `future` and run the `coroutine`. Then, when the coroutine has completed with either an exception or a result, we set the result or exception of the future.
- Each task maintains a single stack, and its execution pointer as well.
- A task object can be used to monitor the status of the underlying coroutine.

#### Running concurrently with tasks

- A task makes the coroutine run concurrently.
- It is a wrapper around the coroutine that schedules a coroutine to run on the event loop as soon as possible so we can execute multiple tasks at roughly the same time.

##### `asyncio.create_task`

- It schedules the execution of a `Coroutines`, gives it to run, and returns a Task object instantly.
- It gives a coroutine to run and returns a task object instantly.
- It takes a coroutine object as a parameter and returns a `Task` object.
- Once we have a `Task` object, we can put it in an `await` expression that will extract the return value once it is complete.
- We should usually use an `await` keyword on our tasks at some point in our application.

```python
import asyncio
from util import delay

async def main():
  sleep_for_three = asyncio.create_task(delay(3))
  print(type(sleep_for_three))
  result = await sleep_for_three
  print(result)

asyncio.run(main())
```

#### Running multiple tasks concurrently

```python
import asyncio
from util.delay import delay

async def main():
  sleep_for_three = asyncio.create_task(delay(3))
  sleep_again = asyncio.create_task(delay(3))
  sleep_once_more = asyncio.create_task(delay(3))

  await sleep_for_three
  await sleep_again
  await sleep_once_more

asyncio.run(main())
```

```python
import asyncio
from util.delay import delay

async def hello_every_second():
  for i in range(2):
    await asyncio.sleep(1)
    print('I am running other code while I am running')

async def main():
  first_delay = asyncio.create_task(delay(3))
  second_delay = asyncio.create_task(delay(3))

  await hello_every_second()
  await first_delay
  await second_delay

asyncio.run(main())
```

#### Canceling tasks

- Cancelling a task will cause that task to raise a `CancelledError` when we `await` it, which we can then handle as needed.
- `CancelledError` can only be thrown from an `await` statement. This means that if we call to cancel on a task when it is executing plain Python code, that code will run until completion until we hit the next `await` statement (if one exists) and a `CancelledError` can be raised. Calling cancel won’t magically stop the task in its tracks; it will only stop the task if you’re currently at an `await` point or its next `await` point.

```python
import asyncio
from util.delay import delay
from asyncio import CancelledError

async def main():
  long_task = asyncio.create_task(delay(10))
  seconds_elapsed = 0
  while not long_task.done():
    print('Task is not finished, checking again in a second.')
    await asyncio.sleep(1)
    seconds_elapsed += 1
    if seconds_elapsed == 5:
      long_task.cancel()

  try:
    await long_task
  except CancelledError:
    print('Our task was cancelled.')

asyncio.run(main())
```

#### Setting a timeout and cancelling with `wait_for`

- It takes in a coroutine or task object, and a timeout is specified in seconds. Then, it returns a coroutine that we can `await`.
- If the task exceeds the specified timeout, a `TimeoutException` will be raised. Once we have reached the timeout threshold, the task will automatically be cancelled.

```python
import asyncio
from util.delay import delay

async def main():
  delay_task = asyncio.create_task(delay(2))
  try:
    result = await asyncio.wait_for(delay_task, timeout=1)
    print(result)
  except asyncio.exceptions.TimeoutError:
    print('Got a timeout!')
    print(f'Was the task cancelled? {delay_task.cancelled()}')

asyncio.run(main())
```

#### Shielding a task from cancellation `shield`

- It prevents cancellation of the coroutine we pass in, giving it a 'shield', which cancellation requests then ignore.

```python
import asyncio
from util.delay import delay

async def main():
  delay_task = asyncio.create_task(delay(10))

  try:
    result = await asyncio.wait_for(asyncio.shield(delay_task), 5)
    print(result)
  except asyncio.exceptions.TimeoutError:
    print('Task took longer than five seconds, it will finish soon')
    result = await delay_task
    print(f'finished in {result} second(s)')

asyncio.run(main())
```

### Running in Threads

- `asyncio.to_thread(<function>, /, *args, **kwargs)`

[Ref](https://docs.python.org/)

---

## aiohttp

### Asycnhronous HTTP client/server for asyncio and python (`aiohttp`)

- `pip install aiohttp`
- It makes asyncio-friendly web requests.
- It uses non-blocking sockets to make web requests and returns coroutines for them, which then can `await` for a result.
- It has not only support as an HTTP client but also has the functionality to create asyncio-ready web application servers as well.
- It provides web server functionality in the web module.

#### Asynchronous [context managers](../context_manager.md)

- `with` works for the synchronous. `async with` works for the asynchronous.
- It acquires and closes HTTP sessions cleanly with two special coroutine methods:
  1. `__aenter__` acquires a resource.
  2. `__aexit__` closes the resource.
- Normally, you won't need to write your own async database connections and transactions.

#### Session

- `aiohttp` can create a session by using `async with` and `aiohttp.ClientSession`.
- Within a session, you can keep many connections open, which can then be recycled (connection pooling).
- A session object has methods to make any number of web requests, such as `GET`, `PUT`, and `POST`.
- A `ClientSession` will create a default maximum of 100 connections by default. To change this limit, we can create an instance of an `aiohttp TCPConnector` specifying the maximum number of connections and passing that to the `ClientSession`.

#### Setting and handling timeouts for groups of requests and cancelling requests

- `ClientTimeout` data structure can specify timeouts for an entire request, establishing a connection, or reading data.

```python
import asyncio
from aiohttp import ClientSession, ClientTimeout
from util import fetch_status

async def main():
  session_timeout = ClientTimeout(total=1, connect=.1)
  async with ClientSession(timeout=session_timeout) as session:  # creates a session
    await fetch_status(session, 'https://example.com')  # returns a status code for the given URL

asyncio.run(main())
```

#### Running tasks concurrently

```python
import asyncio
from util import async_timed, delay

@async_timed()
async def main() -> None:
  delay_times = [ 3, 3, 3 ]
  tasks = [ await asyncio.create_task(delay(seconds)) for seconds in delay_times ]
  [ await task for task in tasks ]

asyncio.run(main())
```

- It creates several tasks all at once in the tasks list. Once we have created all the tasks, we await their completion in a separate list comprehension. This works because `create_task` returns instantly, and we don't do any awaiting until all the tasks have been created. This ensures that it only requires at most the maximum pause in `delay_times`, giving a runtime of about 3 seconds.

- **Drawbacks:**
  - If one of our coroutines finishes long before the others, we'll be trapped in the second list comprehension waiting for all other coroutines to finish.
  - If one of our coroutines has an exception, it will be thrown when we await the failed task. This means that we won't be able to process any tasks that were completed successfully because that one exception will halt our execution.

#### Running requests concurrently with `gather`

- If an awaitable we pass in is a coroutine, `gather` will automatically wrap it in a task to ensure that it runs concurrently.
- It returns an awaitable.
- When we use it in an `await` expression, it will pause until all awaitables that we passed into it are complete. Then, it will return a list of the completed results.
- `gather` guarantees the results will be returned in the order we passed them in.

```python
import asyncio
from aiohttp import ClientSession
from util import async_timed, fetch_status

@async_timed()
async def main() -> None:
  async with ClientSession as session:
    urls = [ 'https://example.com' for _ in range(1000) ]
    requests = [ fetch_status(session, url) for url in urls ] # generates a list of coroutines for each request we want to make
    status_codes = await asyncio.gather(*requests) # waits for all requests to complete

asyncio.run(main())
```

##### Handling exceptions with `gather`

- `gather` gives an optional parameter `return_exceptions`, which can specify how we want to deal with exceptions from our awaitables.
  - `return_exceptions=False` is the default. Both a coroutine and `gather` will throw an exception when we `await` it. Even if a coroutine is failed, our other coroutines will continue to run as long as we handle the exception, or the exception does not result in the event loop stopping and cancelling the tasks.
  - `return_exceptions=True` `gather` will return any exceptions as part of the result list it returns when we await it. `gather` will not throw any exceptions itself, and we'll be able to handle all exceptions as we wish.

- **Drawbacks:**
  - Cancelling tasks is not easy if one throws an exception.
  - Before we can process our results, we must wait for all coroutines to finish.

#### Processing requests `as_completed`

- It takes a list of awaitables and returns an iterator of futures. We can then iterate over these futures, awaiting each one.
- There is no deterministic ordering of results since we have no guarantees as to which requests will complete first.

```python
import asyncio
from aiohttp import ClientSession
from util import fetch_status

async def main():
  async with ClientSession as session:
    fetchers = [ fetch_status(session, 'https://www.example.com', 1), # coroutine 1
                 fetch_status(session, 'https://www.example.com', 1), # coroutine 2
                 fetch_status(session, 'https://www.example.com', 10), # coroutine 3
               ]

    for finished_task in asyncio.as_completed(fetchers, timeout=2):  # If it takes longer than the timeout, each awaitable in the iterator will throw a TimeoutException when we await it.

      try:
        result = await done_task
        print(result)
      except asyncio.TimeoutError:
        print('We got a timeout error')

      for task in asyncio.tasks.all_tasks():
        print(task)

asyncio.run(main())
```

- **Drawbacks:**
  - The order is completely non-deterministic.
  - While we will correctly throw an exception and move on, any tasks created will still be running in the background.

#### Finer-grained control with `wait`

- It returns two sets:
  - 1. A set of tasks that are finished with either a result or an exception.
  - 2. A set of tasks that are still running.

##### Waiting for all tasks to complete: `return_when=asyncio.ALL_COMPLETED`

- We wait until all tasks are completed before returning.
- Handling exceptions:
  - 1. We can use `await` and let the exception be thrown and wrap it in `try except` block to handle the exception.
  - 2. We can use `task.result()` and `task.exception()`.

```python
import asyncio
import logging

from aiohttp import ClientSession
from util import fetch_status

async def main() -> None:
  async with ClientSession as session:
    good_request = fetch_status(session, 'https://www.example.com')
    bad_request = fetch_status(session, 'python://bad'))
    fetchers = [ asyncio.create_task(good_request),
                 asyncio.create_task(bad_request)
               ]
  done, pending = await asyncio.wait(fetchers)
  for done_task in done:
    # result = await done_task will throw an exception
    if done_task.exception() is None: # checks to see if we have an exception
      print(done_task.result())
    else:
      logging.error("Request got an exception", exc_info=done_task.exception())

asyncio.run(main())
```

##### Watching for exceptions: `return_when=asyncio.FIRST_EXCEPTION`

- We want to handle exceptions to ensure responsiveness.
  - 1. If there is no exception, `FIRST_EXCEPTION` equals `ALL_COMPLETED`.
  - 2. If any task throws an exception, `wait` will immediately return once that exception is thrown.

```python
import asyncio
import logging

from aiohttp import ClientSession
from util import fetch_status

async def main() -> None:
  async with ClientSession as session:
    fetchers = [ asyncio.create_task(fetch_status(session, 'python://bad')),
                 asyncio.create_task(fetch_status(session, 'https://www.example.com', delay=3)),
                 asyncio.create_task(fetch_status(session, 'https://www.example.com', delay=3)),
    ]
  done, pending = await asyncio.wait(fetchers, return_when=asyncio.FIRST_EXCEPTION)
  for done_task in done:
    # result = await done_task will throw an exception
    if done_task.exception() is None: # checks to see if we have an exception
      print(done_task.result())
    else:
      logging.error("Request got an exception", exc_info=done_task.exception())
  for pending_task in pending:
    pending_task.cancel()
asyncio.run(main())
```

##### Processing results as they complete: `return_when=asyncio.FIRST_COMPLETED`

- To reach the result as soon as it completes.

```python
import asyncio
import logging

from aiohttp import ClientSession
from util import fetch_status

async def main() -> None:
  async with ClientSession as session:
    fetchers = [ asyncio.create_task(fetch_status(session, 'https://www.example.com')),
                 asyncio.create_task(fetch_status(session, 'https://www.example.com')),
                 asyncio.create_task(fetch_status(session, 'https://www.example.com')),
    ]
  done, pending = await asyncio.wait(fetchers, return_when=asyncio.FIRST_COMPLETED)
  for done_task in done:
    result = await done_task
asyncio.run(main())
```

###### Handling timeouts

- `wait` sets timeouts to specify how long we want all awaitables to complete with `timeout` parameter. If we exceed the timeout, it returns both done and pending tasks.
  - 1. **Coroutines are not cancelled:** We must explicitly loop over the tasks and cancel them.
  - 2. **Timeout errors are not raised:**  If the timeout occurs the wait returns all tasks are done and all tasks that are still pending up to that point when the timeout occurred.

```python
import asyncio
import logging

from aiohttp import ClientSession
from util import fetch_status

async def main() -> None:
  async with ClientSession as session:
    fetchers = [ asyncio.create_task(fetch_status(session, 'https://www.example.com')),
                 asyncio.create_task(fetch_status(session, 'https://www.example.com')),
                 asyncio.create_task(fetch_status(session, 'https://www.example.com', delay=3)),
    ]
  done, pending = await asyncio.wait(fetchers, timeout=1)
  for done_task in done:
    result = await done_task
asyncio.run(main())
```

- Tasks in the pending set are not cancelled and will continue to run despite the timeout.
- If we want to terminate the pending tasks, we explicitly loop through the pending set and call cancel on each task.

---

## async delay app

```python
import asyncio
import os
import shutil
import sys
import tty

from asyncio import StreamReader
from collections import deque
from typing import Callable, Deque, Awaitable


async def create_stdin_reader() -> StreamReader:
 stream_reader = asyncio.StreamReader()
 protocol = asyncio.StreamReaderProtocol(stream_reader)
 loop = asyncio.get_running_loop()
 await loop.connect_read_pipe(lambda: protocol, sys.stdin)
 return stream_reader

async def read_line(stdin_reader: StreamReader) -> str:
 def erase_last_char():
  move_back_one_char()
  sys.stdout.write(' ')
  move_back_one_char()
 delete_char = b'\x7f'
 input_buffer = deque()
 while ( input_char := await stdin_reader.read(1)) != b'\n':
  if input_char == delete_char:
   if len(input_buffer) != 0:
    input_buffer.pop()
    erase_last_char()
    sys.stdout.flush()
  else:
   input_buffer.append(input_char)
   sys.stdout.write(input_char.decode())
   sys.stdout.flush()
 clear_line()
 return b''.join(input_buffer).decode()

class MessageStore:
 def __init__(self, callback: Callable[[Deque], Awaitable[None]], max_size: int):
  self._deque = deque(maxlen=max_size)
  self._callback = callback

 async def append(self, item):
  self._deque.append(item)
  await self._callback(self._deque)

def save_cursor_position():
 sys.stdout.write('\0337')

def restore_cursor_position():
 sys.stdout.write('\0338')

def move_to_bottom_of_screen() -> int:
 _, total_rows = shutil.get_terminal_size()
 input_row = total_rows - 1
 sys.stdout.write(f'\033[{input_row}E')
 return total_rows

def move_to_top_of_screen():
 sys.stdout.write('\033[H')

def move_back_one_char():
 sys.stdout.write('\033[1D')

def delete_line():
 sys.stdout.write('\033[2K')

def clear_line():
 sys.stdout.write('\033[2K\033[0G')

async def sleep(delay: int, message_store: MessageStore):
 await message_store.append(f'Starting delay {delay}')
 await asyncio.sleep(delay)
 await message_store.append(f'Finished delay {delay}')


async def main():
 tty.setcbreak(sys.stdin)
 os.system('clear')
 rows = move_to_bottom_of_screen()

 async def redraw_output(items: deque):
  save_cursor_position()
  move_to_top_of_screen()
  for item in items:
   delete_line()
   print(item)
  restore_cursor_position()

 messages = MessageStore(redraw_output, rows-1)

 stdin_reader = await create_stdin_reader()

 while True:
  line = await read_line(stdin_reader)
  delay_time = int(line)
  asyncio.create_task(sleep(delay_time, messages))

asyncio.run(main())
```

---

## AsyncGenerator

- An async generator can be annotated by the generic type `AsyncGenerator[YieldType, SendType]`. For example,

```python
async def echo_round() -> AsyncGenerator[int, float]:
    sent = yield 0
    while sent >= 0.0:
        rounded = await round(sent)
        sent = yield rounded
```

- Unlike normal generators, async generators cannot return a value, so there is no ReturnType type parameter.

```python
async def coroutine_method():
    return 3

async def generator_method():
    yield 3

# This is correct
r = await coroutine_method()

# This will raise an exception!
r = await generator_method()
```

---

## async input reader

```python
import asyncio
import sys
from util.delay import delay
from util.create_stdin_reader import create_stdin_reader

async def main():
  stdin_reader = await create_stdin_reader()
  while True:
    delay_time = await stdin_reader.readline()
    asyncio.create_task(delay(int(delay_time)))

asyncio.run(main())
```

---

## Awaitables

![awaitables](/img/awaitables.png)

- When you call `await` you must call it on one of the following:

- **A coroutine object**, which is the return value of a coroutine function defined using async def.
  - The coroutine’s code will only be executed when it is awaited or wrapped in a task.

- **A future object**, which represents a process ongoing somewhere else which may have finished.
  - Awaiting a future will not cause code to be executed, but might pause your current task until another process has been completed.

- **An object which implements the `__await__` magic method**
  - What happens then could be anything, check the documentation for the object in question.

---

## Web Applications

### Creating web applications with [`aiohttp`](../aiohttp.md)

- Build async [REST API](../../api/rest_api.md)s with [`aiohttp`](../aiohttp.md)

#### `web` module of `aiohttp`

- We can define _endpoints(routes)_ with a `RouteTableDef`.
  - A `RouteTableDef` provides a decorator that lets us specify a request type (GET, POST, etc.) and a string representing the endpoint name.

### ASGI

### Creating ASGI web applications with Starlette

- Build a simple REST API with WebSocket support

### Using Django's asynchronous views

---

## Event loop

- It manages the execution of a set of Python functions and switches between them as they block and unblock.
- An event loop contains within a list of object calls called `Task`s.
- At any one time the event loop can only have one Task executing, whilst the other tasks in the loop are all paused.
- An event loop cannot forcibly interrupt a coroutine that is currently executing. A coroutine that is executing will continue executing until it yields control. The event loop serves to select which coroutine to schedule next and keeps track of which coroutines are blocked and unable to execute until some IO has been completed, but it only does these things when no coroutine is currently executing.

### Use `asyncio`'s non-blocking socket coroutines to allow multi-clients to connect properly

- When an event loop is triggered by either
  - a socket event happening or
  - a timeout triggering an iteration of the loop,
 waiting for coroutines will run until complete or hit the next `await` statement.

- When we hit an `await` in a coroutine that utilizes a non-blocking socket, it will register that socket with the system's selector and keep track that the coroutine is paused waiting for a result.

### Event loop coroutines for sockets

- They take in a socket and `await` until we have data to act on.

#### 1. `sock_accept`

- `connection, address = await loop.sock_accept(socket)` is analogous to `socket.accept` and will `await` the coroutine that it returns.
- It returns a tuple of a socket connection and a client address.

#### 2. `sock_recv`

- `data = await loop.sock_recv(socket)` will `await` until a socket has bytes we can process.

#### 3. `sock_sendall`

- `success = await loop.sock_sendall(socket, data)` will wait until all data we want to send to a socket has been sent and will return `None` on success.

---

## chat client

```python
import asyncio
import logging
import os
import sys
import tty
from asyncio import StreamReader, StreamWriter
from collections import deque
from util import create_stdin_reader, cursor, message_store
from util.message_store import MessageStore

async def read_and_send(message: str, writer: StreamWriter):
  writer.write((message + '\n').encode())
  await writer.drain()

async def listen_for_messages(reader: StreamReader, message_store: MessageStore):
  while (message := await reader.readline()) != b'':
    await message_store.append(message.decode())
  await message_store.append('Server closed connection')


async def main():
  tty.setcbreak(0)
  os.system('clear')
  rows = cursor.move_to_bottom_of_screen()

  async def redraw_output(items: deque):
    cursor.save_cursor_position()
    cursor.move_to_top_of_screen()
    for item in items:
      cursor.delete_line()
      print(item)
    cursor.restore_cursor_position()

  messages = MessageStore(redraw_output, rows-1)
  stdin_reader = await create_stdin_reader.create_stdin_reader()
  sys.stdout.write('Enter username: ')
  username = await cursor.read_line(stdin_reader)
  
  reader, writer = await asyncio.open_connection('127.0.0.1', 8000)
  writer.write(f'CONNECT {username}\n'.encode())
  await writer.drain()

  message_listener = asyncio.create_task(listen_for_messages(reader, messages))
  input_listener = asyncio.create_task(read_and_send(stdinreader, writer))

  try:
    await asyncio.wait([message_listener, input_listener], return_when=asyncio.FIRST_COMPLETED)
  except Exception as e:
    logging.exception(e)
    writer.close()
    await writer.wait_closed()

asyncio.run(main())
```

---

## chat server

```python
import asyncio
import logging
from asyncio import StreamReader, StreamWriter

class ChatServer:
  def __init__(self):
    self._username_to_writer = {}
  
  async def start_chat_server(self, host: str, port: int):
    server = await asyncio.start_server(self.client_connected, host, port)

    async with server:
      await server.serve_forever()
  
  async def client_connected(self, reader: StreamReader, writer: StreamWriter):
    command = await reader.readline()
    print(f'CONNECTED {reader} {writer}')
    command, args = command.split(b' ')
    print(command)
    # print(args)
    if command == b'CONNECT':
      username = args.replace(b'\r\n', b'').decode()
      self._add_user(username, reader, writer)
      await self._on_connect(username, writer)
    else:
      logging.error('Got invalid command from client, disconnecting.')
      writer.close()
      await writer.wait_closed()

  def _add_user(self, username: str, reader: StreamReader, writer: StreamWriter):
    self._username_to_writer[username] = writer
    asyncio.create_task(self._listen_for_messages(username, reader))

  async def _remove_user(self, username: str):
    writer = self._username_to_writer[username]
    del self._username_to_writer[username]
    try:
      writer.close()
      await writer.wait_closed()
    except Exception as e:
      logging.exception('Error closing client writer, ignoring.', exc_info=e)

  async def _notify_all(self, message: str):
    inactive_users = []
    for username, writer in self._username_to_writer.items():
      try:
        writer.write(message.encode())
        await writer.drain()
      except ConnectionError as e:
        logging.exception('Could not write to client.', exc_info=e)
        inactive_users.append(username)
    [ await self._remove_user(username) for username in inactive_users ]

  async def _listen_for_messages(self, username: str, reader: StreamReader):
    try:
      while (data := await asyncio.wait_for(reader.readline(), 60)) != b'':
        await self._notify_all(f'{username}: {data.decode()}')
      await self._notify_all(f'{username} has left the chat\n')
    except Exception as e:
      logging.exception('Error reading from client.', exc_info=e)
      await self._remove_user(username)

  async def _on_connect(self, username: str, writer: StreamWriter):
    writer.write(f'Welcome! {len(self._username_to_writer)} user(s) are online!\n'.encode())
    await writer.drain()
    await self._notify_all(f'{username} connected!\n')

async def main():
  chat_server = ChatServer()
  await chat_server.start_chat_server('127.0.0.1', 8000)

asyncio.run(main())
```

---

## cli sql

```python
## The code creates some errors

import asyncio
import asyncpg
import os
import shutil
import sys
import tty

from collections import deque
from asyncio import StreamReader
from asyncpg import Pool
from typing import Callable, Deque, Awaitable

async def create_stdin_reader() -> StreamReader:
 stream_reader = asyncio.StreamReader()
 protocol = asyncio.StreamReaderProtocol(stream_reader)
 loop = asyncio.get_running_loop()
 await loop.connect_read_pipe(lambda: protocol, sys.stdin)
 return stream_reader

class MessageStore:
 def __init__(self, callback: Callable[[Deque], Awaitable[None]], max_size: int):
  self._deque = deque(maxlen=max_size)
  self._callback = callback

 async def append(self, item):
  self._deque.append(item)
  await self._callback(self._deque)

def save_cursor_position():
 sys.stdout.write('\0337')

def restore_cursor_position():
 sys.stdout.write('\0338')

def move_to_bottom_of_screen() -> int:
 _, total_rows = shutil.get_terminal_size()
 input_row = total_rows - 1
 sys.stdout.write(f'\033[{input_row}E')
 return total_rows

def move_to_top_of_screen():
 sys.stdout.write('\033[H')

def move_back_one_char():
 sys.stdout.write('\033[1D')

def delete_line():
 sys.stdout.write('\033[2K')

def clear_line():
 sys.stdout.write('\033[2K\033[0G')


async def run_query(query: str, pool: Pool, message_store: MessageStore):
 async with pool.acquire() as connection:
  try:
   result = await connection.fetchrow(query)
   await message_store.append(f'Fetched {len(result)} rows from: {query}')
  except Exception as e:
   await message_store.append(f'Got exception {e}: from {query}')

async def read_line(stdin_reader: StreamReader) -> str:
 def erase_last_char():
  move_back_one_char()
  sys.stdout.write(' ')
  move_back_one_char()
 delete_char = b'\x7f'
 input_buffer = deque()
 while ( input_char := await stdin_reader.read(1)) != b'\n':
  if input_char == delete_char:
   if len(input_buffer) != 0:
    input_buffer.pop()
    erase_last_char()
    sys.stdout.flush()
  else:
   input_buffer.append(input_char)
   sys.stdout.write(input_char.decode())
   sys.stdout.flush()
 clear_line()
 return b''.join(input_buffer).decode()

async def main():
 tty.setcbreak(0)
 os.system('clear')
 rows = move_to_bottom_of_screen()

 async def redraw_output(items: deque):
  save_cursor_position()
  move_to_top_of_screen()
  for item in items:
   delete_line()
   print(item)
  restore_cursor_position()

 messages = MessageStore(redraw_output, rows - 1)
 stdin_reader = await create_stdin_reader()

 async with asyncpg.create_pool( host='127.0.0.1',
         port=5432,
         user='postgres',
         password='password',
         database='products',
         min_size=6,
         max_size=6) as pool:
  while True:
   query = await read_line(stdin_reader)
   asyncio.create_task(run_query(query, pool, messages))

asyncio.run(main())
```

---

## Designing an `asyncio` echo server

- `listen_for_connections` coroutine will loop forever and listen for any incoming connections.
- It will allow other code to run concurrently, while we’re paused and waiting for a connection.
- We need to handle multiple connections to read and write at the same time so we create a task for each connection.
- When we await a task that failed, the exception will get thrown where we perform the await, and the traceback will reflect that.

```python
import asyncio
import logging
import signal
import socket

from asyncio import AbstractEventLoop
from typing import List

async def echo(connection: socket, loop: AbstractEventLoop) -> None:
  try:
    while data := await loop.sock_recv(connection, 1024): # loop forever waiting for data from a client connection
      if data == b'boom\r\n':
        raise Exception("Unexpected network error") # a line from the output: Task exception was never retrieved
      # no exception is thrown to call stack and no cleanup here `await` is required
      await loop.sock_sendall(connection, data)
  except Exception as ex:
    logging.exception(ex)
  finally:
    connection.close()

echo_tasks = []

async def connection_listener(server_socket: socket, loop: AbstractEventLoop) -> None:
  while True:
    connection, address = await loop.sock_accept(server_socket)
    connection.setblocking(False)
    print(f'Got a connection from {address}')
    echo_task = asyncio.create_task(echo(connection, loop)) # whenever we get a connection, create an echo task to listen for client data
    echo_tasks.append(echo_task)

class GracefulExit(SystemExit):
  pass

def shutdown() -> None:
  raise GracefulExit()

async def close_echo_tasks(echo_tasks: List[asyncio.Task]) -> None:
  waiters = [asyncio.wait_for(task, 2) for task in echo_tasks] # `asyncio.wait_for` sets timeouts on a task
  for task in waiters:
    try:
      await task
    except asyncio.exceptions.TimeoutError:
      pass

async def main():
  server_socket = socket.socket()
  server_socket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)

  server_address = ('127.0.0.1', 8000)
  server_socket.setblocking(False)
  server_socket.bind(server_address)
  server_socket.listen()

  for signame in [ 'SIGINT', 'SIGTERM' ]:
    loop.add_signal_handler(getattr(signal, signame), shutdown) # listen to the event, it can safely interact with the event loop
  await connection_listener(server_socket, loop)

loop = asyncio.new_event_loop() # create a new event loop

try:
  loop.run_until_complete(main()) # take a coroutine and run it until it finishes
except GracefulExit:
  loop.run_until_complete(close_echo_tasks(echo_tasks))
finally:
  loop.close()
```

---

## `requests`

- This library abstracts away the complexities of making HTTP requests.
- It does not perform well with `asyncio` because it uses blocking sockets.

```python
"""
# `response` is a `Response` object, with which we can get
# all the information we need from this object.
"""
import requests

# `GET` retrieves resources from a given API. It is read-only.
response = requests.get('<url>') 

# `HEAD` asks for a response identical to that of `GET`,
# but only returns the status_code or HTTP header.
response = requests.head('<url>')
response.status_code # 200
response.headers["Content-Type"] # 'application/json; charset=utf-8'

# `POST` creates a new resource.
response = requests.post('<url>', data = {'key':'value'})

# `PUT` updates an existing resource.
response = requests.put('<url>', data = {'key':'value'})

# `DELETE` deletes a resource.
response = requests.delete('<url>')

# `OPTIONS` sends a `OPTIONS` request.
response = requests.options('<url>')

# `PATCH` partially updates an existing resource.
responce = requests.patch('<url>', params={<key>: <value>}, <args>)

# Passing parameters in URLs
payload = {'key1': 'value1', 'key2': ['value2', 'value3']}
response = requests.get('httpbin.org/get?key=val', params=payload)
print(r.url) # httpbin.org/get?key1=value1&key2=value2&key2=value3

# Response content
print(response.text)

# Encoding of the response based on the HTTP headers
response.encoding # 'utf-8'
response.encoding = 'ISO-8859-1' # changes the encoding

# JSON response content
response = requests.get('<url>')
response.json() # If decoding fails, it raises an exception.
```

- `JSON` is a data format of which format is similar to a key-value store in a Python dictionary. It’s the _defacto_ interchange format for most REST APIs.

### Status codes

- Status codes are numbered based on the category of the result.

Code  Meaning                 Description
**2xx Successful operation**
200   OK                      The requested action was successful.
201   Created                 A new resource was created.
202   Accepted                The request was received, but no modification has been made yet.
204   No Content              The request was successful, but the response has no content.
**3xx Redirection**
**4xx Client error**
400   Bad Request             The request was malformed.
401   Unauthorized            The client is not authorized to perform the requested action.
404   Not Found               The requested resource was not found.
415   Unsupported Media Type  The request data format is not supported by the server.
422   Unprocessable Entity    The request data was properly formatted but contained invalid or missing data.
**5xx Server error**
500   Internal Server Error   The server threw an error when processing the request.

### Session Objects

- It allows you to
  - persist certain parameters across requests.
  - persist cookies across all the requests made from the Session instance.

- If you are making several requests to the same host, the underlying TCP connection will be reused.

```python
import requests
from requests.exceptions import HTTPError

for url in ['https://api.github.com', 'https://api.github.com/invalid']:
  try:
    response = requests.get(url)
    response.raise_for_status() # it will be raised in case of an error
  except HTTPError as http_err:
    print(f'HTTP error occurred: {http_err}')
  except Exception as err:
    print(f'Other error occurred: {err}')
  else:
    print('Success')
```

---

## Build socket-based network applications with `asyncio` that can handle multi-client simultaneously with one thread

- A socket allows multiple users to connect simultaneously, letting them send and receive messages concurrently.

### 1. Starting a server and listening for a connection

### 2. Reading and writing data to and from a socket

- `recv` gets data from a particular socket.
  - It takes an `int` representing the number of bytes we wish to read at a given time.
  - We can't read all data from a socket at once; we need to buffer until we reach the end of the input.
- We'll treat the end of input as a carriage return plus a line feed or `'\r\n'`. This is what gets appended to the input when a user presses `[Enter]` in `telnet`.

### 3. Build a multi-client echo server using non-blocking sockets and OS' event notification system

- It will work properly for more than one client at a time with only a single thread.
- Steps
  1. We loop forever, calling `socket.accept` to listen for new connections.
  2. Each time we get one, we append it to a list of connections we've got so far.
  3. We loop over each connection, receiving data as it comes in and writing that data back out to the client connection.

- Once the first client connects, we will block waiting for it to send its first echo message to us. This causes other clients to be stuck waiting for the next iteration of the loop, which won't happen until the first client sends us data.
- When we mark a socket as non-blocking, `server_socket.setblocking(False)`, its methods will not block waiting to receive data before moving on to execute the next line of code.
  - If the socket has data ready for processing, then we will get data returned as we would with a blocking socket.
  - If not, the socket will instantly let us know it does not have any data ready, and we are free to move on to execute other code.
- A `BlockingIOError` may be thrown when our server socket has no connection yet and therefore no data to process.

### 4. Use the `selectors` module to build a socket event loop

- We give a list of sockets we want to monitor for events, and instead of constantly checking each socket to see if it has data, the OS tells us explicitly when sockets have data.

- `selectors` allows high-level and efficient I/O multiplexing.
- `BaseSelector` can be used to wait for I/O readiness notifications on multiple file objects.
  - `register` registers the file object to monitor, when we have a socket that we're interested in getting notifications about.
  - `unregister` unregisters a file object from selection, removing it from monitoring.
  - `select` wait until some registered file objects become ready, or the timeout expires.
- `DefaultSelector` is an alias to the most efficient implementation available on the current system.

- Working with `selectors` is a bit too low-level for most applications.

### 5. Add custom shutdown logic

- To implement custom shutdown logic, we'll implement listeners in our application for both the `SIGINT` and `SIGTERM` signals.

#### 5.1. Listening for signals

- To implement custom shutdown logic, we will implement listeners for both:
  - 1. `SIGINT`:= signal interrupt
    - In python, we can catch it by `KeyboardInterrupt`.
  - 2. `SIGTERM` := signal terminate
    - It is triggered when we run `kill` on a process.

- We can directly listen for signals with the `add_signal_handler` method, which can safely interact with the event loop.
- `asyncio.all_tasks()` returns a set of all running tasks.

- When we run this application, we'll see that our delay coroutine starts right away and waits for 10 seconds.
- If we press `CTRL-C` within these 10 seconds, `CancelledError` is thrown:

```python
"""
A signal handler that cancels all currently running tasks.
"""

import asyncio
import signal

from asyncio import AbstractEventLoop
from typing import Set
from util.delay import delay

def cancel_tasks():
  print('Got a SIGINT')
  tasks : Set[asyncio.Task] = asyncio.all_tasks()
  print(f'Cancelling {len(tasks)} task(s).')
  [task.cancel() for task in tasks]

async def main():
  loop : AbstractEventLoop = asyncio.get_running_loop()
  loop.add_signal_handler(signal.SIGINT, cancel_tasks)
  await delay(10)

asyncio.run(main())
```

```python
import selectors
import socket
from selectors import SelectorKey
from typing import List, Tuple

selector = selectors.DefaultSelector()

# create a TCP socket server
# server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM) # socket.AF_INET := type of address, here the hostname and port number # socket.SOCK_STREAM := TCP protocol will be used
server_socket = socket.socket()
server_socket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1) # socket.SO_REUSEADDR, 1 := reuse the port number after stopping and restarting the application
server_socket.setblocking(False)

server_address = ('127.0.0.1', 8000) 
server_socket.bind(server_address) # clients will use 127.0.0.1 to send data to our server
server_socket.listen() # allows clients to connect to our server socket

selector.register(server_socket, selectors.EVENT_READ)

while True:
  events: List[Tuple[SelectorKey, int]] = selector.select(timeout=1) # create a selector that will timeout after 1 sec

  if len(events) == 0:
    print('No events, waiting a bit more!')
  
  for event, _ in events:

    event_socket = event.fileobj # gets the socket for the event, which is stored in the fileobj field

    if event_socket == server_socket: # This is a connection attempt.
      connection, client_address = server_socket.accept() # wait for a connection by blocking until we get a communication # connection:= another socket that we read data from and write data to our client # client_address:= the address of the client that connected
      connection.setblocking(False)
      print(f'I got a connection from {client_address}!')
      selector.register(connection, selectors.EVENT_READ) # register the client that connected with our selector

    else:
      data = event_socket.recv(1024) # receive data from the client, and echo it back
      print(f"I got some data: {data}")
      event_socket.send(data)
```

---

## Concurrency methods

### Multiple processing

- It runs simultaneous things at the same time.
- Each process runs on a different core.
- It is best when we have CPU-intensive work.
- `if __name__ == "__main__"` will be used. Otherwise, `multiprocessing` module will complain.

- `multiprocessing` steps:
  1. It creates a process with `target` function, where `Process()` specifies the target function that the process runs.
  2. It calls its `start` method to execute it.
  3. It calls its `join` method to make other processes wait for it to complete running.

```python
from multiprocess import Process
import os

def hello_from_process():
 print(f"Hello from child process {os.getpid()}")

if __name__ == "__main__":

 # `Process(target=<function>, args=<parameters_of_the_function>`
 hello_process = Process(target=hello_from_process)
 hello_process.start()
 print(f"Hello from process {os.getpid()}")
 hello_process.join() # `join` blocks the main process until each process has finished
```

### Single processing

#### Asynchronous I/O: `asyncio`

- It uses `cooperative multitasking`, and runs one at a time. It cooperates by announcing when they're ready to be switched out.
- It leads to resource utilization improvements for applications that use I/O operations.
  - It handles multiple I/O operations at once.
- It allows us to pause the execution of a particular method when we have an I/O operation; we can run other code while waiting for our initial I/O to complete in the background.
- It may interoperate with `multithreading` and `multiprocessing`.
- In asyncio, the event loop keeps a queue of tasks instead of messages.
- It primarily helps us make I/O-bound work concurrent, but it exposes APIs for making CPU-bound work concurrent as well.

- The steps to write an asyncio program are as follows:

  1. Create an event loop.
  2. Call async/await functions which are coroutines.
  3. Create a task to run on the loop.
  4. Wait for the tasks to be complete.
  5. Close the loop.

#### Multithreading

- Independent code pieces can be put in multiple threads that the CPU can, in theory, run concurrently on multiple cores.
- User-created threads in Python do not receive `KeyboardInterrupt` exceptions; only the main thread will receive them. To handle this:
  1. **_Daemon threads (demon)_ for long-running background tasks** To terminate our app properly, we set `thread.daemon=True` before we run `thread.start()`.
  2. **Cancelling or interrupting a running thread in our way**

```python
import os, threading

def hello_from_thread():
  print(f"Hello from thread {threading.current_thread()}!")

hello_thread = threading.Thread(target=hello_from_thread)
hello_thread.start()

print(f"Python process running with process id: {os.getpid()}")

total_threads = threading.active_count()
thread_name = threading.current_thread().name

print(f"Python is currently running {total_threads} thread(s).")
print(f"The current thread is {thread_name}.")

# join will cause the program to pause until the thread we started is completed.
hello_thread.join()
```

#### `threading`

- It runs one at a time.
- It allows you to have different parts of your program run concurrently.
- It can simplify your design.
- It uses `preemptive multitasking`.
- If the task is I/O bound, you can use it.

**Tip:** When you’re determining the number of threads to use for a particular problem, it is best to start small (the amount of CPU cores plus a few is a good starting point), test it, and benchmark it, gradually increasing the number of threads.

---

## concurrent futures

### `concurrent.futures` module

- Future is thread-safe.
- If I have a small number of tasks, I schedule them all in one go and wait for them all to be complete. Here's a simple example:

```python
import concurrent.futures

## Executor manages all the tasks that are running, either in separate processes or threads.
with concurrent.futures.Executor() as executor:
    futures = {
        executor.submit(perform, task) for task in get_tasks_to_do()
    }

    for future in concurrent.futures.as_completed(futures):
        print(f"The outcome is {future.result()}")
```

### executor

#### Executor Objects

- It provides methods to execute calls asynchronously.

##### 1. ThreadPoolExecutor

- Asynchronous execution can be performed with threads.

##### 2. ProcessPoolExecutor

- Separate processes

---

## Handling CPU-bound work

### Using process pools

- `multiprocessing` module has `process pools`, which is similar to `connection pools`.
  - `process pools` creates a collection of Python processes.
- By default, it will create processes equal to the number of cores, `multiprocessing.cpu_count()`.

### Using `async` and `await` to manage CPU-bound work

- `with Pool() as process_pool:` to avoid resource-utilization issues.

- **Problem:** `process_pool.apply()` blocks until the function completes.
- **Solution:** Use `apply_async` and `get` method to block and obtain the results of the function call.

#### `Executor` (an abstract class of `concurrent.futures` module)

##### Methods for asynchronously running works

1. `submit(<callable>) -> <Future>` is equivalent to `Pool.apply_sync`.
2. `map(<callable>, [<function arguments>]) -> <Iterator_of_results>` executes each argument asynchronously. It returns similarly to `asyncio.as_completed`.

##### `ProcessPoolExecutor` implementation of `PoolExecutor`

- The order of iteration is deterministic based on the order we passed in the list, which differs from `asyncio.as_completed`.

```python
import asyncio
from concurrent.futures import ProcessPoolExecutor
from functools import partial
from typing import List

def count(count_to: int) -> int:
  counter = 0
  while counter < count_to:
    counter += 1
  return counter

async def main():
  with ProcessPoolExecutor as process_pool:
    loop: AbstractEventLoop = asyncio.get_running_loop()
    numbers = [ 1, 3, 5, 22, 100000000]
    calls: List[partial[int]] = [ partial(count, num) for num in nums ]
    call_coros = []

    for call in calls:
      call_coros.append(loop.run_in_executor(process_pool, call))
    results = await asyncio.gather(*call_coros)

    for result in results:
      print(result)

if __name__ == "__main__":
  asyncio.run(main())
```

- `run_in_executor` (asyncio event loop) takes in a callable alongside an executor (either a thread pool or process pool) and runs that callable inside the pool. It returns an awaitable, which can be used in an `await` statement or passed into an API function such as `gather`.

### Solving a problem with MapReduce using `asyncio`

- Implementing a MapReduce workflow with multiprocessing is the in mapreduce folder.

### Handling shared data between multiple processes with locks

- Multiprocessing supports the `shared memory objects` concept.
  - `Shared memory object` is a chunk of memory allocated that a set of the separate process can access. Each process can read and write into that memory space as needed.
- Multiprocessing supports two kinds of shared data:
  - values
  - array
- A `lock`, or `mutual exclusion` (`mutex`), synchronizes the access to shared data.
- `Critical section` is the locked section of a code.
- Locks support two main operations:
  - acquire the lock `get_lock.acquire()`
  - release the lock `get_lock.release()`

#### Sharing data with process pools

- Neither `Value` nor `Array` objects cannot be pickled and unpickled.
- `process pool initializers` are called when each process in our pool starts up. Using this, we can create a reference to the shared memory that our parent process created.

---

## Handling blocking work with threads

### 1. `threading` module

- It creates and manages threads.
- It exposes `Thread` class.
  - `Thread` has a `run` method that we can override.
- `cancel` method definition by subclassing the `Thread` class lets to shut down the client socket. Then, `recv` and `sendall` will be interrupted, allowing to exit `while` loop and close out the thread.
- How to cleanly terminate threads on application shutdown. ([code](multithreaded_echo_server.py))

### 2. Using threads with `asyncio`

- Use threads with asyncio to run web requests concurrently

#### 2.1. `requests`: A popular HTTP client library

- It is blocking so each call to `requests.get` will stop any thread from executing other Python code until the request finishes.
- Using it in a coroutine or a task by itself, will block the entire event loop until the request finishes.
- To properly use this library with asyncio, we must run these blocking operations inside of a thread.

#### 2.2. Thread pool executors

- Use this to distribute work to a pool of threads.
- `Executor` abstract class provides an implementation to work with threads named `ThreadPoolExecutor`.

#### 2.3. Thread pool executors with `asyncio`

- A pool of threads allows us to use asyncio API methods like gather to wait for results from threads.

#### 2.4. Default executors

- `asyncio.to_thread` coroutine was introduced to further simplify putting work on the default thread pool executor. It takes in a function to run in a thread and a set of arguments to pass to that function. ([code](to_thread.py))

### 3. Locks, shared data, and deadlocks

- Any time you have two threads or processes that could modify a shared piece of non-thread-safe data, you’ll need to utilize a lock to properly synchronize access.
- Avoid race conditions with locks from the `threading` module, `Lock` implementation.
  - Call its `acquire` and `release` methods around critical sections of code or use it in `context manager`.
- `from threading import Lock`
- `list_lock = Lock()`

#### 3.1. Reentrant locks

- Avoid deadlocks with reentrant locks
- A reentrant lock is a special kind of lock that can be acquired by the same thread more than once, allowing the thread to reenter the critical sections
- `from threading import Rlock`
- `list_lock = RLock()`
- Internally, reentrant locks work by keeping a recursion count. Each time we acquire the lock from the thread that first acquired the lock, the count increases, and each time we release the lock it decreases. When the count is 0, the lock is finally released for other threads to acquire it.

#### 3.2. Deadlocks

- It is impossible to have a deadlock with one lock, excluding the reentrant deadlock.
- Overall, when dealing with multiple locks that you need to acquire, ask yourself:
  - Am I acquiring these locks in a consistent order?
  - Is there a way I can refactor this to use only one lock?

### 4. Event loops in separate threads

- Run the asyncio event loop in a separate thread and send coroutines to it in a thread-safe manner
- Use multithreading to run multiple event loops at the same time by building a responsive HTTP stress-testing user interface in Tkinter.

#### 4.1. `Tkinter`

- A platform-independent desktop GUI toolkit provided in the default Python installation.
- Responsive user interfaces with frameworks
- `Tkinter` is not asyncio-aware.

#### 4.2. Building a responsive UI with `asyncio` and threads

- There are a few `asyncio` functions to learn that both are non-blocking and have thread safety built in to submit this kind of work properly.
  1. An asyncio event loop `call_soon_threadsafe` function takes in a Python function (not a coroutine) and schedules it to execute it in a thread-safe manner at the next iteration of the asyncio event loop.
  2. `asyncio.run_coroutine_threadsafe`

@todo 180-184 skipped

### 5. Using threads for CPU-bound work

- `hashlib` and `numpy` perform CPU-intensive work in pure C and release GIL.

#### 5.1. Multithreading with `hashlib`

- Hashing sensitive text for security ([code](multithread_hashing.py))

#### 5.2. Multithreading with `numpy`

- Solving a data analysis problem ([code](multithread_numpy.py))
- It is generally safe to assume matrix operations can potentially be multithreaded for a performance win.

---

## Multithread hashing

```python
import asyncio
import functools
import hashlib
import os
import random
import string
from concurrent.futures.thread import ThreadPoolExecutor

def random_password(length: int) -> bytes:
  ascii_lowercase = string.ascii_lowercase.encode()
  return b''.join(bytes(random.choice(ascii_lowercase)) for _ in range(length))

passwords = [ random_password(10) for _ in range(10000) ]

def hash(password: bytes) -> str:
  salt = os.urandom(16)
  return str(hashlib.scrypt(password, salt=salt, n=2048, p=1, r=8))


async def main():
  loop = asyncio.get_running_loop()
  tasks = []
  with ThreadPoolExecutor() as pool:
    for password in passwords:
      tasks.append(loop.run_in_executor(pool, functools.partial(hash, password)))
  await asyncio.gather(*tasks)

asyncio.run(main())
```

---

## Multithread numpy

```python
import asyncio
import functools
import numpy as np
from concurrent.futures.thread import ThreadPoolExecutor

data_points = 4000000000
rows = 50
columns = int(data_points / rows)
matrix = np.arange(data_points).reshape(rows, columns)

def mean_for_row(arr, row):
  return np.mean(arr[row])


async def main():
  loop = asyncio.get_running_loop()
  with ThreadPoolExecutor() as pool:
    tasks = []
    for i in range(rows):
      mean = functools.partial(mean_for_row, matrix, i)
      tasks.append(loop.run_in_executor(pool, mean))
    results = asyncio.gather(*tasks)

asyncio.run(main())
```

---

## Multithread echo server

```python
from threading import Thread
import socket


class ClientEchoThread(Thread): # inherits from `Thread` class

 def __init__(self, client):
  super().__init__()
  self.client = client

 def run(self):
  try:
   while True:
    data = self.client.recv(2048)
    if not data: # when the connection was shut down or closed by the client
     raise BrokenPipeError('Connection closed!')
    print(f'Received {data}, sending!')
    self.client.sendall(data)
  except OSError as e:
   print(f'Thread interrupted by {e} exception, shutting down!')

 def close(self):
  if self.is_alive(): # shut down the connection if the thread is alive; the thread may not be alive if the client closed the connection
   self.client.sendall(bytes('Shutting down!', encoding='utf-8'))
   self.client.shutdown(socket.SHUT_RDWR) # shut down the client connection for reads and writes


with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as server:

 server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
 server.bind(('127.0.0.1', 8000))
 server.listen()

 connection_threads = []
 try:
  while True: # listen for connections on our server socket
   connection, _ = server.accept() # block waiting for a client to connect
   thread = ClientEchoThread(connection)
   connection_threads.append(thread) 
   thread.start()
 except KeyboardInterrupt:
  print('Shutting down!')
  [ thread.close() for thread in connection_threads ]
```

---

## Non-blocking database drivers

- We need to use an asyncio-friendly library that uses non-blocking sockets since typical SQL libraries block the main thread (therefore the event loop) until a result is retrieved.

### Running asyncio-friendly database queries with `asyncpg`

- `asyncpg` asynchronously connects Postgres and runs queries against them. (`aiomysl` := MySQL)
- To run queries against our database, we first connect to our Postgres instance and create the database directly outside of Python.
- `execute` inserts data, and `fetch` runs a query.
- `fetch` gets all results, whereas `fetchrow` returns a single query.

#### Connecting to a Postgres database, creating a database, and running queries

```python
import asyncpg
import asyncio

from asyncpg import Record
from typing import List

CREATE_BRAND_TABLE = \
  """
  CREATE TABLE IF NOT EXISTS brand(
    brand_id SERIAL PRIMARY KEY,
    brand_name TEXT NOT NULL
  );"""

CREATE_PRODUCT_TABLE = \
  """
  CREATE TABLE IF NOT EXISTS product(
    product_id SERIAL PRIMARY KEY,
    product_name TEXT NOT NULL,
    brand_id INT NOT NULL,
    FOREIGN KEY (brand_id) REFERENCES brand(brand_id)
  );"""

CREATE_PRODUCT_COLOR_TABLE = \
  """
  CREATE TABLE IF NOT EXISTS product_color(
    product_color_id SERIAL PRIMARY KEY,
    product_color_name TEXT NOT NULL
  );"""

CREATE_PRODUCT_SIZE_TABLE = \
  """
  CREATE TABLE IF NOT EXISTS product_size(
    product_size_id SERIAL PRIMARY KEY,
    product_size_name TEXT NOT NULL
  );"""

CREATE_SKU_TABLE = \
  """
  CREATE TABLE IF NOT EXISTS sku(
    sku_id SERIAL PRIMARY KEY,
    product_id INT NOT NULL,
    product_size_id INT NOT NULL,
    product_color_id INT NOT NULL,
    FOREIGN KEY (product_id) REFERENCES product(product_id),
    FOREIGN KEY (product_size_id) REFERENCES product_size(product_size_id),
    FOREIGN KEY (product_color_id) REFERENCES product_color(product_color_id)
  );"""

COLOR_INSERT = \
  """
  INSERT INTO product_color VALUES(1, 'Blue');
  INSERT INTO product_color VALUES(2, 'Black');
  """
SIZE_INSERT = \
  """
  INSERT INTO product_size VALUES(1, 'Small');
  INSERT INTO product_size VALUES(2, 'Medium');
  INSERT INTO product_size VALUES(3, 'Large');
  """

async def main():
  connection = await asyncpg.connect( host='127.0.0.1',
                                      port=5432,
                                      user='postgres',
                                      database='products',
                                      password='password' )

  statements = [  CREATE_BRAND_TABLE,
                  CREATE_PRODUCT_TABLE,
                  CREATE_PRODUCT_COLOR_TABLE,
                  CREATE_PRODUCT_SIZE_TABLE,
                  CREATE_SKU_TABLE,
                  SIZE_INSERT,
                  COLOR_INSERT ]

  print('Creating the product database...')
  for statement in statements:
    status = await connection.execute(statement)
    print(status)
  print('Finished creating the product database!')

  await connection.execute("INSERT INTO brand VALUES(DEFAULT, 'Levis')")
  await connection.execute("INSERT INTO brand VALUES(DEFAULT, 'Seven')")

  results : List[Record] = await connection.fetch('SELECT brand_id, brand_name FROM brand')
  for brand in results:
    print(f'id: {brand["brand_id"]}, name: {brand["brand_name"]}')

  await connection.close()

asyncio.run(main())
```

### Executing queries concurrently with connection pools

- `executemany` coroutine writes an SQL query and passes in a list of parameters we want to insert instead of having to create one `INSERT` statement for each brand.

```python
import asyncio
import asyncpg

from typing import Tuple, Union, List
from random import sample

def load_common_words() -> List[str]:
  with open('/Users/macos/Desktop/python/concurrency/common_words.txt') as common_words:
    return common_words.readlines()

def generate_brand_names(words: List[str]) -> List[Tuple[Union[str, ]]]:
  return [(words[index],) for index in sample(range(100), 100)]

async def insert_brands(common_words, connection) -> int:
  brands = generate_brand_names(common_words)
  insert_brands = "INSERT INTO brand VALUES(DEFAULT, $1)"
  return await connection.executemany(insert_brands, brands)

async def main() -> None:
  common_words = load_common_words()
  connection = await asyncpg.connect( host='127.0.0.1',
                                      port=5432,
                                      user='postgres',
                                      database='products',
                                      password='password' )
  await insert_brands(common_words, connection)

asyncio.run(main())
```

```python
import asyncio
import asyncpg

from typing import List, Tuple
from random import sample, randint

def load_common_words() -> List[str]:
  with open('/Users/macos/Desktop/python/concurrency/common_words.txt') as file:
    return file.readlines()

def gen_products( common_words: List[str],
                  brand_id_start: int,
                  brand_id_end: int,
                  products_to_create: int ) -> List[ Tuple[str, int] ]:
  products = []
  for _ in range(products_to_create):
    description = [ common_words[index] for index in sample(range(1000), 10) ]
    brand_id = randint(brand_id_start, brand_id_end)
    products.append((" ".join(description), brand_id))
  return products

def gen_skus( product_id_start: int,
              product_id_end: int,
              skus_to_create: int ) -> List[Tuple[int, int, int]]:
  skus = []
  for _ in range(skus_to_create):
    product_id = randint(product_id_start, product_id_end)
    size_id = randint(1,3)
    color_id = randint(1,2)
    skus.append((product_id, size_id, color_id))
  return skus

async def main() -> None:
  common_words = load_common_words()
  connection = await asyncpg.connect( host='127.0.0.1',
                                      port=5432,
                                      user='postgres',
                                      database='products',
                                      password='password' )
  product_tuples = gen_products( common_words,
                                  brand_id_start=1,
                                  brand_id_end=100,
                                  products_to_create=1000 )
  await connection.executemany("INSERT INTO product VALUES(DEFAULT, $1, $2)", product_tuples)
  sku_tuples = gen_skus( product_id_start=1,
                         product_id_end=1000,
                         skus_to_create=100000 )
  await connection.executemany("INSERT INTO sku VALUES(DEFAULT, $1, $2, $3)", sku_tuples)
  await connection.close()
asyncio.run(main())
```

#### Creating database connection pools running multiple SQL queries concurrently

- A connection pool contains a finite number of connections that we can access when we need to run a query.
- Once a connection is acquired from the pool (`acquire`) to run a query and that query finishes, we return or release it to the pool for others to use.
- `asyncpg` creates a connection pool using `create_pool` coroutine, which we use instead of `connect`.
  - Parameters for a number of connections are `min_size` and `max_size`.
- async pools use `async with` syntax, asynchronous context manager.
- `async with connection.transaction()` starts a transaction.
  - If there is an exception, the transaction will be rolled back.

```python
import asyncio
import asyncpg

product_query = \
"""
SELECT p.product_id, p.product_name, p.brand_id, s.sku_id, pc.product_color_name, ps.product_size_name
FROM product as p
JOIN sku as s on s.product_id = p.product_id
JOIN product_color as pc on pc.product_color_id = s.product_color_id
JOIN product_size as ps on ps.product_size_id = s.product_size_id
WHERE p.product_id = 100
"""

async def query_product(pool):
  async with pool.acquire() as connection:
    return await connection.fetchrow(product_query)

async def main() -> None:
  async with asyncpg.create_pool( host='127.0.0.1',
                                  port=5432,
                                  user='postgres',
                                  password='password',
                                  database='products',
                                  min_size=6,
                                  max_size=6 ) as pool:
  
    # execute two product queries concurrently
    await asyncio.gather(query_product(pool), query_product(pool))

asyncio.run(main())
```

### Managing asynchronous database transactions and handling an error in a transaction

```python
import asyncio
import asyncpg
import logging

async def main():
  connection = await asyncpg.connect( host='127.0.0.1',
                                      database='products',
                                      username='postgres',
                                      password='password',
                                      port=5432 )
  try:
    async with connection.transaction():
      insert_brand = "INSERT INTO brand VALUES(9999, 'big_brand')"
      await connection.execute(insert_brand)
      await connection.execute(insert_brand) # an exception will be raise due to duplicate primary key
  except Exception:
    logging.exception('Error while running transaction')
  finally:
    query = "SELECT brand_name FROM brand WHERE brand_name LIKE 'big_%'"
    brands = await connection.fetch(query)
    print(brands) # [] := transaction is rolled back.

  await connection.close()

asyncio.run(main())
```

```python
import asyncio
import asyncpg

from asyncpg.transaction import Transaction

async def main():
  connection = await asyncpg.connect( host='127.0.0.1',
                                      database='products',
                                      username='postgres',
                                      password='password',
                                      port=5432 )
  transaction : Transaction = connection.transaction() # creates a transaction instance
  await transaction.start() # start the transaction
  try:
    await connection.execute("INSERT INTO brand VALUES(DEFAULT, 'brand_1')")
    await connection.execute("INSERT INTO brand VALUES(DEFAULT, 'brand_2')")
  except asyncpg.PostgresError:
    print('Errors, rolling back transaction!')
    await transaction.rollback()
  else:
    print('No errors, committing transaction!')
    await transaction.commit()

  query = "SELECT brand_name FROM brand WHERE brand_name LIKE 'big_%'"
  brands = await connection.fetch(query)
  print(brands) # [] := transaction is rolled back.

  await connection.close()

asyncio.run(main())
```

### Using asynchronous generators to stream query results

- Postgres supports streaming query results through the concept of cursors.
  - Cursors use `asynchronous generators`.
- `async for` fetches elements one at a time from our result set.
- Cursors can go forward only. To go backwards, we execute SQL to do so using `DECLARE ... SCROLL CURSOR`.

```python
import asyncio
import asyncpg

async def main():
  connection = await asyncpg.connect( host='127.0.0.1',
                                      database='products',
                                      username='postgres',
                                      password='password',
                                      port=5432 )
  async with connection.transaction():
    query = 'SELECT product_id, product_name FROM product'
    ## async for ##
    # async for product in connection.cursor(query):
    #   print(product)
    ###############
    cursor = await connection.cursor(query) # creates a cursor for the query
    await cursor.forward(500) # move the cursor forward 500 records
    products = await cursor.fetch(100) # get the next 100 records
    for product in products:
      print(product)

  await connection.close()

asyncio.run(main())
```

```python
import asyncio
import asyncpg

async def take(generator, to_take: int):
  item_count = 0
  async for item in generator:
    if item_count > to_take - 1:
      return
    item_count += 1
    yield item

async def main():
  connection = await asyncpg.connect( host='127.0.0.1',
                                      database='products',
                                      username='postgres',
                                      password='password',
                                      port=5432 )
  async with connection.transaction():
    query = 'SELECT product_id, product_name FROM product'
    product_generator = await connection.cursor(query)
    async for product in take(product_generator, 5):
      print(product)
    print('Got the first 5 products')
  
  await connection.close()

asyncio.run(main())
```

[asyncpg documentation](https://magicstack.github.io/asyncpg/current/)

---

## Protocol

```python
import asyncio
from asyncio import AbstractEventLoop, Future, Transport
from typing import Optional

class HTTPGetClientProtocol(asyncio.Protocol): # extends asyncio.Protocol class

 def __init__(self, host: str, loop: AbstractEventLoop):
  self._host: str = host
  self._future: Future = loop.create_future()
  self._transport: Optional[Transport] = None # transport communicates with the server
  self._response_buffer: bytes = b''

 async def get_response(self):
  return await self._future

 def _get_request_bytes(self) -> bytes:
  request = f"GET / HTTP/1.1\r\n" \
        f"Connection: close\r\n" \
            f"Host: {self._host}\r\n\r\n"
  return request.encode()

 def connection_made(self, transport: Transport):
  """ `Transport` calls it when the underlying socket has successfully
  connected with the HTTP server.
  """
  print(f'Connection made to {self._host}')
  self._transport = transport
  self._transport.write(self._get_request_bytes())

 def data_received(self, data):
  """ `Transport` calls it whenever it receives data,
  passing it to us as bytes.
  """
  print('Data received!')
  self._response_buffer += data # _response_buffer can be called multiple times

 def eof_received(self):
  """Calling this method guarantees that data_received
  will never be called again.
  """
  self._future.set_result(self._response_buffer.decode())
  return False

 def connection_lost(self, exc: Optional[Exception]) -> None:
  if exc is None:
   print('Connection closed without error.')
  else:
   self._future.set_exception(exc)

async def make_request(host: str, port: int, loop: AbstractEventLoop) -> str:
 def protocol_factory():
  return HTTPGetClientProtocol(host, loop)

 _, protocol = await loop.create_connection(protocol_factory, host=host, port=port)
 return await protocol.get_response()

async def main():
 loop = asyncio.get_running_loop()
 result = await make_request('www.example.com', 80, loop)
 print(result)

asyncio.run(main())
```

---

## server

```python
import asyncio
import logging

from asyncio import StreamWriter, StreamReader

class ServerState:

  def __init__(self):
    self._writers = []
  
  async def add_client(self, reader: StreamReader, writer: StreamWriter):
    """send messages to all connected clients and
    remove it when a client disconnects
    """
    self._writers.append(writer)
    await self._on_connect(writer)
    asyncio.create_task(self._echo(reader, writer))

  async def _on_connect(self, writer: StreamWriter):
    """sends a message to the client informing them how many other
    users are connected and notify any other connected clients that
    the new user has connected
    """
    writer.write(f'Welcome! {len(self._writers)} user(s) are online!\n'.encode())
    await writer.drain()
    await self._notify_all('New user connected!\n')
  
  async def _echo(self, reader: StreamReader, writer: StreamWriter):
    """When a user disconnects, we notify any other connected clients
    that someone disconnected
    """
    try:
      while (data := await reader.readline()) != b'':
        writer.write(data)
        await writer.drain()
      self._writers.remove(writer)
      await self._notify_all((f'Client disconnected. {len(self._writers)} user(s) are online!\n'))
    except Exception as e:
      logging.exception('Error reading from client.', exc_info=e)
      self._writers.remove(writer)

  async def _notify_all(self, message: str):
    for writer in self._writers:
      try:
        writer.write(message.encode())
        await writer.drain()
      except ConnectionError as e:
        logging.exception('Could not write to client.', exc_info=e)
        self._writers.remove(writer)

async def main():
  server_state = ServerState()
  
  async def client_connected(reader: StreamReader, writer: StreamWriter) -> None:
    await server_state.add_client(reader, writer)

  # start server and start serving forever
  server = await asyncio.start_server(client_connected, '127.0.0.1', 8000)

  async with server:
    await server.serve_forever()

asyncio.run(main())
```

---

## Stream reader

```python
import asyncio
from asyncio import StreamReader
from typing import AsyncGenerator

async def read_until_empty(stream_reader: StreamReader) -> AsyncGenerator[str, None]:
 while response := await stream_reader.readline():
  yield response.decode()

async def main():
 host: str = 'www.example.com'
 request: str = f"GET / HTTP/1.1\r\n" \
       f"Connection: close\r\n" \
       f"Host: {host}\r\n\r\n"

 stream_reader, stream_writer = await asyncio.open_connection(host, 80)

 try:
  stream_writer.write(request.encode())
  await stream_writer.drain()
  responses = [ response async for response in read_until_empty(stream_reader) ]
  print(''.join(responses))

 finally:
  stream_writer.close()
  await stream_writer.wait_closed()

asyncio.run(main())
```

---

## Streams

- Streams are a high-level set of classes and functions that create and manage network connections and generic streams of data.

### Stream readers and stream writers

- We develop networking applications in `asycnio` using `stream`. [code](stream_reader.py)
- `open_connection` will create
  - `StreamWriter` to send out the HTTP request
    - `StreamWriter`'s `write` method is a plain method.
  - `StreamReader` to read the response.
- `drain` coroutine blocks until all queued data gets sent to the socket, ensuring we've written everything before moving on.
  - `write` -> `await` -> `drain`

### Using streams for network connections

- `connect_read_pipe(<protocol_factory>, <pipe>)` connects a protocol to a file-like object.
  - A _protocol factory_ is a function that creates a protocol instance.
  - A _pipe_ is a file-like object, which is defined as an object with methods such as `read` and `write` on it.
- `StreamReaderProtocol` connects instances of stream readers to protocols.
  - Using this, a command-line application will not be blocked by the event loop when waiting for the user input.

### Processing command-line input asynchronously

- [code](cli_sql.py)

### Creating servers

- [code](server.py)
- `asyncio.start_server(<host>, <port>, <client_connected_cb>)` creates servers without managing sockets.
  - `<host>` and `<port>` are the addresses that the server socket will listen for connections.
  - `<client_connected_cb>` is either a callback function or a coroutine that will run whenever a client connects to the server.
    - This callback takes in a `StreamReader` and `StreamWriter` as parameters that will let us read from and write to the client that is connected to the server.

- When we await `start_server`, it will return an `AbstractServer` object.

---

## Subroutine

- A bit of code that can be called by another code.

---

## Mapreduce process pools

```python
import asyncio
import concurrent.futures
import functools
import time
from typing import Dict, List


def partition(data: List, chunk_size: int) -> List:
 for i in range(0, len(data), chunk_size):
  yield data[i:i+chunk_size]

def map_frequencies(chunk: List[str]) -> Dict[str, int]:
 counter = {}
 for line in chunk:
  word, _, count, _ = line.split('\t')
  if counter.get(word):
   counter[word] += int(count)
  else:
   counter[word] = int(count)
 return counter

def merge_dictionaries(first: Dict[str, int], second: Dict[str, int]) -> Dict[str, int]:
 merged = first
 for key in second:
  if key in merged:
   merged[key] += second[key]
  else:
   merged[key] = second[key]
 return merged

async def reduce(loop, pool, counters, chunk_size) -> Dict[str, int]:
 chunks: List[List[Dict]] = list(partition(counters, chunk_size))
 reducers = []
 while len(chunks[0]) > 1:
  for chunk in chunks:
   reducer = functools.partial(functools.reduce, merge_dictionaries, chunk)
   reducers.append(loop.run_in_executor(pool, reducer))
  reducer_chunks = await asyncio.gather(*reducers)
  chunks = list(partition(reducer_chunks, chunk_size))
  reducers.clear()
 return chunks[0][0]


async def main(partition_size: int):
 with open('googlebooks-fre-all-1gram-20120701-a', encoding='utf-8') as file:
  contents = file.readlines()
  loop = asyncio.get_running_loop()
  tasks = []
  with concurrent.futures.ProcessPoolExecutor() as pool:
   for chunk in partition(contents, partition_size):
    tasks.append(loop.run_in_executor(pool, functools.partial(map_frequencies, chunk)))
   intermediate_results = await asyncio.gather(*tasks)
   final_result = await reduce(loop, pool, intermediate_results, 500)
   print(f"Aardvark has appeared {final_result['Aardvark']} times.")


if __name__ == "__main__":
 asyncio.run(main(partition_size=60000))
```

---

## Lock

### Process lock

```python
import asyncio
from concurrent.futures import ProcessPoolExecutor
from multiprocessing import Value

shared_counter: Value

def init(counter: Value):
  global shared_counter
  shared_counter = counter

def increment():
  with shared_counter.get_lock():
    shared_counter.value += 1

async def main():
  counter = Value('d', 0)
  with ProcessPoolExecutor(initializer=init, initargs=(counter,)) as pool:
    await asyncio.get_running_loop().run_in_executor(pool, increment)
    print(counter.value)

if __name__ == "__main__":
  asyncio.run(main())
```

### Thread lock

```python
import asyncio
import requests
from concurrent.futures import ThreadPoolExecutor
from functools import partial
from threading import Lock

counter_lock = Lock()
counter: int = 0

def get_status_code(url: str) -> int:
  global counter
  response = requests.get(url)
  with counter_lock:
    counter += 1
  return response.status_code

async def reporter(request_count: int):
  while counter < request_count:
    print(f'Finished {counter}/{request_count} requests')
    await asyncio.sleep(.5)


async def main():
  loop = asyncio.get_running_loop()
  with ThreadPoolExecutor() as pool:
    request_count = 200
    urls = ['https://www.example.com' for _ in range(request_count)]
    reporter_task = asyncio.create_task(reporter(request_count))
    tasks = [loop.run_in_executor(pool, partial(get_status_code, url)) for url in urls]
    results = await asyncio.gather(*tasks)
    await reporter_task
    print(results)

asyncio.run(main())
```

---

## Thread

- A thread is alive if its `run` method is executing.
- OS knows about each thread, and it can interrupt a thread at any time to start running a different thread.
- It is created at the OS level and more expensive to create than coroutines.
- It has a context-switching cost at the OS level. Saving and restoring thread state when a context switch happens eats up some of the performance gains obtained by using threads.
- Each thread has an `Event Loop` object.

### to thread

```python
import asyncio
import requests

def get_status_code(url: str) -> int:
 response = requests.get(url)
 return response.status_code


async def main():
 urls = ['https://www.example.com' for _ in range(1000)]
 tasks = [asyncio.to_thread(get_status_code, url) for url in urls]
 results = await asyncio.gather(*tasks)
 print(results)

asyncio.run(main())
```

---

## Synchronization

### asyncio lock

```python
import asyncio
import sys
from asyncio import Lock
from util.delay import delay

async def a(lock: Lock):
  print('Coroutine a waiting to acquire the lock')
  async with lock:
    print('Coroutine a is in the critical section')
    await delay(5)
  print('Coroutine a released the lock')

async def b(lock: Lock):
  print('Coroutine b waiting to acquire the lock')
  async with lock:
    print('Coroutine b is in the critical section')
    await delay(2)
  print('Coroutine b released the lock')


async def main():
  sys.path.append('../util')
  lock = Lock()
  await asyncio.gather(a(lock), b(lock))

asyncio.run(main())
```

- When we write applications using multiple threads and multiple processes, we need to worry about race conditions when using non-atomic operations.
- Most objects in `asyncio` provide an optional loop parameter that lets you specify the specific `event loop` to run in. When this parameter is not provided, `asyncio` tries to get the currently running `event loop`, but if there is none, it creates a new one. (Parameters will be removed with version 3.10.)

### Single-threaded concurrency issues

- In asyncio's single-threaded model, we only have one thread executing one line of Python code at any given time. This means that even if an operation is non-atomic, we'll always run it to completion without other coroutines reading inconsistent state information.

- Single-threaded concurrency bugs differ from concurrency bugs in multithreading and multiprocessing.

### Uses of synchronization primitives

- Preventing concurrency bugs
- While working with an API
  - that makes only a few requests concurrently as per a contract we have with a vendor.
  - where we're concerned about overloading.
- A workflow with several workers that need to be notified when new data is available.

### Solving race conditions _with_ locks and other concurrency primitives

#### Using locks to protect critical sections

- `Lock` is an `asyncio` synchronization primitive
- Locks to prevent concurrency bugs and synchronize `coroutine`s
  - They can sometimes be needed when the shared state could change during `await`.
- `asyncio` locks are awaitable objects that suspend `coroutine` execution when they are blocked.
- `async with` is recommended use because `asyncio` locks are context managers. [code](asyncio_lock.py)

### Limiting concurrency and controlling access to a shared source _with_ semaphores

- How to use semaphores to control access to finite resources and limit concurrency, which can be useful in traffic-shaping

### Notifying tasks when something occurs and acquiring the shared sources when it happens _with_ events and conditions

- How to use events to trigger actions when something happens, such as initialization or waking up worker tasks
- How to use conditions to wait for an action and, because of an action, gain access to a shared resource

### Queues

---

## utils

### async timed

```python
import functools
import time
from typing import Callable, Any

def async_timed():

  def wrapper(func: Callable) -> Callable:

    @functools.wraps(func)
    async def wrapped(*args, **kwargs) -> Any:
      print(f'starting {func} with args {args} {kwargs}')
      start = time.time()

      try:
        return await func(*args, **kwargs)
      finally:
        end = time.time()
        total = end - start
        print(f'finished {func} in {total:.4f} second(s)')

    return wrapped

  return wrapper
```

### create stdin reader

```python
import asyncio
import sys
from asyncio import StreamReader

async def create_stdin_reader() -> StreamReader:
  stream_reader = asyncio.StreamReader()
  protocol = asyncio.StreamReaderProtocol(stream_reader)
  loop = asyncio.get_running_loop()
  await loop.connect_read_pipe(lambda: protocol, sys.stdin)
  return stream_reader
```

### cursor

```python
import shutil
import sys
from asyncio import StreamReader
from collections import deque

def save_cursor_position():
 sys.stdout.write('\0337')

def restore_cursor_position():
 sys.stdout.write('\0338')

def move_to_bottom_of_screen() -> int:
 _, total_rows = shutil.get_terminal_size()
 input_row = total_rows - 1
 sys.stdout.write(f'\033[{input_row}E')
 return total_rows

def move_to_top_of_screen():
 sys.stdout.write('\033[H')

def move_back_one_char():
 sys.stdout.write('\033[1D')

def delete_line():
 sys.stdout.write('\033[2K')

def clear_line():
 sys.stdout.write('\033[2K\033[0G')

async def read_line(stdin_reader: StreamReader) -> str:

 def erase_last_char():
  move_back_one_char()
  sys.stdout.write(' ')
  move_back_one_char()

 delete_char = b'\x7f'
 input_buffer = deque()
 while ( input_char := await stdin_reader.read(1)) != b'\n':
  if input_char == delete_char:
   if len(input_buffer) != 0:
    input_buffer.pop()
    erase_last_char()
    sys.stdout.flush()
  else:
   input_buffer.append(input_char)
   sys.stdout.write(input_char.decode())
   sys.stdout.flush()
 clear_line()
 return b''.join(input_buffer).decode()
```

### delay

```python
"""
It will help us see what other code, if any,
is running concurrently while our coroutines
are paused.
"""
import asyncio

async def delay(delay_seconds: int) -> int:
 print(f'sleeping for {delay_seconds} second(s)')
 await asyncio.sleep(delay_seconds)
 print(f'finished sleeping for {delay_seconds} second(s)')
 return delay_seconds
```

### fetch status

```python
import asyncio
from aiohttp import ClientSession, ClientTimeout

async def fetch_status(session: ClientSession, url: str) -> int:

  ten_millis = ClientTimeout(total=.01)

  async with session.get(url, timeout=ten_millis) as result: # we can process the result within this block
    return result.status
```

### message store

```python
from collections import deque
from typing import Awaitable, Callable, Deque

class MessageStore:
  def __init__(self, callback: Callable[[Deque], Awaitable[None]], max_size: int):
    self._deque = deque(maxlen=max_size)
    self._callback = callback

  async def append(self, item):
    self._deque.append(item)
    await self._callback(self._deque)
```
