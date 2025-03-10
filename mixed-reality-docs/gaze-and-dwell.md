---
title: Head-gaze and dwell
description: Overview of the head-gaze and dwell input model
author:  liamartinez
ms.author: liamar
ms.date: 05/13/2019
ms.topic: article
keywords: Mixed Reality, gaze, dwell, interaction, design
---

# Head-gaze and dwell

When hands are occupied with tools and parts, gestures can be tedious or impossible. Voice commands, like gestures, can be unreliable in certain contexts, for example under excessively loud conditions. Additionally, using voice to control computers isn't universally common, but it certainly is gaining steam! Head-gaze and dwell offers the most familiar and easy-to-master mechanism for working heads-up and hands-free on HoloLens. Additionally, head-gaze and dwell is 100% reliable independent of noise interference nor silence constraints in the operating environment.

## Scenarios

Head-gaze and dwell excels in scenarios where a person's hands are busy with other tasks, and voice isn't 100% reliable or available due to environmental or social constraints. A good example is a person wearing a HoloLens to overlay reference information while repairing a car engine. Their hands are busy with tools or supporting their body as they lean into the engine compartment. The garage space is loud, with the constant banging and buzzing of tools, making voice commands difficult. Head-gaze and dwell allows the person using the HoloLens to confidently navigate their reference material without interrupting their workflow. 

## Device support

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><strong>Input model</strong></td>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens (1st gen)</strong></a></td>
        <td><strong>HoloLens 2</strong></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></td>
    </tr>
     <tr>
        <td>Head-gaze and dwell</td>
        <td>✔️ Recommended</td>
        <td>✔️ Recommended</td>
        <td>✔️ Recommended</td>
    </tr>
</table>


## Design principles

**Avoid "Gaze as a weapon"**

Head-gaze and dwell requires visual feedback to be intuitive, but too much feedback can induce anxiety. The feedback should help a user know what they're targeting, but not auto-select it against their intent. Reading text, icons, and labels requires extra consideration to provide a person room to absorb the information before selecting.
	
**Seek Goldilocks speed**
	
Dwell interactions can have different timers based on impact of navigation - more frequently used functions will generally benefit from faster fill times, while more consequential functions may benefit from longer fill times. When using a fill-effect to show these timers, animation curves of the fill color can positively influence a feeling of faster fill times. Consideration should be taken to enable user decision from fast/medium/slow fill speed overrides.
	
**Say no-no to yo-yo effect**

The yo-yo effect is an uncomfortable pattern of head movement that can emerge when the placement of content and head-gaze and dwell controls forces people to constantly look up and down repeatedly. For example, a list nav with the head-gaze and dwell button at the bottom induces a loop of - look down to dwell, look up at results, look down to dwell, etc. This resulting pattern is uncomfortable and should be avoided by placing navigation controls in a centralized location that requires less back-and-forth. Placement of dwell buttons relative to their effects becomes important for comfort.

<br>

---


## UX Guidelines and best practices

### Target sizes
  To be easily accessible, head-gaze and dwell targets need to be large enough to comfortably look at, and hold one's head stable on the target for the prescribed time. We recommend a minimum target size of 2 degrees to achieve the most comfortable experience. 

### Visual feedback

When using a radial fill to represent the dwell timer, start from the center of button. A consistent response is less confusing than all different directions on different buttons. 

  * This rule can be broken though for directional interactions (e.g., nav up/down/left/right, etc.). For example, Microsoft Dynamics 365 Guides makes an exception on NEXT/BACK being left right fills.
  * Consider inverting radial fill from outside, for scenarios like toggling a button off. The inverse feeling of pushing a button is a nice visual pattern to maintain. 

### Progressive disclosure

Progressive disclosure means only showing as much detail as is relevant at each stage of an interaction. For dwell, that means the dwell target is revealed on highlight (e.g., in a list control).

 ### Oversized targets
Dwell region can be larger than inactive icon to make it easier to use, like the Back button in Microsoft Dynamics 365 Guides.

### Prevent flickering with delayed feedback
Use a short delay before starting visual feedback to avoid flickering when someone passes over a dwell target.
* For buttons interacted with frequently, keep the delay very short so the application feels reactive.
* For buttons that are interacted with infrequently, a longer delay can be appropriate to avoid the interface feeling twitchy.


<br>

---

## UI patterns

### High frequency buttons

:::row:::
    :::column:::
        High frequency buttons are buttons that are used commonly throughout an application. A good example of these are the next and back buttons in Microsoft Dynamics 365 Guides.<br>
        <br>
        **Recommendations**<br>
  * High frequency buttons should be large, easier to hit with head-gaze
  * Stay near eye height to avoid ergonomic straining.<br>
        <br>
*Image: Microsoft Dynamics 365 Guides next button*
    :::column-end:::
        :::column:::
       ![Microsoft Dynamics 365 Guides next button](images/GuideNextButton.png)<br>
    :::column-end:::
:::row-end:::

<br>

---


### Low frequency buttons
Low frequency buttons are buttons that are not interacted with as regularly throughout the application. A good example might be a button to access the settings menu, or a button to clear all work.

* Try to keep these buttons out of the way of frequent head-gaze paths to avoid accidental activation. 

<br>

---

### Confirmations

:::row:::
    :::column:::
        When an action has significant impact, like charging money, deleting work, or starting a long process, it is useful to confirm that a person meant to select a button.<br>
        <br>
        **Recommendations**<br>
  * Show selection highlight on main button.
  * Reveal dwell target at same time as selection highlight.
  * For the secondary button, reveal the dwell target on head-gaze.<br>
        <br>
*Image: Microsoft Dynamics 365 Guides confirmation dialog*
    :::column-end:::
        :::column:::
       ![Microsoft Dynamics 365 Guides Confirmation Dialog](images/GuidesConfirmation.png)<br>
    :::column-end:::
:::row-end:::
		
<br>

---

### Toggle buttons
Toggle buttons require some nuanced logic to work properly. When a person dwells on a toggle button and actives it, they need to exit the button and then return to restart the dwell logic. It is important that togglable buttons have a clear active versus inactive state. 

<br>

---

### List views

:::row:::
    :::column:::
        List views present a particular challenge for head-gaze and dwell input. People need to be able to scan the content without feeling like that have to tiptoe around the dwell targets.<br>
        <br>
**Recommendations**<br>
  * Have the entire row highlight when head-gazed but doesn’t begin dwell unless head-gaze is on the specific dwell target.
  * Only show the dwell target when the row is highlighted to cut down on visual noise.
  * Be clear and consistent with the position of dwell targets.
  * Don't show all dwell targets at once to avoid repetitive UI.
  * Re-use the same pattern as often as possible to establish UX familiarity.<br>
        <br>
*Image: Microsoft Dynamics 365 Guides list*
    :::column-end:::
        :::column:::
       ![Microsoft Dynamics 365 Guides list](images/GuidesListView.png)<br>
    :::column-end:::
:::row-end:::

<br>

---
 
 ## See also
* [Direct manipulation with hands](direct-manipulation.md)
* [Point and commit with hands](point-and-commit.md)
* [Instinctual interactions](interaction-fundamentals.md)
* [Head-gaze and commit](gaze-and-commit.md)
* [Voice input](voice-input.md)
