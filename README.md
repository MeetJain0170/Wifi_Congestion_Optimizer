📌 Project Title:

Campus WiFi Load Balancing Using Advanced Algorithms

🏫 Course:

Advanced Algorithms

👥 Team Members:

Reva Shukla — Algorithm Lead (MCMF, Graph Model, Cost Function)

Niyati — Simulation Lead (Movement, RSSI, AP Load)

Meet — Load Balancing Lead (Greedy Redistribution, Priority Queue)

🚀 Project Overview

Large university campuses have multiple WiFi access points (APs).
Students automatically connect to the nearest AP, causing:

Some APs to overload

Other APs to remain underutilized

Poor bandwidth and unstable connectivity

Our system solves this by implementing:

✔ Minimum-Cost Maximum Flow (MCMF)

For globally optimal user → AP assignment.

✔ Greedy Load Redistribution

For fast real-time adjustments when APs overload.

✔ Priority Queue (Min-Heap)

To efficiently select which users to move.

✔ Dynamic Simulation + Live Visualization

Using WebSockets + D3.js to show real-time movement & load changes.


System Architecture

 Users Move → RSSI Changes → AP Load Changes →
     ↓               ↓               ↓
        Simulation Layer (Niyati)
     ↓               ↓               ↓
 Graph & Cost Model (Reva) → MCMF (Optimal Assignment)
     ↓
 Greedy PQ Balancing (Meet) → Fix Overloads
     ↓
 WebSocket Backend (Reva)
     ↓
 D3.js Frontend (Live Visualization)




Core Components
1️⃣ Simulation Layer (Niyati)

Handles real-world WiFi dynamics:

User movement

RSSI calculation (based on distance and path loss formula)

AP airtime and load calculation

State updates every simulation tick

This layer feeds live data into the algorithms.

2️⃣ Algorithm Layer (Reva & Meet)
🔹 Minimum-Cost Maximum Flow (Reva)

Builds a flow network:

Source → Users → APs → Sink


Cost includes:

Distance

RSSI penalty

Airtime usage

Sticky client penalty

Channel interference

MCMF produces globally optimal AP assignments.

🔹 Greedy Load Redistribution (Meet)

Runs between MCMF steps.

Detect overloaded APs

Push affected users into a priority queue

Move weakest users (low RSSI / high usage)

Select nearest alternative AP with free capacity

Fast and efficient for real-time stability.

3️⃣ Frontend Visualization Layer

Interactive dashboard using D3.js:

Live moving users

AP coverage circles

AP colors based on load

Lines from users → assigned AP

Tooltips with RSSI, load, airtime, channel, etc.

WebSocket data every second

Gives a real-time view of network balancing.

# 🗂️ Folder Structure

WifiLoadBalancing/
│
├── frontend/                      # 🌐 D3.js Live Visualization UI
│   ├── index.html                #   → Main frontend page (Live Server)
│   └── data/
│        ├── aps.json             #   → Static AP layout for drawing
│        ├── users.json           #   → Static user layout (initial positions)
│        └── campus_layout.json   #   → Multi-floor campus map definition
│
├── src/
│   ├── main.py                   # ⚡ FastAPI backend + WebSocket broadcaster
│   ├── run_simulation.py         # 🎯 Offline algorithm test runner (no UI)
│   │
│   ├── simulation/               # 🧠 Core simulation engine
│   │   ├── simulator.py          #   → Handles movement, RSSI updates, AP load, greedy calls
│   │   ├── movement_generator.py #   → Movement patterns (random walk)
│   │   ├── environment_config.py #   → Parameters for movement + RSSI + AP behavior
│   │   ├── metrics.py            #   → Generates stats like load distribution, fairness
│   │   └── generate_initial_data.py # → Auto-generates realistic AP/user datasets
│   │
│   ├── algorithms/               # 🧮 All algorithm implementations
│   │   ├── graph_model.py            # → Builds bipartite network for MCMF
│   │   ├── mcmf.py                   # → Reva’s Minimum Cost Maximum Flow logic
│   │   ├── cost_function.py          # → Combined cost scoring for MCMF edges
│   │   ├── greedy_redistribution.py  # → Meet’s improved greedy load balancer
│   │   └── priority_queue.py         # → Meet’s stable priority queue for greedy
│   │
│   └── utils/                     # 🧰 Helper utilities
│       ├── file_loader.py         #   → Loads AP/user config files
│       ├── random_data_generator.py#   → Generates synthetic user/AP distributions
│       └── visualization.py       #   → Debug drawing (optional)
│
├── data/                           # 📦 Initial backend input data (used by simulator)
│   ├── aps.json                    # → Fixed AP coordinates + load + channel
│   ├── users.json                  # → Initial user positions + RSSI
│   └── config.json                 # → AP/user global settings
│
├── results/                        # 📊 Simulation outputs (saved summaries)
│
└── README.md                       # 📘 Documentation


🧪 How to Run the Project
✔ Backend (FastAPI WebSocket)
cd WifiLoadBalancing
source venv/bin/activate  (or venv\Scripts\activate on Windows)
python src/main.py


Backend runs on:

http://127.0.0.1:8000


WebSocket endpoint:

ws://127.0.0.1:8000/ws

✔ Frontend (D3.js Visualization)
cd WifiLoadBalancing/frontend
python -m http.server


Open in browser:

http://127.0.0.1:8000/index.html
