---
title: "Daily Quest: Daily Test"
date: 2026-03-17T16:54:47+01:00
draft: true
author: "XXXX" # Change this in config.toml
tags: ["DailyQuest", "DevOpsJourney", "Kubernetes", "Docker"]
categories: ["Quests"]

# LoveIt specific settings (optional)
# toc: true
# share: false
---

## The Mission

<div class="wow-flavour-text" style="font-style: italic; color: #555; border-left: 3px solid #ccc; padding-left: 10px; margin-bottom: 20px;">
    The local system architect looked stressed. "The pipelines are backing up, and we've got a rogue deployment spawning processes like Troggs! We need someone to get into the cluster and stabilize the load."
</div>

Today's quest is all about restoring order to our Kubernetes environment. It’s not just a technical challenge; it's a test of resolve. I accepted the quest, and my log updated.

---

## Quest Log: Stabilizing the Cluster

{{% wowbox type="objective" title="Objectives" %}}
* [ ] Analyze the output of `kubectl top nodes` to identify the offending workload.
* [ ] Implement Vertical Pod Autoscaling (VPA) on the problematic service.
* [ ] **(Optional/Bonus) Add a resource quota to the `production` namespace to prevent future incidents.**
{{% /wowbox %}}

### Step 1: Cutting Teeth (Identifying the Issue)
The first step of any quest is knowing what you're up against. In my case, I was facing a CPU spike that was bringing nodes to their knees. The architecture might be simple, but the impact was severe.

*Here, I would blog the technical content: commands I used, error messages I encountered, and screenshot of my terminal.*

### Step 2: The Proving Pit (Implementing VPA)
Once I found the problem, the real battle began. I had to configure the VPA. This felt like entering the Proving Pit, as getting the configuration right (the "blessing of the spirits") was critical.

```yaml
# A simple VPA deployment
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
  name: critical-service-vpa
spec:
  targetRef:
    apiVersion: "apps/v1"
    kind: Deployment
    name: critical-service
  updatePolicy:
    updateMode: "Auto"
