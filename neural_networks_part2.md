# Neural Networks: Diffusion Models, Self-Driving AI, and Autonomy Levels

## 4. How Diffusion Models Work for Image Generation

### The Core Idea

Diffusion models have a counterintuitive foundation: rather than learning to *draw* an image from scratch, they learn to *denoise*. The training process deliberately destroys images by adding noise, and the network learns to reverse that destruction.

---

### The Forward Process (Training Time)

A real image is systematically destroyed over ~1000 tiny steps by adding Gaussian noise at each step according to a mathematical schedule. By the end, every training image has been reduced to indistinguishable white noise — the same featureless Gaussian distribution regardless of what the original image was.

The neural network (typically a U-Net architecture) is trained to look at any noisy intermediate image and predict the noise that was added. It sees millions of (noisy image, timestep, true noise) triplets and learns to denoise from every noise level simultaneously.

| Timestep | What happens |
|---|---|
| t = 0 | Clean original image |
| t = 1–100 | Tiny amounts of noise added; image still recognizable |
| t = 500 | Roughly half signal, half noise |
| t = 900+ | Nearly pure noise; only faint structure remains |
| t = T | Pure Gaussian noise; indistinguishable from random |

The training loss is simply: `Loss = ||ε - ε_θ(xₜ, t)||²` — how wrong was the network's prediction of the noise?

---

### The Reverse Process (Generation Time)

Generation begins by sampling a random image from a Gaussian distribution — pure white noise with no structure. The denoising network then runs in reverse, repeatedly asking: "given this noisy image at timestep t, what noise should I subtract?" Each step removes a tiny amount of noise, and structure gradually emerges from nothing.

The key insight: the network never had to learn to "draw" anything. It only learned one skill — how to make a noisy image slightly less noisy. Running that skill backwards, step by step, generates coherent images.

---

### How Text Prompts Guide Generation

In models like Stable Diffusion and DALL-E, a text encoder (typically CLIP) converts your prompt into a vector embedding. This embedding is injected into the denoising network at every reverse step via cross-attention — nudging the denoising direction toward images that match the prompt at each step. The strength of this guidance is the "guidance scale" parameter visible in most image generation UIs.

---

### The Latent Diffusion Trick

Running 1000 denoising steps on full-resolution pixel images would be prohibitively slow. Most modern models (Stable Diffusion, etc.) work in a compressed "latent space":

1. A VAE encodes the image into a much smaller representation (typically 8× smaller per spatial dimension)
2. Diffusion happens in that compact latent space
3. A VAE decoder expands the result back to full resolution

This is why these models can run on consumer hardware.

---

### Why Diffusion Models Work So Well

The approach sidesteps the core difficulty of generative modeling — you never have to directly learn the astronomically complex distribution of all natural images. Instead you learn a simple, local denoising function and compose it many times to traverse from noise to image. The model learns what "natural images look like" implicitly, through the denoising task.

---

## 5. AI for Self-Driving Cars

### The Full Pipeline

A self-driving system is not a single neural network but a stack of AI and classical engineering working together. From bottom to top:

**Sensors** — four complementary modalities used simultaneously because each has different failure modes:
- *Cameras*: rich color and texture, fail in rain and darkness
- *LiDAR*: precise 3D point cloud via laser ranging, unaffected by lighting but degraded by heavy precipitation
- *Radar*: cheap, all-weather, accurate velocity measurement but low spatial resolution
- *GPS + HD maps*: centimeter-level localization when GPS signal is strong, plus pre-built road geometry

**Sensor fusion** — raw streams from all sensors must be merged into a single coherent scene. Sensors run at different frequencies, have different coordinate frames, and different latencies. Modern systems often use transformer architectures here, treating each sensor's output as tokens that cross-attend to each other.

**Perception (CNNs + transformers)** — three parallel tasks:
- *Object detection*: draw bounding boxes around every vehicle, pedestrian, cyclist, and obstacle
- *Semantic segmentation*: label every pixel — road, lane marking, sidewalk, vegetation
- *Localization*: match current sensor readings against the HD map to determine exact position

**Trajectory prediction** — knowing where agents are now isn't enough; the system must anticipate where they'll be in 3–5 seconds. Modern approaches use transformer or graph neural network models that reason over social context (e.g., a pedestrian near a crosswalk who has been glancing left is probably about to step off the curb). The output is a probability distribution over multiple possible future trajectories per agent.

**Planning** — three nested levels:
- *Route planning*: get from A to B (essentially GPS navigation)
- *Behavior planning*: should I change lanes? yield? wait for a pedestrian? (rule-based or reinforcement learning)
- *Motion planning*: the precise smooth trajectory over the next few seconds, subject to physical and comfort constraints

