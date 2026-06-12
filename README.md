Name : Syed Daniyal Hussain
Roll no: 2K23/CSM/134

# AI System Specification — Smart Traffic Signal Controller

**Course:** Introduction to Artificial Intelligence  
**Topic:** PEAS Framework and Task Environment Analysis  
**System Selected:** E — Smart Traffic Signal Controller for reducing congestion in cities

---

## Task 1: PEAS Specification

### Performance Measures — How is success measured?
- Average waiting time reduction per vehicle
- Emergency vehicle (Ambulance / Fire Brigade) clearance time
- Accident rate reduction percentage
- Traffic flow smoothness score

### Environment — Where does the agent operate?
- Multi-lane urban roads and complex intersections
- Changing weather conditions (Rain, Fog)
- Presence of pedestrians and cyclists

### Actuators — What actions does the AI take?
- Traffic signal lights (Red / Yellow / Green control)
- Digital display boards for alerts and diversions *(e.g., weather change, Zebra Crossing ahead)*
- Audio alert system for visually impaired pedestrians

### Sensors — How does the AI perceive the environment?
- High-resolution RGB cameras with high FPS (Frames Per Second)
- WIM (Weigh-In-Motion) underground road sensors for vehicle weight and speed detection
- Acoustic sensors for detecting emergency sirens (Ambulance, Fire Brigade)
- Arduino-based pedestrian detection system at Zebra crossings
- Weather sensors for rain and fog detection
- Computer vision systems for road condition monitoring

---

## Task 2: Environment Classification

| Dimension | Classification | Justification |
|-----------|---------------|---------------|
| Observability | **Partially Observable** | Agent can only perceive roads and intersections where its sensors are physically installed |
| Agents | **Multi-agent** | A large city like Karachi requires multiple coordinated signal controllers across many intersections |
| Determinism | **Stochastic** | Unpredictable driver behavior and mechanical failures can change outcomes despite correct AI decisions |
| Sequence | **Sequential** | Each signal decision affects traffic flow for the next 5–10 minutes, so past actions impact future states |
| Dynamics | **Dynamic** | Traffic, pedestrians, and weather all change continuously while the agent is still processing its decision |
| Continuity | **Continuous** | Vehicle speeds and traffic density vary constantly with no fixed discrete steps |

---

## Task 3: Critical Analysis

### Q1 — Which dimension poses the greatest technical challenge?

The most challenging dimension is the **Stochastic Environment**. Even if the AI system works perfectly, human behavior remains unpredictable — drivers may run red lights, make sudden lane changes, or cause accidents. Weather conditions like fog and rain also add randomness that is difficult to model. This means the AI can never fully guarantee outcomes, making it hard to design a reliable decision-making system.

### Q2 — Utility Function and Trade-off

A key trade-off in this system is **Traffic Flow Speed vs. Emergency Vehicle Priority.**

**Utility Function:**
```
U = 0.7 × Emergency_Clearance + 0.3 × Traffic_Flow_Efficiency
```

Normally, the agent balances smooth traffic flow while keeping a path ready for emergency vehicles.

If the weight of `Emergency_Clearance` is **doubled (0.7 → 1.4)**, the agent would immediately override all normal signal cycles whenever a siren is detected — even during peak hours. This clears the path faster for ambulances ✅ but may cause heavier congestion on other roads ❌.

---

## Task 4: Structured Data Representation (JSON)

```json
{
  "system_name": "Smart Traffic Signal Controller",
  "peas": {
    "performance_measures": [
      "Average waiting time reduction per vehicle",
      "Emergency vehicle clearance time",
      "Accident rate reduction percentage",
      "Traffic flow smoothness score"
    ],
    "environment": "Multi-lane urban roads with complex intersections, changing weather conditions, pedestrians and cyclists",
    "actuators": [
      "Traffic signal lights (Red/Yellow/Green control)",
      "Digital display boards for alerts and diversions",
      "Audio alert system for visually impaired pedestrians"
    ],
    "sensors": [
      "High-resolution RGB cameras with high FPS",
      "WIM underground road sensors for vehicle weight and speed",
      "Acoustic sensors for detecting emergency sirens",
      "Arduino-based pedestrian detection at zebra crossings",
      "Weather sensors for rain and fog detection",
      "Computer vision systems for road condition monitoring"
    ]
  },
  "environment_classification": {
    "observability": {
      "choice": "Partially Observable",
      "justification": "Agent can only perceive roads and intersections where its sensors are physically installed"
    },
    "agents": {
      "choice": "Multi-agent",
      "justification": "A large city like Karachi requires multiple coordinated signal controllers across many intersections"
    },
    "determinism": {
      "choice": "Stochastic",
      "justification": "Unpredictable driver behavior and mechanical failures can change outcomes despite correct AI decisions"
    },
    "sequence": {
      "choice": "Sequential",
      "justification": "Each signal decision affects traffic flow for the next 5 to 10 minutes, so past actions impact future states"
    },
    "dynamics": {
      "choice": "Dynamic",
      "justification": "Traffic, pedestrians and weather all change continuously while the agent is still processing its decision"
    },
    "continuity": {
      "choice": "Continuous",
      "justification": "Vehicle speeds and traffic density vary constantly with no fixed discrete steps"
    }
  },
  "utility_function": "U = 0.7 * Emergency_Clearance + 0.3 * Traffic_Flow_Efficiency"
}
```

---

*Assignment submitted for: Introduction to Artificial Intelligence*
