
<template>
  <div class="esc-details-container">
    <!-- Header -->
    <div class="project-header">
        <h1 class="title">Custom 4-in-1 Electronic Speed Controller</h1>
        <p class="subtitle">High-Performance ESC for Quadcopter BLDC Motors</p>
        <div class="header-specs">
            <div class="spec-item">
                <Zap class="icon" size="18" />
                <span>4S LiPo • 7A/channel</span>
            </div>
            <div class="spec-item">
                <Cpu class="icon" size="18" />
                <span>STM32F407 • DRV8323RS</span>
            </div>
            <div class="spec-item">
                <Calendar class="icon calendar-icon" size="18" />
                <span>Ongoing since March 5, 2026</span>
            </div>
        </div>
    </div>

    <div class="prose-content">
        <p class="intro-paragraph">
            In the pursuit of pushing the boundaries of UAV performance and embedded systems design, I developed a fully custom 4-in-1 Electronic Speed Controller tailored for high-efficiency quadcopter applications. This project integrates power electronics, real-time firmware, and robust hardware engineering to deliver precise motor control while optimizing for the demanding requirements of modern FPV and autonomous drone platforms.
        </p>

        <!-- Project Overview -->
        <h2 class="section-title">Project Overview & Specifications</h2>
        <p>
            The ESC is engineered as a <strong class="highlight">4-in-1 layout</strong> (four independent ESC channels on a single board) to minimize weight, reduce wiring complexity, and improve thermal distribution in a compact quadcopter frame.
        </p>

        <div class="specs-grid">
            <div>
                <p class="grid-title">Battery</p>
                <p class="grid-content">4S LiPo — 5.2Ah — 35C/60C</p>
            </div>
            <div>
                <p class="grid-title">Motors</p>
                <p class="grid-content">1400KV BLDC • Max efficient current: 7A</p>
            </div>
            <div>
                <p class="grid-title">Key ICs</p>
                <p class="grid-content">MCG4D8N04YHE3-TP • DRV8323RS • STM32F407VET6</p>
            </div>
        </div>

        <p>
            Core components include low <span class="code-text">Rds(on)</span> MOSFETs, a high-performance gate driver with integrated protection, and a powerful Cortex-M4 microcontroller capable of running advanced Field Oriented Control (FOC) or trapezoidal commutation.
        </p>

        <!-- Challenges -->
        <h2 class="section-title">Technical Challenges & Design Philosophy</h2>
        <ul class="challenges-list">
            <li>
                <span>01</span>
                <div>Optimized high-frequency switching with programmable dead-time and adaptive gate drive to maximize efficiency and prevent shoot-through.</div>
            </li>
            <li>
                <span>02</span>
                <div>Precise phase current sensing and robust protection circuitry for reliable operation under propeller strikes and motor stalls.</div>
            </li>
            <li>
                <span>03</span>
                <div>Careful PCB layout with separated power and signal domains, minimized loop inductance, and strategic thermal vias.</div>
            </li>
            <li>
                <span>04</span>
                <div>Real-time firmware on STM32F407 utilizing DMA, advanced timers, and sensorless back-EMF detection.</div>
            </li>
        </ul>

        <!-- Development -->
        <h2 class="section-title">Development Process</h2>
        <p>
            From detailed schematic design and component selection through multi-layer PCB layout to firmware to be developed in C/C++, every stage will be validated with oscilloscope measurements, thermal profiling, and real-world flight testing on a custom quadcopter platform.
            <br><br>
        </p>
        <p>
          I began with detailed schematic capture and component selection based on worst-case thermal and electrical analysis. PCB layout followed high-current best practices, including Kelvin sensing for accurate voltage feedback and minimized loop inductance in the power stage.
        </p>
        <p>
          Firmware is to developed in C/C++ using the STM32 HAL and CMSIS libraries, with custom implementations of motor control algorithms. Extensive bench testing will involve oscilloscope validation of gate drive waveforms, current waveforms, and efficiency measurements across the full throttle range. The system will then be integrated into a test quadcopter platform for real-world flight validation, including throttle response, heat profiling under load, and failure-mode testing.
        </p>

        <!-- Outcomes -->
        <h2 class="section-title">Expected Outcomes & Impact</h2>
        <p class="leading-relaxed">
            The resulting 4-in-1 ESC should deliver excellent efficiency, crisp throttle response, and comprehensive protection features. This project provides hardware-firmware co-design exposure — from power electronics and high-current PCB layout to real-time embedded motor control.
        </p>

        <!-- GitHub Link -->
        <div class="github-card">
            <div>
                <p class="github-title">Open Source Project</p>
                <p class="github-subtitle">Fully documented and available on GitHub</p>
            </div>
            <a href="https://github.com/alexWandugu/4in1-ESC-STM32F407-DRV8323" target="_blank" class="github-button">
                <Github class="icon" size="20"/>
                <span>View Repository</span>
            </a>
        </div>

        <div class="footer-note">
            Future iterations planned: higher current capacity, DShot 1200 support, and integrated Blackbox logging.
        </div>
    </div>
