# DSM 시스템 구조도

```mermaid
%%{init: {
  'theme': 'base',
  'themeVariables': {
    'primaryColor': '#F8FAFC',
    'primaryTextColor': '#1E293B',
    'primaryBorderColor': '#CBD5E1',
    'lineColor': '#475569',
    'secondaryColor': '#F1F5F9',
    'tertiaryColor': '#FFFFFF'
  }
}}%%
graph TB

%% 1. 데이터 소스 (맨 위)
subgraph S1["데이터 소스"]
    A1["🛸 드론 영상"]
    A2["📷 ESP32-CAM 영상"]
end

%% 2. AI 및 관제 프로세스 (중앙 메인 라인)
subgraph S2["시스템 설계: 시스템 구조"]
    B["🧠 YOLOv8 객체 탐지 모델"]
    
    subgraph S2_1["내부 처리 과정"]
        c1["👥 밀집도 분석 (사람)"]
        c2["🐗 야생동물 판단 (멧돼지, 고라니)"]
    end
    
    D["⚠️ 위험 등급 분류"]
    E["📺 실시간 관제 화면 표시"]
end

%% 3. 독립 영역 (데이터 저장소는 좌측, 사용자는 우측 유도)
F1[("🗄️ 데이터 저장소")]
G[["👤 사용자 (관제 시스템)"]]
F2["📋 위험 이력 저장"]

%% --- 스타일 지정 (정갈한 톤앤매너) ---
style S1 fill:#F8FAFC,stroke:#94A3B8,stroke-width:1.5px,stroke-dasharray: 4 4
style S2 fill:#F8FAFC,stroke:#475569,stroke-width:1.5px
style F1 fill:#EFF6FF,stroke:#3B82F6,stroke-width:2px
style G fill:#F0FDF4,stroke:#22C55E,stroke-width:2px
style F2 fill:#FFF7ED,stroke:#F97316,stroke-width:1.5px

%% --- 데이터 흐름 및 상호작용 (선 꼬임 방지 구조) ---
A1 -->|입력 데이터| B
A2 -->|입력 데이터| B

B --> c1
B --> c2

c1 --> D
c2 --> D
D --> E

%% 데이터 저장소 연동 (원본 흐름 반영)
F1 <-->|데이터 연동| E
F1 -->|데이터 제공| B

%% 관제 화면에서 뻗어나가는 흐름
E -->|이력 생성| F2

%% 사용자 상호작용 및 드론 제어 (⭐핵심 기능 반영)
G <-->|실시간 관제 화면 확인| E
G -->|데이터 조회/관리| F1
G -->|위험 이력 확인| F2
G ==>|🛸 드론 제어 명령 전달| A1

%% 화살표 스타일
linkStyle default stroke:#475569,stroke-width:1.5px;
linkStyle 13 stroke:#22C55E,stroke-width:2.5px; %% 드론 제어 선 강조
```
