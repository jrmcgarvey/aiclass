# 6. Artificial Vision in Motion: Self-Driving Cars

---

## 6.1 Historical Roots: Learning to Stay on the Road

The earliest neural network approach to autonomous driving — ALVINN (Autonomous Land Vehicle in a Neural Network), developed by Dean Pomerleau at Carnegie Mellon in the late 1980s — already contained the seed of the central challenge. The system took camera video and sensor data as input and was trained, using backpropagation and gradient descent, to predict the steering action a human driver would take at each moment. The loss function penalized deviations from the human's actual behavior, and the network learned to imitate good driving remarkably well — in conditions similar to its training data.

The failure mode was equally instructive. A model trained only on correct driving has never seen what to do when the vehicle drifts off course, because the training data never includes that situation. Once the car began to deviate, it entered territory the network had never encountered, and it had no learned basis for recovery. It would continue drifting, or behave erratically, having no examples of "I am off the intended path — here is how to return."

The naive fix — deliberately including off-track examples in the training data — fails for an obvious reason: the model would then learn to imitate that behavior too.

The solution that emerged is known as **DAgger** (Dataset Aggregation), formalized by Stéphane Ross and colleagues around 2011. The insight is subtle but important. Rather than having a human physically override the vehicle whenever it drifts, a human expert observes the states the model actually visits — including the slightly-off-nominal ones — and labels each state with the correct action they would take. Those state-action pairs from real, imperfect operation are added to the training set, and the model is retrained. Iterating this process produces a model that has learned recovery behavior from states it actually reaches, not just from the idealized states an expert would visit. This combination of supervised learning with ongoing human feedback closed the gap that purely imitation-based training could not.

---

## 6.2 The Full Stack

A self-driving vehicle is not a single AI system but a tightly integrated pipeline of AI and classical engineering components, each solving a distinct subproblem, with the outputs of each stage feeding the next. Understanding this stack reveals both the sophistication of the engineering and the reasons why full autonomy has proven so difficult to achieve.

The pipeline begins with **sensors**. A fully capable autonomous vehicle typically carries four complementary sensing modalities. **Cameras** provide rich color and texture information across a 360-degree field but perform poorly in rain, fog, and darkness. **LiDAR** fires pulses of laser light and measures the return time to construct a precise three-dimensional point cloud of the surroundings — accurate and lighting-independent but expensive, and degraded by heavy precipitation. **Radar** is cheap, penetrates weather reliably, and measures the velocity of detected objects with high accuracy, though its spatial resolution is too coarse to distinguish object shapes. **GPS combined with high-definition maps** provides centimeter-level positional accuracy when satellite signal is strong and supplies pre-built knowledge of road geometry, lane markings, and speed limits.

Beyond these four primary modalities, autonomous vehicles also incorporate sensors that more closely parallel other aspects of human perception. **Inertial measurement units (IMUs)** — arrays of accelerometers and gyroscopes — detect vehicle slip, unexpected lateral forces, and orientation changes, giving the system a digital analog of the vestibular sense that tells a human driver when the car is sliding on ice. Wheel speed sensors and suspension data can signal road surface conditions. There is active research interest in using **microphones** to detect emergency vehicle sirens, horns, and other auditory cues, though audio has not yet become a primary sensing modality in production systems.

The diversity is deliberate. Each sensor has distinct failure modes; the system is designed so that any single sensor can fail without disabling the car. That redundancy comes at significant hardware cost, which has become a major point of differentiation between competing approaches to the problem.

Humans navigate with a still richer sensory palette — eye contact with pedestrians, the sound of tires on wet pavement, a vibration through the steering wheel, spoken navigation guidance — and current autonomous systems replicate only a subset of these inputs. The gap is real, if narrowing.

---

## 6.3 Perception

Sensor data from all modalities must first be fused into a unified representation of the scene. This **sensor fusion** step is more complex than it might appear: the sensors run at different frequencies, have different spatial coordinate frames, and have different latencies. Transformer architectures have become the approach of choice here, treating each sensor's output as a sequence of tokens that cross-attend to each other, learning which information from which sensor is most relevant in any given driving context.

