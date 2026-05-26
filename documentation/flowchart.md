flowchart TD
    A([START]) --> B[Initialize Database]
    B --> C[Show Main Menu]

    C --> D{What does\nthe user choose?}

    D -->|Join Queue| E[Enter customer name]
    E --> F{Name valid?}
    F -->|No| C
    F -->|Yes| G[Assign ticket number\nAdd to waiting list]
    G --> C

    D -->|Call Next| H{Is someone\nalready being served?}
    H -->|Yes| C
    H -->|No| I{Anyone\nwaiting?}
    I -->|No| C
    I -->|Yes| J[Call next customer\nSet status to Serving]
    J --> C

    D -->|Mark as Done| K{Is someone\nbeing served?}
    K -->|No| C
    K -->|Yes| L[Mark customer as Done\nFree up the counter]
    L --> C

    D -->|View Queue| M[Show all waiting customers]
    M --> C

    D -->|View History| N[Show all past records]
    N --> C

    D -->|View Statistics| O[Show queue stats]
    O --> C

    D -->|Delete Record| P[Remove selected record]
    P --> C

    D -->|Exit| Q([END])
