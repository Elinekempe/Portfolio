# Voor ondersteuning van diagrammen, de code van de Activity- en Use Case-diagram


### Activity Diagram 
``` 
@startuml
start
:Speler start spel;
:Laad highscores;
:Initialiseer bord (easy/medium/hard);

repeat
  :Speler kiest actie;
  if (Klik op cel?) then (ja)
    if (Cel is onthuld of vlag?) then (ja)
      :Geen actie;
    else (nee)
      if (Eerste klik?) then (ja)
        :Start timer;
      endif
      if (Cel is mijn?) then (ja)
        :Stop timer;
        if (Eerste klik <= 1s?) then (ja)
          :Toon alle mijnen;
          :Quick-loss melding;
          :Auto-restart;
          stop
        else (nee)
          :Toon alle mijnen;
          :Verliesmelding + geluid;
          :Opnieuw proberen -> restart;
          stop
        endif
      else (nee)
        :Onthul cel (flood-fill bij leeg);
        :Update bord;
        if (Gewonnen?) then (ja)
          :Stop timer;
          :Highscore check & opslaan;
          :Winmelding + geluid;
          :Confetti (meer bij record);
          :Opnieuw spelen -> restart;
          stop
        endif
      endif
    endif
  else (nee)
    if (Rechtsklik vlag?) then (ja)
      if (Cel is onthuld?) then (ja)
        :Geen actie;
      else (nee)
        :Toggle vlag;
      endif
    else (nee)
      if (Niveau knop?) then (ja)
        :Reset timer;
        :Laad nieuw niveau;
      else (nee)
        if (Herstart knop?) then (ja)
          :Reset timer;
          :Herstart huidig niveau;
        else (nee)
          :Wacht op volgende actie;
        endif
      endif
    endif
  endif
repeat while (Spel actief?) is (ja)
-> nee;
stop
@enduml
```


### Use Case Diagram 
``` 
@startuml
title Minesweeper - Use Case Diagram

actor ":Speler:" as Player <<User>>
actor ":Bezoeker:" as Visitor <<Guest>>  
actor ":Timer:" as Timer <<System>>

rectangle "=== Minesweeper Game ===" as System {
  
  together {
    (Start nieuw spel) as UC1
    (Selecteer niveau) as UC2
  }
  
  together {
    (Klik op cel) as UC3
    (Toggle vlag) as UC4
    (Herstart spel) as UC5
  }
  
  together {
    (Update timer) as UC6
    (Quick-loss check) as UC7
  }
  
  together {
    (Toon winbericht) as UC8
    (Opslaan highscore) as UC9
    (Bekijk records) as UC10
  }
}

Player -down-> UC1
Player -down-> UC2
Player -down-> UC3
Player -down-> UC4
Player -down-> UC5
Player -down-> UC8
Player -down-> UC10

Visitor -down-> UC1
Visitor -down-> UC2
Visitor -down-> UC10

Timer -down-> UC6
Timer -down-> UC7

UC8 -right-> UC9 : <<include>>
UC3 -up-> UC6 : <<include>>

note top of UC2
  **Opties:**
  • Easy (8×8, 10 mijnen)
  • Medium (12×12, 25 mijnen)
  • Hard (16×16, 50 mijnen)
end note

note bottom of UC7
  Auto-restart binnen 1 seconde
  om frustratie te voorkomen
end note

note right of UC9
  localStorage per niveau:
  minesweeper-highscore-{level}
end note
@enduml
```