From the fused representation, three parallel perception tasks proceed. **Object detection** assigns bounding boxes and class labels to every vehicle, pedestrian, cyclist, and obstacle in the scene. CNNs trained on massive datasets of labeled driving footage do this reliably in good conditions. **Semantic segmentation** labels every pixel of every camera image with a category — road surface, lane marking, sidewalk, vegetation, building — giving the car a fine-grained understanding of the drivable space. **Localization** matches current sensor readings against the stored HD map to determine the car's precise position and heading, typically to within a few centimeters.

---

## 6.4 Prediction and Planning

Knowing the current state of the scene is necessary but not sufficient. The system must anticipate the near-future behavior of every other agent — where will that cyclist be in three seconds? Will that pedestrian at the corner step into the road? This trajectory prediction problem is among the hardest in the stack because human behavior is governed by social conventions and intentions that are not directly observable.

Modern prediction models use transformers or graph neural networks that represent each agent as a node in a graph and reason over the interactions between them. A pedestrian facing the road, near a crosswalk, who has been glancing toward oncoming traffic, is likely about to cross. The output of such a model is not a single predicted trajectory for each agent but a probability distribution over several plausible futures. Planning must then navigate safely across all plausible futures simultaneously, not just the most likely one.

Planning itself is organized into three nested levels. **Route planning** is essentially navigation: select a path through the road network from origin to destination. **Behavior planning** makes higher-level tactical decisions at each moment: when to change lanes, when to yield, when to proceed through an intersection, how to react to an unusual obstacle. **Motion planning** works out the precise trajectory — the curve through space and the speed profile along it — that the vehicle should execute over the next few seconds, subject to both physical constraints (steering geometry, tire friction limits) and comfort constraints (passengers notice sudden lateral accelerations even when mechanically safe).

The final stage, **control**, translates the planned trajectory into actual commands to the vehicle's actuators: steering angle, throttle percentage, brake pressure. This stage is typically implemented with classical feedback controllers — PID controllers and model predictive control — rather than neural networks, because these methods are well-understood, formally analyzable, and certifiable for safety.

---

## 6.5 The Modular vs. End-to-End Debate

The pipeline described above represents the **modular philosophy**: each stage of reasoning is implemented as a distinct, interpretable, testable component with a human-designed interface specifying what it should produce. The perception module is told to output bounding boxes and class labels; the prediction module is told to output trajectory probability distributions; the planning module is told to produce a safe motion plan. Neural networks operate *within* each module, learning from data — but what they are learning to produce is defined by engineers. The result is that any stage can be individually inspected, tested, and debugged: if the car behaves unexpectedly, engineers can examine the output of each stage and determine precisely where the reasoning went wrong.

Tesla has pursued a substantially different philosophy, using **end-to-end neural networks** that take camera pixels as input and produce driving commands as output, with intermediate representations learned rather than designed. The argument for this approach is that human engineers cannot anticipate all the intermediate representations that matter; learning them from data may produce a richer internal model than hand-engineered modules can. Tesla has progressively replaced its earlier hand-engineered modules with learned representations, arguing that the network can discover better internal structure than engineers can design.

Both approaches have made remarkable progress. The fundamental challenge for both is the long tail of rare situations: the child who runs into the road between parked cars, the construction zone laid out in a way no training example anticipated, the driver ahead behaving in an inexplicable way. No finite training set covers all such cases, and the consequences of failure are severe.

This long-tail problem cuts more deeply against the end-to-end approach. Neural networks are fundamentally interpolators: they perform well on inputs similar to their training distribution and degrade on inputs far from it. Rare events — a mattress falling from a truck, a horse on the highway, an unusual temporary road configuration — may appear too infrequently in training data for a network to learn robust responses. And because neural networks require many examples of a pattern to learn it reliably, a single dashcam recording of an unusual situation contributes almost nothing. The physical world generates genuinely novel situations continuously; the tail is mathematically inexhaustible.

The 2018 Uber autonomous vehicle fatality in Tempe, Arizona is a sobering illustration. The system struck and killed Elaine Herzberg, who was walking her bicycle across a multi-lane road at night. The NTSB investigation found that the system cycled between classifying her as an unknown object, a vehicle, and a bicycle — never settling on a stable classification — and was not designed to infer from a bicycle detection that a human was likely nearby. The emergency braking system had been disabled by engineers to reduce false positives. This was a perception failure under an unusual combination of circumstances that the training distribution had not adequately covered.

