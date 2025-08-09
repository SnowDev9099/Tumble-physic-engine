# Tumble-physic-engine
the SDK for making mods for Ape Sprint VR in the sandbox physics mode.


# NPC System for Unity 6 — Modding & Setup Guide

## Overview
This system provides a fully procedural NPC framework for a modding SDK for Ape Sprint.

### Features
- Procedural walking using IK (no animation clips needed)
- Head, arm, and spine tracking
- NavMeshAgent-based movement
- Sight & hearing-based perception
- VR physics interaction (push, grab, punch)
- Active ragdoll blending for hits & recovery
- Fully modular — add or swap AI states easily

---

## Folder Structure
```
Assets/
  Scripts/
    NPC/
      NPCController.cs
      NPCPerception.cs
      ProceduralWalker.cs
      ProceduralRig.cs
      NPCInteraction.cs
      NPCRagdoll.cs
      NPCHealth.cs
      VRHandInteractor.cs
      NPCSpawner.cs
```
---

## Creating a New NPC Prefab
1. **Create Root Object**
   - Empty GameObject → name `NPC_<Name>`
   - Add: CapsuleCollider, Rigidbody, NavMeshAgent
   - Freeze Rigidbody rotation X/Z

2. **Add Scripts**
   - NPCController
   - NPCPerception
   - ProceduralWalker
   - ProceduralRig
   - NPCInteraction
   - NPCHealth
   - NPCRagdoll

3. **Add Model**
   - Child your humanoid mesh under the root
   - Add Animator (no Controller needed)

4. **Rig Setup**
   - Add Rig Builder to NPC root
   - Create Rigs for head look, arm reach, and legs
   - Assign targets in ProceduralRig script

5. **NavMesh**
   - Place patrol points in scene
   - Assign to NPCController
   - Bake NavMesh

---

## Modding Workflow

### Adding New AI States
- Inherit from `NPCController`
- Override `UpdateState()` and `HandleState()` methods
- Example: `NPCSniper` could add a "TakeCover" state

### Custom Models
- Ensure humanoid bone structure matches Unity's Humanoid rig
- Reassign IK targets in ProceduralRig

### Custom Attacks
- Add new methods in `NPCController`
- Use `ProceduralRig` to move arms/weapons toward targets

### Mod Hooks
- Events in `NPCPerception`: `OnPlayerSeen`, `OnSoundHeard`
- Events in `NPCHealth`: `OnDeath`, `OnDamageTaken`
- Subscribe to these in your mod to trigger effects

---

## VR Interaction
- Attach `VRHandInteractor` to VR hand GameObjects
- Punch: Apply impulse to NPC rigidbody
- Grab: Parent NPC limb to hand temporarily

---

## Best Practices for Modders
- Do not modify core scripts — create extensions
- Keep procedural tuning in separate ScriptableObjects
- Test with placeholder models before releasing

---
