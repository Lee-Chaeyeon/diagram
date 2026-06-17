# diagram
다이어그램 생성 및 편집용

```mermaid
%%{init: {'theme': 'neutral', 'themeVariables': { 'primaryColor': '#F4F5F7', 'edgeLabelBackground':'#ffffff', 'clusterBkg':'#FAFAFA', 'clusterBorder':'#E0E0E0'}}}%%
graph TB

    %% 데이터 소스 영역
    subgraph S1["Data Source"]
        A1["드론 영상"]
        A2["ESP32-CAM 영상"]
        A3["테스트 영상"]
    end

    %% AI 및 분석 서버 영역 (Flask 웹서버 내부)
    subgraph S2["Flask Web Server / AI Pipeline"]
        B["YOLOv8 객체 탐지 모델"]
        
        subgraph S2_1["분석 및 판단"]
            C1["밀집도 분석 (사람)"]
            C2["야생동물 판단 (멧돼지, 고라니)"]
        end
        
        D["위험 등급 분류"]
        E["실시간 관제 화면 표시"]
    end

    %% 저장소 영역
    subgraph S3["Storage"]
        F1[("위험 이력 저장<br>(데이터 저장소)")]
        F2[("캡처 이미지 저장")]
    end

    %% 사용자 영역
    G[["사용자 (관제 시스템)"]]

    %% --- 데이터 흐름 및 연결 관계 ---
    
    %% 1. 데이터 입력
    A1 -->|입력 데이터| B
    A2 -->|입력 데이터| B
    A3 -->|입력 데이터| B

    %% 2. AI 모델 내부 처리
    B --> C1
    B --> C2
    
    %% 3. 위험 등급 분류 및 화면 표시
    C1 --> D
    C2 --> D
    D --> E

    %% 4. 실시간 화면에서의 저장 및 출력
    E -->|출력/저장| F1
    E -->|출력/저장| F2

    %% 5. 상호 연결 및 관제 흐름
    G <-->|실시간 모니터링| E
    G <-->|데이터 조회 및 이력 관리| F1
    G <-->|이미지 확인| F2

    %% 스타일 정의 (현대적이고 직관적인 톤앤매너)
    style B fill:#EBF5FF,stroke:#1E88E5,stroke-width:2px;
    style C1 fill:#E8F5E9,stroke:#43A047,stroke-width:1px;
    style C2 fill:#E8F5E9,stroke:#43A047,stroke-width:1px;
    style D fill:#FFF3E0,stroke:#FB8C00,stroke-width:2px;
    style E fill:#EDE7F6,stroke:#5E35B1,stroke-width:2px;
    style F1 fill:#ECEFF1,stroke:#607D8B,stroke-width:1px;
    style F2 fill:#ECEFF1,stroke:#607D8B,stroke-width:1px;
    style G fill:#263238,stroke:#263238,stroke-width:2px,color:#fff;
{content: }
