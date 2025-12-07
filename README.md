# Intelligent Meeting Automation with n8n

[![standard-readme compliant](https://img.shields.io/badge/readme%20style-standard-brightgreen.svg?style=flat-square)](https://github.com/RichardLitt/standard-readme)

An intelligent meeting assistant that automatically processes meeting transcriptions, generates structured summaries, assigns tasks, and sends email notifications using n8n workflows and AI.

This repository contains a complete implementation and documentation for an **intelligent meeting automation agent** designed for sprint planning and daily standup meetings. The project leverages n8n for workflow automation, Google Gemini for natural language processing, and integrates with Google Docs, Google Drive, and Gmail for input and output.

## Table of Contents

- [Background](#background)
- [Install](#install)
- [Usage](#usage)
  - [Workflow Overview](#workflow-overview)
  - [Demo Video](#demo-video)
- [Contributors](#contributors)
- [License](#license)

## Background

This project was developed at **Escuela Colombiana de Ingeniería Julio Garavito** as part of the **HAUT_M: Hyperautomation** course. It aims to create an intelligent meeting assistant capable of:

- Summarizing meeting discussions
- Extracting tasks and assigning responsible parties
- Estimating tentative deadlines
- Sending automatic email summaries to stakeholders

The main motivation was to explore **intelligent automation** and demonstrate how tools like n8n can integrate multiple services to improve team productivity. By using a **low-code/no-code workflow automation platform**, the team was able to quickly build a functional MVP while iterating over improvements.

Key technologies:

- **n8n**: Workflow automation platform (open-source, low-code, autohosted)
- **Google Gemini**: AI model for text summarization and task extraction
- **Google Docs / Drive / Gmail**: Integration for meeting transcription input and email output

## Install

This project is implemented with **n8n**, which can be deployed locally or in the cloud. Follow the official n8n installation guide:

- [n8n Quickstart](https://docs.n8n.io/getting-started/installation/)

Basic Docker installation example:

```bash
docker run -it --rm \
    --name n8n \
    -p 5678:5678 \
    -v ~/.n8n:/home/node/.n8n \
    n8nio/n8n
```

After installation, import the workflow JSON file provided in this repository to start the automation.

## Usage

The agent workflow is designed to **process meeting transcriptions from multiple sources, extract actionable insights, and distribute structured summaries via email**.

### Workflow Overview

The automation workflow consists of **three main stages**:

1. **Inputs**

   - **Bluedot Webhook**: Receives real-time meeting transcriptions from external services
   - **Google Drive Trigger**: Detects new files containing transcriptions
   - **Form Submission**: Captures meeting metadata and links to documents

2. **Processing**

   - **Access & Read Text**: Extracts raw transcription text
   - **Format Webhook Transcription**: Cleans and organizes text for AI processing
   - **Process with LLM (Gemini)**: Summarizes meeting, extracts tasks, assigns responsibilities, and estimates deadlines
   - **Centralize Triggers Data**: Combines inputs from all sources
   - **JSON Parser**: Structures AI output into JSON
   - **Convert Markdown to HTML**: Prepares email-ready content

3. **Outputs**

   - **Setup Email Recipients**: Defines stakeholders
   - **Send Message**: Delivers structured summary via email
   - **No Operation**: Ends workflow when no further actions are required

**Prompt example for Gemini AI**:

```
You are a professional meeting assistant. Analyze the transcript and produce a structured output with:
- Meeting Summary
- Action Items (tasks)
- Assigned Responsible(s)
- Tentative Due Dates
Format output in Markdown for HTML conversion. Assign tasks if missing and estimate deadlines.
```

## Demo Video

Here is a demonstration of the intelligent meeting automation workflow implemented in n8n:

<video width="720" height="480" controls>
    <source src="docs/media/meeting_workflow_demo.webm" type="video/webm">
    Your browser does not support the video tag.
</video>

## Contributors

- [Jcro15](https://github.com/Jcro15) - Juan Camilo Rojas Ortiz
- [lrvalencia](https://www.linkedin.com/in/lrvalencia/) - Luiggi Valencia Vélez
- [LePeanutButter](https://github.com/LePeanutButter) - Santiago Botero

## License

[MIT](LICENSE) © Juan Camilo Rojas Ortiz, Luiggi Valencia Vélez, Santiago Botero García

---

This **README** follows the Standard Readme specification.