</div>
</template>

<script>
import { Zap, Cpu, Github, Calendar } from 'lucide-vue-next';

export default {
  name: 'EscProjectDetails',
  components: {
    Zap,
    Cpu,
    Github,
    Calendar
  }
};
</script>

<style scoped>
.esc-details-container {
    color: var(--text-color);
}

.project-header {
    background: linear-gradient(135deg, #1e2937, #334155);
    border-radius: 16px;
    padding: 2rem;
    text-align: center;
    margin-bottom: 2rem;
}

.title {
    font-size: 2.25rem; /* 36px */
    font-weight: 700;
    color: #ffffff;
    margin-bottom: 0.75rem;
}

.subtitle {
    color: #90b8f3; /* Equivalent to text-blue-400 */
    font-size: 1.125rem; /* 18px */
}

.header-specs {
    display: flex;
    justify-content: center;
    gap: 1.5rem;
    margin-top: 1.5rem;
    font-size: 0.875rem; /* 14px */
    color: #e2e8f0; /* Lighter text for specs */
}

.spec-item {
    display: flex;
    align-items: center;
    gap: 0.5rem;
}

.spec-item .icon {
    color: #facc15; /* amber-400 */
}

.spec-item:last-child .icon {
    color: #34d399; /* emerald-400 */
}

.spec-item .calendar-icon {
    color: #9ca3af; /* neutral-400 */
}

.prose-content {
    max-width: 100%;
}

.intro-paragraph {
    font-size: 1.125rem; /* 18px */
    line-height: 1.7;
    color: var(--secondary-color);
    margin-bottom: 3rem;
}

.section-title {
    font-size: 1.5rem; /* 24px */
    font-weight: 600;
    color: var(--text-color);
    margin-top: 3rem;
    margin-bottom: 1.5rem;
    position: relative;
    padding-bottom: 0.5rem;
}

.section-title:after {
    content: '';
    position: absolute;
    width: 50px;
    height: 3px;
    background: var(--primary-color);
    bottom: 0;
    left: 0;
}

.highlight {
    color: var(--primary-color);
}

.specs-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1.5rem;
    background-color: var(--light-gray);
    border: 1px solid #374151; /* zinc-800 */
    border-radius: 12px;
    padding: 1.75rem;
    margin: 2rem 0;
}

.grid-title {
    font-size: 0.75rem; /* 12px */
    text-transform: uppercase;
    letter-spacing: 0.05em;
    color: var(--secondary-color);
    margin-bottom: 0.25rem;
}

.grid-content {
    font-weight: 500;
    color: var(--text-color);
}

.code-text {
    font-family: 'Courier New', Courier, monospace;
    color: #facc15; /* amber-400 */
    background-color: #1f2937;
    padding: 2px 6px;
    border-radius: 4px;
}

.challenges-list {
    list-style: none;
    padding: 0;
    margin-top: 2rem;
}

.challenges-list li {
    display: flex;
    gap: 1rem;
    align-items: flex-start;
    margin-bottom: 1rem;
}

.challenges-list span {
    color: var(--primary-color);
    font-weight: 700;
    font-size: 1.25rem;
    line-height: 1.4;
}

.leading-relaxed {
    line-height: 1.8;
}

.github-card {
    margin-top: 2.5rem;
    padding: 1.5rem;
    background-color: #1e2937;
    border: 1px solid #4a5568;
    border-radius: 16px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-wrap: wrap;
    gap: 1rem;
}

.github-title {
    color: #34d399; /* emerald-400 */
    font-weight: 500;
}

.github-subtitle {
    font-size: 0.875rem;
    color: var(--secondary-color);
}

.github-button {
    display: inline-flex;
    align-items: center;
    gap: 0.75rem;
    background-color: #ffffff;
    color: #111827; /* zinc-900 */
    padding: 0.75rem 1.5rem;
    border-radius: 12px;
    font-weight: 600;
    text-decoration: none;
    transition: background-color 0.3s ease;
}

.github-button:hover {
    background-color: #90b8f3; /* blue-400 */
}

.footer-note {
    text-align: center;
    font-size: 0.75rem;
    color: var(--secondary-color);
    margin-top: 4rem;
}
</style>