---

## 6.6 Waymo's World Model: Neuro-Symbolic Integration

A crucial and often underappreciated element of Waymo's modular approach is its explicit **world model** — a set of physics-based, algorithmically encoded representations of how the physical world behaves. This is distinct from what the neural networks have learned statistically from data: it is structured knowledge encoded directly by engineers, of the kind associated with classical "Good Old-Fashioned AI" (GOFAI). The result is a **neuro-symbolic architecture** — a hybrid that combines the pattern-recognition power of deep learning with the precision and generalizability of explicit knowledge representation.

The world model is not a safety net that the neural network falls back on when confused. It is woven into the system more deeply than that, operating in at least four distinct ways:

**As a constraint on neural network outputs.** Rather than letting the network predict anything and checking it afterward, the world model defines what outputs are physically valid. If the prediction module suggests a trajectory for a vehicle that violates kinematic constraints — turning sharper than physics allows at that speed — that trajectory is ruled out before planning considers it. The world model acts as a filter running in parallel with learned inference.

**As a prior that resolves uncertainty.** When sensor data is ambiguous — say, partial occlusion makes object classification uncertain — the world model provides probabilistic constraints. If the system knows it is at an intersection and something is moving at 12 mph on the sidewalk, the world model says this is almost certainly a cyclist, not a vehicle. The network's uncertainty is resolved partly by what physical and contextual plausibility dictates. This is Bayesian reasoning, not fallback.

**As the substrate for simulation.** Waymo runs continuous simulation of possible futures using the world model to propagate scenarios forward. The neural network's job is partly to assign probabilities to those simulated futures rather than to predict futures from scratch. This is a profound architectural difference from pure learned prediction.

**As the space within which planning operates.** Motion planning does not search through arbitrary trajectories — it searches through trajectories already constrained to be physically executable, geometrically consistent with the HD map, and within comfort limits. The world model defines the feasible space; planning finds the best option within it.

This architecture reflects one of the oldest debates in AI: explicit knowledge representation versus learning from data. Waymo's position is that some things we know precisely and should encode that way, while the neural networks handle what cannot be known analytically. It is arguably the most sophisticated real-world deployment of neuro-symbolic AI yet built.

---

## 6.7 The SAE Autonomy Scale

Discussion of self-driving cars is often confused by imprecise use of the term "autonomous." The Society of Automotive Engineers has defined a six-level taxonomy that provides useful precision:

| Level | Description | Human role |
|---|---|---|
| 0 | No automation | Driver performs all tasks |
| 1 | Driver assistance | Single aids, such as adaptive cruise control |
| 2 | Partial automation | Car manages steering and speed; human must supervise continuously |
| 3 | Conditional automation | Car manages driving; may request human takeover |
| 4 | High automation | Fully driverless within a defined operational domain |
| 5 | Full automation | Fully driverless in all conditions without restriction |

A legally and commercially critical threshold lies between Level 2 and Level 3. Below Level 3, the human driver retains legal responsibility at all times. At Level 3 and above, the manufacturer assumes responsibility for the vehicle's behavior during autonomous operation. This distinction has powerfully shaped how companies position their products.

---

## 6.8 Waymo: Onboard Intelligence

Waymo operates fully driverless paid robotaxi services across San Francisco, Los Angeles, Phoenix, and Austin — true Level 4 operation within those cities' defined operational domains. A common misconception is that Waymo vehicles rely on cloud computing for their real-time decisions. This is incorrect.

All time-critical decisions — perception, prediction, and planning — are executed onboard, in the vehicle, by a purpose-built computer processing the sensor data in real time. The physics of the situation demand this: a cellular round-trip to a data center and back introduces hundreds of milliseconds of latency. A pedestrian stepping into the road at 30 miles per hour covers several feet in that time.

The cloud is used — but for different purposes: training new models on aggregated fleet data, distributing software updates, remote monitoring, and providing human assistance in edge cases where the car has safely stopped to await guidance. A cellular outage would not cause a Waymo vehicle to stop or behave unsafely.

Each Waymo vehicle carries camera, LiDAR, and radar arrays together with the onboard computer that processes their output. This sensor suite is expensive, which has constrained Waymo's scaling relative to camera-only competitors.