**Control** — the motion plan is translated into actual actuator commands (steering angle, throttle, brake pressure), typically by classical PID controllers rather than neural networks, since these are well-understood and certifiable for safety.

---

### The Modular vs. End-to-End Debate

There is a genuine philosophical divide in the industry:

- **Waymo's approach**: modular pipeline with distinct, testable components. Each module can be independently validated. Engineers can reason about why a specific decision was made. Waymo's co-CEO has argued that end-to-end architectures are "wildly inadequate to go to full autonomy safely and at scale."

- **Tesla's approach**: end-to-end neural networks that go from camera pixels nearly directly to steering commands. Tesla's AI chief argued that "codifying human values" in a modular system was too difficult, and scrapped hundreds of thousands of lines of explicit code in favor of a learned end-to-end architecture.

Both approaches have made remarkable progress. The core challenge for both remains the "long tail" — the endless variety of rare, unusual situations that are hard to anticipate in advance.

---

## 6. Waymo, Tesla, and Autonomy Levels

### The SAE Autonomy Scale

The Society of Automotive Engineers defines six levels of driving automation:

| Level | Name | Human responsibility |
|---|---|---|
| 0 | No automation | Driver does everything |
| 1 | Driver assistance | Single aids (cruise control, lane keep) |
| 2 | Partial automation | Car steers/accelerates; human must supervise |
| 3 | Conditional automation | Car handles most driving; may need human help |
| 4 | High automation | Fully self-driving within a defined area |
| 5 | Full automation | Self-driving anywhere, any conditions |

A critical legal threshold sits between Level 2 and Level 3: below Level 3, the human driver is always legally responsible. At Level 3 and above, the manufacturer assumes responsibility. This is why many companies have preferred Level 2 classifications even for very capable systems.

---

### Waymo: Genuine Level 4, Onboard Processing

Waymo operates fully driverless paid robotaxi services in San Francisco, Los Angeles, Phoenix, and Austin. It is a true Level 4 system within its operational domains.

A common misconception is that Waymo relies on centralized cloud processing. In reality, all real-time driving decisions — perception, prediction, planning — happen onboard in the vehicle itself. The car cannot afford the latency of a round trip to a data center for a split-second braking decision. Each Waymo vehicle carries a powerful onboard computer processing terabytes of sensor data per hour.

The cloud *is* used, but only for:
- Training new AI models offline
- Aggregating fleet data across all vehicles
- Pushing software updates to the fleet
- Remote monitoring and edge-case assistance

Wireless connectivity supports the fleet but is not required for safe operation.

---

### Tesla FSD: Level 2 in Consumer Cars, Level 4 in Robotaxi

Tesla's "Full Self-Driving" branding has been genuinely controversial. FSD (Supervised) — the system available to ordinary Tesla owners — is officially classified as a Level 2 system. The driver must remain attentive and ready to take control at all times. Tesla's own website states: "currently enabled features require active driver supervision and do not make the vehicle autonomous."

Tesla launched a commercial Robotaxi service in Austin, Texas in June 2025, initially with a safety employee in the passenger seat. By late January 2026, Tesla was operating Robotaxi in Austin without any employee in the car — genuine Level 4 operation within a geofenced area. As of August 2025, Tesla also launched Robotaxi in San Francisco, though California law requires a safety driver in the seat there.

FSD itself runs entirely on the car's onboard hardware (Tesla's custom AI chip, currently "Hardware 4"). Tesla uses camera-only perception — no LiDAR — arguing that the data from millions of customer vehicles in the wild provides sufficient training signal to make cameras work. Waymo argues that cameras alone are insufficient for the reliability needed in a fully driverless system.

---

### Key Comparisons

| | Waymo | Tesla FSD (consumer) | Tesla Robotaxi |
|---|---|---|---|
| Autonomy level | Level 4 | Level 2 | Level 4 (geofenced) |
| Human required | No | Yes, supervising | No |
| Sensors | Camera + LiDAR + radar | Camera only | Camera only |
| Processing | Onboard | Onboard | Onboard |
| HD maps required | Yes | No | No |
| Cities operational | SF, LA, Phoenix, Austin | Anywhere (with driver) | Austin, SF (limited) |
| Architecture | Modular pipeline | End-to-end neural net | End-to-end neural net |

---

### The Safety Data

Waymo has published comparative safety data showing significant advantages over human drivers: 92% fewer crashes with injuries to pedestrians, 82% fewer crashes injuring cyclists and motorcyclists, and 85% fewer crashes with serious injuries. No equivalent independently verified data exists yet for Tesla's Robotaxi at scale, given its recent and limited deployment.

---

*Generated from a conversation with Claude (claude.ai)*
