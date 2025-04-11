# Obsidian Vault

A centralized knowledge base and project management system for LLM integration and the Master Control Program (MCP) ecosystem.

## Overview

This vault serves as the central hub for coordinating multiple Local LLM projects and their integration through the MCP client. The structure enables seamless communication and updates between subprojects while maintaining a clear separation between public and private content.

## Structure

- `vault/` - Main Obsidian vault containing all project documentation
  - `BeWhyOrg/` - Public project documentation and planning
    - `BeWhyOrg/InServer/` - Software that runs on the server
      - `BeWhyOrg/InServer/Backend/` - Laravel as API
      - `BeWhyOrg/InServer/Frontend/` - Angular Framework
    - `BeWhyOrg/Local/` - Local project documentation
      - `BeWhyOrg/Local/AI/` - AI and LLM related documentation
        - `BeWhyOrg/Local/AI/MCPs/` - Model Communication Protocols documentation
          - `BeWhyOrg/Local/AI/MCPs/Obsidian-MCP-Actions/` - Obsidian MCP Actions system
    - `Estado` - Where we will have short-cuts and analysis of the Portuguese State
  - `Private/` - Personal notes and sensitive information (git-ignored)
  - `Logs/` - Daily and weekly progress tracking, Where LLM can use as dairy if needed leaving project as it is
    - `Logs/Daily-Logs/` - Daily progress notes and tasks
    - `Logs/Weekly-Logs/` - Weekly progress summaries
    - `Logs/Tasks/` - Detailed logs for specific tasks
  - `Template/` - Standardized templates for consistent documentation
  - `assets/` - Media and resource files

## Purpose

The primary goals of this project are:

1. Coordinate development of local LLM projects
2. Implement MCP client for inter-project communication
3. Maintain organized documentation and knowledge sharing
4. Enable collaborative development while protecting private information

## Getting Started

Clone this repository and open the `vault` folder in Obsidian to access the full project documentation. Note that the `Private` folder is git-ignored to protect sensitive information.
Can reach me at bewhyorg@gmail.com or at join at https://discord.gg/MVSCqR7m
