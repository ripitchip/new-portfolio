---
date: '2025-07-30T21:22:33-04:00'
draft: false
title: 'Presentation of lazygit'
tags:
  - tools
categories:
  - blog
---
## Why do I use lazygit
I use Lazygit in order to have a gui for my git folder management.
It is usefull to see modifications commits ect.
You can manage multiple aspect of yoiur git project:
- commits
- patch selection (selecting line to add to commits)
- branches
- history
## What is really cool?
### GitMoji
Fiorstly you can use gitmoji, quite usefull on commits
![GitMoji example](/images/posts/lazygit/gitmoji.png)
```yaml
customCommands:
  - key: "<c-c>"
    context: "files"
    description: "commit files with format"
    prompts:
      - type: "menu"
        title: "What kind of commit type is it?"
        key: "Type"
        options:
          - name: ":ambulance:"
            description: "(fix) 🚑 Fatal bug fix"
            value: ":ambulance: fix:"
          - name: ":bug:"
            description: "(fix) 🐛 Bug fix"
            value: ":bug: fix:"
          - name: ":+1:"
            description: "(fix) 👍 Functional improvements and corrections"
            value: ":+1: fix:"
          - name: ":cop:"
            description: "(fix) 👮 Security related fixes"
            value: ":cop: fix:"
          - name: ":tada"
            description: "(feat) 🎉 Big feature addition"
            value: ":tada: feat:"
          - name: ":sparkles:"
            description: "(feat) ✨ Partial function addition"
            value: ":sparkles: feat:"
          - name: ":up:"
            description: "(feat) 🆙 Update of dependent packages, etc"
            value: ":up: feat:"
          - name: ":memo:"
            description: "(docs) 📝 Add or modify documents"
            value: ":memo: docs:"
          - name: ":bulb"
            description: "(docs) 💡 Adding or modifying comments to the source code"
            value: ":bulb: docs:"
          - name: ":art:"
            description: "(style) 🎨 Layout related fixes"
            value: ":art: style:"

          - name: ":lipstick:"
            description: "(style) 💄 Lint: Fix errors and code style"
            value: ":lipstick: style:"
          - name: ":recycle:"
            description: "(refactor) ♻️  Refactor"
            value: ":recycle: refactor:"
          - name: ":fire:"
            description: "(refactor) 🔥 Delete code or files"
            value: ":fire: refactor:"
          - name: ":green_heart:"
            description: "(test) 💚 Testing and CI fixes"
            value: ":green_heart: test:"
          - name: ":rocket:"
            description: "(perf) 🚀 Performance improvement"
            value: ":rocket: perf:"
          - name: ":wrench:"
            description: "(chore) 🔧 Modifying the configuration file"
            value: ":wrench: chore:"
          - name: ":building_construction:"
            description: "(chore) 🏗️ Architecture fixes"
            value: ":building_construction: chore:"
          - name: ":construction:"
            description: "(wip) 🚧 Working on"
            value: ":construction: wip:"
      - type: "input"
        title: "Enter the Message"
        key: "Message"
        initialValue: ""
```
### Custom commands
Using Gitmoji with custom commands allows you to create a command that selects the desired Gitmoji and even the desired issue number.
Here is an example:
![Example of a custom command](/images/posts/lazygit/custom.gif)
For this config I first select the correct gitmoji and then the issue.
For that i have a bash command that get all my gitlab issues (based on glab)
```yaml
  - type: "menuFromCommand"
    title: "Which remote repository to push to?"
    key: "Issue"
    command: >-
      bash -c "glab issue list -O json | jq -r 'sort_by(.id) | .[] | \"#\\(.iid) TITLE:\\(.title)\"'"
    filter: '#(?P<id>\d+) TITLE:(?P<title>.*)'
    valueFormat: "{{ .id }}"
    labelFormat: "#{{ .id | bold | cyan }} Title:{{.title | bold | red}}"
  - type: "confirm"
    title: "Commit"
    body: "Commit with the message '{{.Form.Type}} #{{.Form.Issue}} {{.Form.Message}}'. Is this okay?"
command: 'bash -c ''type="{{.Form.Type}}"; message="{{.Form.Message}}"; issue={{.Form.Issue}}; commit_message="$type #$issue $message"; git commit -m "$commit_message"'''
loadingText: "Commiting..."
```