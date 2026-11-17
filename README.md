# Hey, I'm Siddharth Sivapuram 👋

### Electronics & Communication Engineering @ IIT Guwahati | Software Engineering | AI/ML | Systems Engineering

I'm an ECE undergraduate at **IIT Guwahati**, interested in building software systems that combine strong engineering fundamentals with intelligent algorithms.

My interests include **Software Engineering, Artificial Intelligence, Machine Learning, Backend Development, and Systems Engineering**. I enjoy understanding problems from the ground up, experimenting with algorithms, and building practical end-to-end solutions.

- 🎓 Electronics and Communication Engineering — IIT Guwahati
- 💻 Interested in Software Engineering, AI/ML, and systems-oriented development
- 🧠 Exploring machine learning, graph neural networks, probabilistic models, and algorithms
- ⚙️ Interested in concurrency, performance optimization, and scalable software
- 🚀 Building projects that connect theoretical concepts with practical applications

---

## 🚀 Featured Projects

My main projects explore three different engineering areas: low-level systems, applied AI/ML, and real-time intelligent applications.

## 01. In-Memory Virtual File System

**Systems Engineering · C++17 · Concurrency · Data Structures**

[View Repository](https://github.com/siddharthh-29/In-Memory-VFS)

A virtual file system designed from scratch in C++17 to provide lightweight hierarchical data management with thread safety and persistence.

### Problem

Applications such as database storage engines, in-memory caches, and sandboxed execution environments need efficient hierarchical data management.

Building such a system introduces several challenges:

- Concurrent reads and writes can cause race conditions.
- In-memory data is volatile and needs a persistence mechanism.
- Deeply nested directory structures require careful memory and resource management.

### Engineering Approach

- **Composite Design Pattern:** Represent files and directories through a common hierarchical structure.
- **N-ary Tree:** Organize directories and files into a tree-based structure.
- **Reader–Writer Synchronization:** Use `std::shared_mutex` to support concurrent readers while protecting modifications.
- **Binary Serialization:** Flatten the in-memory tree into a custom binary representation for persistence.
- **State Reconstruction:** Rebuild the virtual file system from serialized data after restart.

### Engineering Goals

- Thread-safe file and directory operations.
- Efficient hierarchical traversal and manipulation.
- Persistent state without relying on an external database.
- Target throughput of 100,000+ operations per second under concurrent workloads.
- Sub-millisecond operation latency as a performance objective.

**Tech:** C++17 · Object-Oriented Programming · Data Structures · N-ary Trees · `std::shared_mutex` · Binary Serialization · Concurrency

---

## 02. Intelligent GNSS Map Matching — Smart India Hackathon

**Applied AI/ML · Geospatial Intelligence · Hidden Markov Models**

### Problem

Coarse GNSS data can make it difficult to distinguish between vehicles travelling on nearby roads, particularly:

- Highways and service roads.
- Flyovers and roads underneath them.
- Parallel or closely spaced road segments.

GNSS measurements can also contain noise, outliers, and intermittent positioning errors.

The objective was to develop an intelligent map-matching solution that identifies the road type travelled by a vehicle and supports applications such as automated tolling and driving-pattern analysis.

### Solution Architecture

**1. GNSS Data Preprocessing**

- Process coarse GNSS observations and vehicle-related features.
- Apply Kalman filtering for position estimation.
- Use Z-score-based outlier detection to identify anomalous measurements.
- Work with features such as latitude, longitude, speed, and height.

**2. Map Matching**

- Integrate the OSRM API to map-match GNSS trajectories to road networks.
- Snap observed coordinates to road segments.
- Use road information to distinguish highways, service roads, and unknown road types.

**3. Switching Hidden Markov Model**

Developed a Switching Hidden Markov Model-based approach to classify the hidden road state from observed vehicle data.

Two configurations were explored:

| Configuration | Features |
|---|---|
| Simple model | Latitude, longitude, speed |
| Complex model | Latitude, longitude, speed, acceleration, height |

The model predicts hidden road categories:

- Highway
- Service road
- Flyover

**4. Journey Analytics**

- Estimate distance travelled across different road categories.
- Calculate time spent on each road type.
- Generate trajectory-based journey statistics.

**5. Web Application**

Built a web interface using Flask, HTML, CSS, and JavaScript.

Features include:

- Uploading `.pos` and `.kml` trajectory files.
- Visualizing vehicle trajectories using OpenStreetMap.
- Displaying road-category statistics.
- GNSS-based toll calculation.

### Applications

- GNSS-based automated tolling.
- Insurance driving-pattern analysis.
- Road-level vehicle tracking and analytics.

**Tech:** Python · Flask · Hidden Markov Models · Switching HMM · Kalman Filtering · Z-score Outlier Detection · OSRM · OpenStreetMap · HTML · CSS · JavaScript

---

## 03. SpatialMesh — Immersive 3D Spatial Audio

**Samsung EnnovateX AX Hackathon 2026 · Problem Statement 8**

**AI/ML · Graph Neural Networks · Audio Processing · Real-Time Systems**

[View Repository](https://github.com/siddharthh-29/SpatialMesh-AX2026) · [Watch Demo](https://youtu.be/VT_2EgvCe5k) · [Installation Guide](https://youtu.be/PEdSFaae3fc) · [Presentation](https://drive.google.com/file/d/1mayaPPAfyEff-Vt1P6nm2eUfwn0psPMj/view?usp=sharing)

**Team SpatialMesh — IIT Guwahati**

Team members: Rohith Sai Anvesh Polisetty and Siddharth Sivapuram.

### Problem

Traditional multi-party voice calls do not provide meaningful spatial separation between participants. Multiple speakers can sound as though their voices originate from the same direction.

SpatialMesh aims to create a more natural conversation experience by positioning each participant at a distinct location in a virtual 3D soundscape.

The system uses AI to predict speaker positions and HRTF-based binaural rendering to reproduce spatial audio through headphones.

### System Architecture

```text
       Raw Mono Audio
       (4 Participants)
              |
              v
    HRTF Pre-Convolution
       (SONICOM Dataset)
              |
              v
      CNN Audio Encoder
     (4-layer 1D CNN)
       128-d Embedding
              |
              v
       Spatial Graph
    133-d Nodes / 7-d Edges
              |
              v
       GATv2Conv GNN
       2 Layers / 4 Heads
              |
              v
    Azimuth + Elevation
       Per Participant
              |
              v
     HRTF Binaural Rendering
              |
              v
       Stereo Audio
          Headphones
```

### 1. HRTF-Based Spatial Audio Processing

Used Head-Related Transfer Functions (HRTFs) to model how sound changes when it travels from a particular spatial position to the listener's ears.

The binaural rendering process applies separate filters for the left and right ears:

\[
y_L(t)=x(t)*h_L(t,\theta,\phi)
\]

\[
y_R(t)=x(t)*h_R(t,\theta,\phi)
\]

Where:

- \(x(t)\) is the input audio.
- \(h_L\) and \(h_R\) are the left and right HRTF filters.
- \(\theta\) and \(\phi\) represent azimuth and elevation.

Used the SONICOM HRTF dataset for spatial acoustic processing.

### 2. CNN Audio Encoder

Implemented a four-layer 1D CNN to extract audio representations.

- Generates a 128-dimensional learned embedding for each speaker.
- Encodes useful audio characteristics for subsequent spatial reasoning.
- Integrates with the graph-based speaker representation.

### 3. Graph-Based Speaker Representation

Modelled the entire multi-party conversation as a spatial graph.

- Each speaker is represented as a graph node.
- Each node contains 133 features.
- Each directed edge contains seven acoustic relationship features.
- The graph enables joint reasoning about the spatial arrangement of participants.

### 4. GATv2 Graph Neural Network

Used `GATv2Conv` from PyTorch Geometric to reason over the speaker graph.

- Two graph attention layers.
- Four attention heads.
- Uses directed edge features.
- Predicts azimuth and elevation coordinates for each speaker.

An important implementation finding was that the initial GATConv approach did not make use of the edge features as intended. The architecture was changed to GATv2Conv to incorporate edge information.

### 5. Binaural Audio Rendering

The predicted spatial coordinates are used to select the corresponding HRTF characteristics.

The system then performs HRTF convolution to generate binaural output, creating the perception of speakers positioned at different locations around the listener.

### 6. Spatial Context Agent

Implemented a rule-based monitor–reason–act loop that monitors the call context and triggers spatial adjustments.

The four documented tool calls are:

| Tool | Function |
|---|---|
| `trigger_gnn_reassign()` | Reassigns speaker positions on mute/unmute events |
| `boost_ild_separation()` | Widens azimuth separation during noise spikes |
| `update_world_lock()` | Updates the soundfield when head yaw exceeds 35° |
| `set_speaker_priority