---

## 6.9 Tesla: A Different Bet

Tesla's consumer "Full Self-Driving" product is officially classified as a Level 2 system. The driver must remain attentive and ready to intervene at all times; the system provides assistance but does not assume responsibility. Tesla's own documentation states this clearly, even as the product's name has attracted regulatory scrutiny for implying a capability it does not yet have.

Tesla's technical bet differs from Waymo's in two important respects. First, **camera-only sensing**: Tesla argues that humans navigate complex environments using only eyes, and that sufficient camera data — drawn from millions of customer vehicles driving millions of miles daily — can train a system to do the same, making expensive LiDAR unnecessary. Second, **end-to-end neural networks**: Tesla has progressively replaced its hand-engineered perception and planning modules with learned representations, arguing that the network can discover better internal representations than engineers can design.

Tesla launched a commercial robotaxi service in Austin, Texas in mid-2025, initially with a safety employee present in the passenger seat. By early 2026, the service was operating in Austin without any Tesla employee in the vehicle — genuine Level 4 operation within that geofenced area. The service has since expanded in limited form to San Francisco, though California regulations required a safety driver to remain seated there.

---

## 6.10 Beyond Passenger Cars: Autonomous Trucking

The economic case for autonomous vehicles may be even stronger in long-haul freight than in passenger transport. Trucking faces a persistent driver shortage, and the costs of human drivers — wages, mandatory rest periods, hours-of-service regulations — represent the largest single operating expense for carriers. A self-driving semi-truck that can run continuously without rest stops represents a transformative efficiency gain.

**Aurora Innovation** has moved furthest toward commercial reality. In May 2025, Aurora became the first company to operate a commercial driverless trucking service with heavy-duty Class 8 trucks on public roads, running regular freight between Dallas and Houston with no human in the cab. By early 2026, Aurora had surpassed 250,000 driverless miles across a network of routes in the Texas Sun Belt, with a reported safety record of zero Aurora Driver-attributed collisions. A nuance worth noting: some trucks have carried a passive observer at certain partners' request — not operating the vehicle, but present — and Aurora's next-generation hardware, planned for mid-2026, is designed to eliminate even that. Aurora is, by a significant margin, the most advanced commercial deployment in autonomous trucking.

Other companies are at earlier stages of development and testing. **Kodiak Robotics** is conducting autonomous freight operations in the Sun Belt. **Torc Robotics**, acquired by Daimler Truck, is developing systems for integration into Freightliner vehicles. **Gatik** focuses on a narrower problem — short, fixed-route "middle mile" logistics between warehouses and distribution centers — arguing that constrained, repeatable routes are more tractable than open-ended highway driving.

The technical challenges of trucking differ meaningfully from those of robotaxis. Highway driving at sustained speeds is in some respects simpler than urban navigation — fewer pedestrians, fewer intersections, more predictable behavior from other vehicles — but a loaded semi-truck weighing 80,000 pounds has braking distances and handling characteristics that demand exceptional prediction and planning horizons. The consequences of a perception failure at highway speed are severe.

A common near-term deployment model is **"driver-out" on the highway, driver-in at terminals**: a human driver handles the complex urban pickup and delivery legs, while the autonomous system manages the highway segment. This approach sidesteps the hardest parts of the problem while capturing a significant fraction of the efficiency gains. Aurora's current operations fit this model, with the autonomous system handling the highway corridors between major freight hubs.

---

## 6.11 Safety and the Long Road Ahead

Waymo has published comparative safety analyses showing significant advantages over human-driven vehicles across metrics including injury-causing crashes per mile and crashes involving pedestrians and cyclists. These figures reflect millions of fully driverless miles across multiple cities.

No equivalent independently verified dataset yet exists for Tesla's robotaxi at comparable scale, given its recent and more limited deployment. The coming years will produce the data needed to make meaningful comparisons between the two technical philosophies.

Neither company has solved the problem. Level 5 — full automation under any conditions anywhere — remains a distant goal. The challenge is not the typical driving that both systems handle well; it is the unbounded variety of atypical situations that the physical world generates without warning. Both the modular and end-to-end approaches are ultimately attempts to build systems robust enough to handle that long tail. The question of which approach gets there first, and at what scale, remains genuinely open.

---
