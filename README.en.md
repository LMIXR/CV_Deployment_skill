<p align="center">
  <img src="docs/assets/cv-deployment-cover.png" alt="a real CV Deployment skill — environment setup, dependency builds, video integration, and service deployment. Engineering experience from LMIXR/helpfile." width="100%">
</p>

<h1 align="center">a real CV Deployment skill</h1>

<p align="center"><strong>Practical engineering experience for deploying computer vision applications.</strong></p>

<p align="center">
  <a href="README.md">简体中文</a> · <strong>English</strong>
</p>

<p align="center">
  Help agents set up environments, build dependencies, connect video sources, and deploy applications.
</p>

<p align="center">
  <a href="#getting-started">Getting started</a> ·
  <a href="#what-it-covers">What it covers</a> ·
  <a href="cv-deployment-skills/cv-deploy/SKILL.md">Read the skill</a> ·
  <a href="https://github.com/LMIXR/helpfile">Experience source: helpfile</a>
</p>

---

## From engineering experience to agent action

**The engineering experience in this project comes from [LMIXR/helpfile](https://github.com/LMIXR/helpfile).**

helpfile documents environment setup, dependency builds, video integration, and deployment work for computer vision applications. This project organizes that experience into `$cv-deploy`: an agent identifies the target platform and project constraints, reads the relevant guidance, chooses an approach, and carries out the authorized work.

The skill preserves historical versions, applicable conditions, and troubleshooting clues. When the operating system, architecture, or dependencies differ, it guides the agent to assess whether the experience applies before preparing commands and configuration for the current project.

## What it covers

| Stage | Typical tasks | Guide |
| --- | --- | --- |
| **01 · Environment** | Ubuntu / Jetson, NVIDIA, CUDA, networking, and offline installation | [Environments and platforms](cv-deployment-skills/cv-deploy/references/platforms.md) |
| **02 · Build** | OpenCV, Qt, inference frameworks, C++ libraries, Python, and ABI compatibility | [Building dependencies](cv-deployment-skills/cv-deploy/references/build.md) |
| **03 · Video** | FFmpeg, GStreamer, RTSP, ONVIF, and GB28181 | [Video integration](cv-deployment-skills/cv-deploy/references/video.md) |
| **04 · Deploy** | Packaging shared libraries and plugins, systemd, Windows services, and Docker | [Packaging and deployment](cv-deployment-skills/cv-deploy/references/deployment.md) |
| **Supporting services** | MySQL, MongoDB, Redis, MinIO, Kafka, and Tomcat | [Data and messaging services](cv-deployment-skills/cv-deploy/references/services.md) |
| **Supporting tools** | Ansible, Jenkins, Jitsi, mobile tooling, and other utilities | [Tooling guide](cv-deployment-skills/cv-deploy/references/tools.md) |

The material covers **Ubuntu, CentOS, Windows, macOS, Jetson, Raspberry Pi, and RK3399**, along with selected Android / iOS tooling. Coverage varies by platform; the guides explain the scope of the available experience.

The project overview is available in Chinese and English. The skill instructions and reference guides are currently written in Chinese.

## Getting started

### Use it in this repository

The skill is installed at [`.agents/skills/cv-deploy/`](.agents/skills/cv-deploy/SKILL.md). Open this repository in an agent that supports this directory and invoke it:

```text
$cv-deploy Build the OpenCV and FFmpeg dependencies this project needs on Ubuntu, using its existing CMake configuration.
```

You can also start with a specific problem:

```text
$cv-deploy Diagnose why RTSP connects on this Jetson but video decoding fails. Keep the current JetPack version.
$cv-deploy Build the Windows dependencies with the project's MSVC and Qt kit, then prepare the release directory.
$cv-deploy Set up the existing WVP and ZLMediaKit applications as services, preserving their ports and data directories.
$cv-deploy Prepare only an offline deployment plan and configuration files. Do not install or run validation in this task.
```

### Install it in another project

Download this repository, then run the following from the **target project's root directory**, replacing the repository path:

```sh
mkdir -p .agents/skills
cp -R /path/to/CV_Deployment_skill/cv-deployment-skills/cv-deploy .agents/skills/
```

If the target project already has a skill with the same name, compare and merge any local changes first. For other agents, place the entire `cv-deploy` directory in their supported skill location, or have them read `SKILL.md` directly. The reference guides ship with the skill and can be read offline.

## Where the experience comes from

- **Original engineering notes: [LMIXR/helpfile](https://github.com/LMIXR/helpfile).**
- The [source index](cv-deployment-skills/cv-deploy/references/source-index.md) contains **119 links to engineering source files**, including the original notes, scripts, and configuration.
- Personal paths, addresses, and passwords from the original material are not used as default configuration. Historical version combinations remain as clues to applicability.

This version packages the collected experience as a skill. It has not undergone runtime acceptance testing across platforms. The scope of execution and validation depends on the task.

## Repository structure

```text
.agents/skills/
├── cv-deploy/                 Project installation
└── canvas-design/             Tool used to design the project cover
cv-deployment-skills/
├── README.md                  Maintenance notes
└── cv-deploy/                 Skill source and reference guides
docs/
├── assets/                    GitHub cover
└── design/                    Design philosophy and attribution
```

After updating `cv-deployment-skills/cv-deploy/`, sync the changes to the project installation. Contributions based on real deployment work are welcome through [Issues](https://github.com/LMIXR/CV_Deployment_skill/issues). Include the platform, versions, symptoms, and relevant logs so the experience can become reusable guidance.
