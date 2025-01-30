## Introduction
The following design will be for an app similar to the late Plug.dj website: "Sax.dj". Plug.dj was a platform where users could make chatroom-like instances and queue up songs to alternate as the dj for that room, and share music with a group. 

## Description of functionality
Sax.dj will function similar to chatrooms. A registered user will be able to create rooms. In these rooms there is a chat, a video/dj queue, and an option to add a video to the queue yourself. The user should also be able to see existing rooms and join them. A user should be able to send chat messages, add/remove their own songs to the queue and close and delete the instance if they are the creator.

There will be a second role of moderator. These users can close any room, regardless if they're the creator or not. 


## C4 Level 2

```plantuml
@startuml C4_Elements
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Container.puml
LAYOUT_WITH_LEGEND()

Person(newuser, "New user", "Sees only the log-in screen")
Person(user, "Registered User", "Logged-in users can create and join instances and play music.")
Person(moderator, "Moderator", "User with extra permissions to moderate instances")

System_Boundary(plugdj, "Plug.dj Remake") {
    Container(frontend, "Frontend Web Application", "User interface for interacting with the website.")
    Container(backend, "Backend API", "Communicates with database and external APIs")
    ContainerDb(db, "Database", "Stores user data, instance data, and chat history.")
}


System_Ext(videoapi, "Youtube API service", "Provides music/video content for instances")

BiRel(newuser, frontend, "Sign up / Log-in")
Rel(newuser, user, "After log-in or sign up succeeds")
Rel(user, frontend, "Chat, Vote, Create Playlists")
Rel(moderator, frontend, "Moderate Content/Users")

Rel(frontend, backend, "API Requests (Auth, User management, Instance management, database entries)")
Rel(backend, db, "Store/Retrieve Data")
Rel(backend, videoapi, "Fetch Media Content")
@enduml
```

## Design choices / alternatives

My experience is:
- Frontend Web:
    - Vanilla JS
    - Svelte (long ago (> 2 years ))
    - Flask (long ago (> 1 year))
    - Ruby on rails (somewhat recent (< 1 year))
    - Angular (long ago (> 1 year))
- Backend API:
    - Rest
- Database:
    - Supabase (used recently)
    - Sqlite3 in Javascript for queries
    - Sqlite3 in python for queries
- Hosting:
    - AWS: running files in an instance in a VPC

#### Frontend

| Alternative   | Criteria      | Rating | Motivation                                                                                                               |
| ------------- | ------------- | ------ | ------------------------------------------------------------------------------------------------------------------------ |
| Ruby on rails | Experience    | --     | Only worked on an established project that I added things to, instead of creating something from scratch                 |
|               | Compatibility | --     | I mainly work on Windows machines, which does not have great compatibility with Ruby (on rails) without the use of a VPN |
|               | Stack         | +++    | Full stack framework, so it would be able to do front, database and backend in 1 language/framework                      |
|               |               |        |                                                                                                                          |
| Svelte        | Experience    | --     | Worked in svelte a little bit for a few school assignments, but was not my strong suit.                                  |
|               | Compatibility | ++     | Shouldn't be any issues running on whatever system                                                                       |
|               | Stack         | -      | Just front-end, so I would need other methods to communicate with a database and API                                     |
|               |               |        |                                                                                                                          |
| Vanilla JS    |               |        |                                                                                                                          |



## Security

## Scaling/Reliability to the extreme

## Help

