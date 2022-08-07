# Server logic

request -> server -> response

Processes:
1.  **pipe** validate data contained in the request
2.  **guard** make sure the user is authenticated (optional)
3.  **controller** route the request to a particular function
4.  **service** run some business logic
5.  **repository** access a database

**Parts of Nest**

1.  **Controllers**: handles incoming requests
2.  **Services**: handles data access and business logic
3.  **Modules**: Groups together code
4.  **Pipes**: Validates incoming data
5.  **Filters**: Handles error that occur during request handling
6.  **Guards**: Handles authentication
7.  **Interceptors**: Adds extra logic to incoming requests or outgoing responses
8.  **Repositories**: Handles data stored in a DB


## Creating module
`nest generate module "module-name"`

## Creating controller
`nest generate controller foldername/filename --flat`
flat here means don't create extra contrllers folder

# DEPENDENCY INJECTION

## Why dependency injection exists??

### Inversion of Control Principle
-> *Classes should not create instances of its dependencies on its own.*

❌BAD
```
import { MessagesRepository } from './messages.repository'

export class MessagesService {
  messagesRepo: MessagesRepository;

  constructor() {
    this.messagesRepo = new MessagesRepository();
  }
}
```

✅BETTER
```
import { MessagesRepository } from './messages.repository'

export class MessagesService {
  messagesRepo: MessagesRepository;

  constructor(repo: MessagesRepository) {
    this.messagesRepo = repo;
  }
}
```

✅GOOD
```
import { MessagesRepository } from './messages.repository'

interface Repository {
	findOne(id: string);
	findAll();
	create(content: string);
}

export class MessagesService {
  messagesRepo: Repository;

  constructor(repo: Repository) {
    this.messagesRepo = repo;
  }
}
```	

This is good because we can pass anything in repository! But still there a drawback:
To write a controller logic, we have to have services implemented, and to have services running, we have to have repository implemented. And, this gets messed up if a controller depends upon many services and services depends upon many repositories. And, if controller depends upon many services, we cannot imagine what we have.

To solve this problem and still able to use inversion of control, dependecy injection is introduced.

![de11f6e3c3277b2448942492a8164b2c.png](:/886f9a0bb4e541c5808e39d1125c314f)


Providers = things that can be used as dependencies for other classes

* * *

# Project: My Car Value 

![bbf7030ea940200ff730139ef75aacf1.png](:/b2d9bcf361224d6db4ed04a6b826c0d6)

![e25f96d4e0402b6965877650d40c53fc.png](:/18379e900335459f85bb29fc718a28e4)

# Authentication Vs Authorization

**Authentication**: Figure out who is making a request.

**Authorization**: Figure out if the person making the request is allowed to make it.

# Nest Request Handling steps

![87b80505f68eb4eff314045f1555305f.png](:/be392015a189481d862b2c7ef94f3b05)

