---
layout: about
title: about
permalink: /
subtitle: <a href='https://www.eng.cam.ac.uk/'>Department of Engineering, University of Cambridge</a>.

profile:
  align: right
  image: prof_pic.jpeg
  address: >
    <p>Cambridge, United Kingdom</p>
    <p>Email: yz892@cam.ac.uk</p>
    <p><a href="/assets/pdf/Yi_Zhang_CV.pdf">Link to CV</a></p>

news: false
selected_papers: false
social: true  # includes social icons at the bottom of the page
---
PhD Candidate in Agri-Food Robotics at the [University of Cambridge](https://www.cam.ac.uk/), supervised by [Prof. Fulvio Forni](https://sites.google.com/site/fulvioforni/) and funded by the [AgriFoRwArdS CDT](https://agriforwards-cdt.blogs.lincoln.ac.uk/) and [RT Corporation](https://rt-net.jp/). My research focuses on physics-based, interaction-driven robot control for contact-rich manipulation, with an emphasis on robustness, interpretability, and safe physical interaction.

Before Cambridge, I completed an MSc in Robotics and Autonomous Systems at the University of Lincoln, where I worked on controller-based reinforcement learning for robotic manipulation. I received my BEng in Mechanical Engineering from [Osaka University](https://www.osaka-u.ac.jp/en), where I developed tactile-feedback-based cooperative object transportation with mobile robots equipped with flexible tactile sensors under the supervision of [Prof. Yuichiro Sueoka](https://sueokalab.com/) and [Prof. Koichi Osuka](https://researchmap.jp/osuka-koichi). I also spent a year at [UC Berkeley](https://www.berkeley.edu/) as an exchange student and research assistant, working on autonomous driving interaction prediction as well as combustion modelling and experimentation. 

My research interests include robotic manipulation, control theory, human-robot interaction, tactile sensing, and distributed robotic systems.

## Projects

### Distributed virtual model control for human-robot collaboration
Developed a decentralized, agent-agnostic control framework for shared workspaces with humans and robots. Introduced force-based deadlock detection and negotiation, demonstrating scalability to multiple humans and robots without changing the controller structure.

<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 720px; margin: 1rem 0 1.25rem;">
  <iframe
    src="https://www.youtube.com/embed/klX4RPFnotc"
    title="Distributed virtual model control for human-robot collaboration"
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen>
  </iframe>
</div>

Zhang, Y., Faris, O., Sirithunge, C., Chu, K.-F., Iida, F., Forni, F. "Distributed Virtual Model Control for Scalable Human-Robot Interaction in Shared Workspace." ICRA 2026 (IEEE International Conference on Robotics and Automation). [paper link](https://arxiv.org/abs/2602.17415)

### Robust robotic cutting via virtual model control
Designed a virtual-mechanism-based controller for rocking chop motions without explicit trajectory planning, using controlled switching and regulated energy injection to produce stable periodic cutting. Demonstrated robust cutting across vegetables, knife geometries, cutting-board heights, and robot platforms with the same controller structure.

<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 720px; margin: 1rem 0 1.25rem;">
  <iframe
    src="https://www.youtube.com/embed/67v-U4gp9_k"
    title="Robust robotic cutting via virtual model control"
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen>
  </iframe>
</div>

Zhang, Y., Iida, F., Forni, F. "Periodic robust robotic rock chop via virtual model control." Under review for IJRR, 2025. [paper link](https://arxiv.org/abs/2508.02604)

### Compliant reaching under uncertainties
Developed virtual model controllers that unify motion planning and control for safe reaching in cluttered, partially known environments. Validated virtual mechanism designs on a 17-DoF upper-body humanoid robot and showed predictable and safe behavior under known and unknown obstacles.

<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 720px; margin: 1rem 0 1.25rem;">
  <iframe
    src="https://www.youtube.com/embed/rZoGYubyb7E"
    title="Compliant reaching under uncertainties"
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen>
  </iframe>
</div>

Zhang, Y., Larby, D., Iida, F., Forni, F. "Virtual Model Control for Compliant Reaching under Uncertainties." IROS 2024 (IEEE/RSJ International Conference on Intelligent Robots and Systems). [paper link](https://ieeexplore.ieee.org/document/10801592)


### Passive data-driven iFIR control for robotics
Developed a passive, data-driven velocity controller learned from a few minutes of probing data using VRFT. Experimental validation on the Franka Research 3 showed up to 74.5% reduction in tracking error over an optimized PID baseline and recovery after dynamics changes through re-learning.

<div class="row">
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.html path="assets/img/research/ifir_robot_setup.png" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.html path="assets/img/research/ifir_robotics.png" class="img-fluid rounded z-depth-1" %}
  </div>
</div>

Zhang, Y., Wang, Z., Forni, F. "Passive iFIR filters for data-driven velocity control in robotics." Under review, 2026. [paper link](https://arxiv.org/abs/2603.29882)

Related paper: Wang, Z., Zhang, Y., Forni, F. "Dissipative iFIR filters for data-driven design." European Journal of Control, 2025. [paper link](https://www.sciencedirect.com/science/article/pii/S0947358025001293)

<!-- ### Event-based variable-stiffness control inspired by neuron models
Explored neuromorphic-inspired virtual mechanisms for explosive and rhythmic motion generation, using state-dependent virtual springs and damping to achieve event-triggered task completion without explicit trajectory generators. Validated on robotic throwing and adaptive drumming tasks.

Video: to be added


### Virtual model control for structured policy
Explored interpretable structured policies for reinforcement learning using virtual model control as the policy backbone.

Video: to be added

Not yet listed as published or under review on this site -->

### Controller-based reinforcement learning in robotic manipulation
Studied controller-based reinforcement learning during my MSc at the University of Lincoln, combining a roughly tuned controller with TD3 to improve learning efficiency.

Presented at TAROS 2023 / Joint Robotics CDT Annual Conference 2023

### Cooperative object transportation with flexible tactile sensors
Developed tactile-feedback-based cooperative object transportation with mobile robots equipped with flexible tactile sensors. This work started from my undergraduate thesis and focused on decentralized cooperative transport with compliant sensing.

<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 720px; margin: 1rem 0 1.25rem;">
  <iframe
    src="https://www.youtube.com/embed/NBYaup4oivA"
    title="Cooperative object transportation with flexible tactile sensors"
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen>
  </iframe>
</div>

Zhang, Y., Sueoka, Y., Ishihara, H., Kawasetsu, T., Osuka, K. "A Decentralized Approach to Cooperative Object Transportation with Robots Equipped with Flexible Tactile Sensors." DARS 2022 (16th International Symposium on Distributed Autonomous Robotic Systems). [paper link](https://link.springer.com/chapter/10.1007/978-3-031-51497-5_8)

Zhang, Y., Sueoka, Y., Ishihara, H., Kawasetsu, T., Osuka, K. "A Decentralized Approach to Cooperative Object Transportation with Robots Equipped with Flexible Tactile Sensors." RSJ 2021 (39th annual conference of the Robotics Society of Japan).

### Intern at HCI Co., Ltd.
During my internship at HCI Co., Ltd., led the development of a robot hand that can play rock-paper-scissors with people.
Trained FANUC robots to complete sequences of tasks with different hands and tools, and worked on programming and electrical wiring with FANUC, Mitsubishi, and Yaskawa systems.

{% include figure.html path="assets/img/intern/HCI.JPG" class="img-fluid rounded z-depth-1" %}

### Autonomous driving interaction prediction
Worked at UC Berkeley on interaction prediction for autonomous driving, including debugging and optimizing multi-vehicle prediction code, improving interaction identification, and analyzing challenge results based on the INTERACTION dataset.

{% include figure.html path="assets/img/research/example_prediction_challenge.png" class="img-fluid rounded z-depth-1" %}

### Combustion modelling and experimentation
Worked at UC Berkeley on combustion-related projects including argon power cycle experiments, HCCI combustion experiments under different operating conditions, data analysis in MATLAB, and combustion simulation using CONVERGE.
