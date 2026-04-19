erDiagram
    %% 1. 독립적인 엔티티
    EXHIBITION {
        Long id PK
        String title
        String description
    }

    %% 2. 핵심 엔티티
    USER {
        Long id PK
        String email
        String name
        String role
    }

    PROGRAM {
        Long id PK
        String title
        String type
    }

    %% 3. 스케줄 엔티티
    PERFORMANCE_SCHEDULE {
        Long id PK
        Long program_id FK
        DateTime start_time
    }

    EXPERIENCE_SCHEDULE {
        Long id PK
        Long program_id FK
        DateTime start_time
    }

    %% 4. 예약 및 게시글 엔티티
    RESERVATION {
        Long id PK
        Long user_id FK
        Long program_id FK "Null 허용 (입장권 처리용)"
        Long schedule_id FK "Null 허용 (입장권/체험 처리용)"
        String status
    }

    POST {
        Long id PK
        Long user_id FK
        String title
        String content
    }

    %% 관계선 (Relationships)
    USER ||--o{ RESERVATION : "예약한다 (1:N)"
    USER ||--o{ POST : "작성한다 (1:N)"
    
    PROGRAM ||--o{ PERFORMANCE_SCHEDULE : "공연 일정을 가진다 (1:N)"
    PROGRAM ||--o{ EXPERIENCE_SCHEDULE : "체험 일정을 가진다 (1:N)"
    PROGRAM ||--o{ RESERVATION : "예약 대상이 된다 (1:N)"
    
    PERFORMANCE_SCHEDULE ||--o{ RESERVATION : "예약 대상이 된다 (1:N)"
    EXPERIENCE_SCHEDULE ||--o{ RESERVATION : "예약 대상이 된다 (1:N)"
