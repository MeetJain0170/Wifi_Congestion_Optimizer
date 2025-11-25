# 📡 WiFi Congestion Balancing System  
### Intelligent Multi-Floor AP Load Distribution • Real-time Visualization • Algorithmic Network Simulation

This project simulates and visualizes **WiFi Access Point congestion** across a multi-floor campus using advanced algorithms, live WebSocket updates, and an interactive D3.js interface.

It solves the common problem found in real universities:  
> *“Everyone connects to the closest AP → a few APs explode with load while others sit idle.”*

This system balances users intelligently across APs in real time, visualizes their movement, and evaluates dynamic network health.

---

## 🚀 Features

### **🔧 Backend Simulation**
- Real multi-floor environment with 7 floors & dozens of rooms  
- Intelligent user placement & movement  
- Access Point constraints (band, airtime, load, capacity)  
- RSSI-based AP selection  
- Band-based coverage simulation (2.4 / 5 / 6 GHz)  
- Dynamic AP reassignment  
- Live WebSocket state updates (every 0.2 seconds)

### **📊 Frontend Visualization**
- Full-campus multi-floor SVG visualization  
- Animated WiFi coverage rings  
- Live user movement trails  
- Dotted lines showing user–AP associations  
- Sidebar floor dashboard (load per floor, user count)  
- AP-Killer (test tool) that floods APs with load  
- Heatmap mode for user density  
- WebSocket live status & error panel  
- Glassmorphism UI with glowing AP nodes

### **🧠 Algorithms Integrated**
1. **Minimum-Cost Maximum Flow (MCMF)**  
2. **Greedy Load Redistribution**  
3. **Priority Queue–based Assignment**  
4. **Graph Modeling for AP Selection**

Used to distribute users across APs **optimally and fairly**.

---

## 🧱 Project Architecture
```
Wifi_Congestion_System/
│
├── WifiLoadBalancing
│ ├── data/
│ │ ├── aps.json # Access point definitions
│ │ ├── config.json # Default band, settings
│ │ └── users.json # Generated simulation users
│ │
│ ├── frontend/
│ │ ├── assets/bg.png
│ │ ├── data/campus_layout.json # Rooms, floors, coordinates
│ │ └── index.html # Full interactive visualization
│ │
│ ├── src/
│ │ ├── algorithms/
│ │ │ ├── cost_function.py
│ │ │ ├── graph_model.py
│ │ │ ├── greedy_redistribution.py
│ │ │ ├── mcmf.py
│ │ │ └── priority_queue.py
│ │ │
│ │ ├── simulation/
│ │ │ ├── simulator.py # Core simulation engine
│ │ │ ├── ap_killer.py # Load-attack tool
│ │ │ └── generate_initial_data.py# User & AP initialization script
│ │ │
│ │ └── main.py # FastAPI backend + websocket
│
├── requirements.txt
├── foldertree.py
└── runcode.txt
```
---

## ⚙️ How It Works

### **Backend (FastAPI + Python)**
- Runs a simulation loop (`simulator_loop`)  
- Updates user movement, AP load, connectivity  
- Calculates dynamic RSSI based on band + distance  
- Sends complete state via WebSocket to frontend  
- Exposes REST APIs to add/remove users, change band, move AP-Killer

### **Frontend (D3.js + TailwindCSS)**
- Renders the entire campus floor-by-floor  
- Updates AP load arcs and user movement in real time  
- Shows heatmap overlays for dense rooms  
- Lets you switch WiFi bands and visualize coverage drop  
- Provides debug logs + network status

---

## 🎮 Interaction Controls

| Feature | Control |
|--------|---------|
| Switch WiFi Band | Buttons: **2.4 / 5 / 6 GHz** |
| Move AP-Killer | `W A S D` keys |
| Deploy AP-Killer | Button in sidebar |
| Add user to a floor | Sidebar + button |
| Remove user | Sidebar – button |
| Zoom | + / – buttons |
| Pan | Mouse drag |

---

## 🖼️ Screenshots / Demo (Add later)
> Replace these with real screenshots








---

## 🔌 API Endpoints

### **State & System**
GET /status
GET /state

markdown


### **User Management**
POST /floor/{level}/add_user
POST /floor/{level}/remove_user

markdown


### **Band Control**
POST /setband
{
"band": "2.4" | "5" | "6"
}

markdown


### **AP-Killer**
POST /apkiller/deploy
POST /apkiller/withdraw
POST /apkiller/floor/{level}
POST /apkiller/move { vx, vy }




---

## 🛠️ Setup Instructions

### **1. Install dependencies**
pip install -r requirements.txt

markdown


### **2. Generate initial data**
python WifiLoadBalancing/src/simulation/generate_initial_data.py

markdown


### **3. Run backend**
uvicorn WifiLoadBalancing.src.main:app --reload --port 8000

markdown


### **4. Open frontend**
Just open:
WifiLoadBalancing/frontend/index.html



(or serve using Live Server)

---

## 🎯 Future Improvements
- ML-based AP selection  
- Predictive load balancing  
- Building-wide roaming optimization  
- Real AP integration (UniFi / Cisco)  
- Admin dashboard with alerts

---

## 👨‍💻 Authors
**Meet Jain**  
Advanced Algorithms Project  
UGDX School of Technology

---

## ⭐ If you like this project…
Consider giving it a **★ star** on GitHub!

---
