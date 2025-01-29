```plantuml
@startuml C4_Elements
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Container.puml
LAYOUT_WITH_LEGEND()

Person(user, "Registered User", "Logged-in users can create and join instances and play music.")
Person(moderator, "Moderator", "User with extra permissions to moderate instances")

System_Boundary(plugdj, "Plug.dj Remake") {
    Container(frontend, "Frontend Web Application", "User interface for interacting with the website.")
    Container(backend, "Backend API", "Communicates with database and external APIs")
    ContainerDb(db, "Database", "Stores user data, instance data, and chat history.")
}


System_Ext(stream, "Youtube API service", "Provides music/video content for instances")

Rel(user, frontend, "Chat, Vote, Create Playlists")
Rel(moderator, frontend, "Moderate Content/Users")

Rel(frontend, backend, "API Requests (Auth, User management, Instance management)")
Rel(backend, db, "Store/Retrieve Data")
Rel(backend, stream, "Fetch Media Content")
@enduml
```
