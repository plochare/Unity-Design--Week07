# Unity Design - Week 07

## Agenda

1. [Unity Animator & Mixamo](#Unity-Animator)
2. [Unity Editor AI Tools](#Unity-AI-Tools)
3. [Vuforia AR SDK](#Vuforia-SDK)

---

# 🎬 Unity Animation System & Mixamo Integration

Animating characters brings your Unity projects to life.  
This guide covers **Unity’s Animation System** and provides a **hands-on workflow to import Mixamo animations**.

---

## 📌 What is the Unity Animation System?

The **Unity Animation System** allows you to animate characters and objects using:

- **Keyframe Animation**: Manual animation inside Unity.
- **Imported Animations**: From tools like Mixamo, Blender, or Maya.
- **Animator Controller**: A state machine that manages multiple animations and transitions.

### Key Concepts

| Concept | Description |
|---------|-------------|
| **Animator Component** | Attaches to a GameObject to control animations. |
| **Animation Clip** | A single animation sequence (e.g., walk, run, jump). |
| **Animator Controller** | Organizes animation clips in states and transitions. |
| **Blend Trees** | Smoothly blend between multiple animations based on parameters. |
| **Root Motion** | Moves the GameObject in world space according to the animation. |

---

## ⚙️ Unity Animator Setup

1. **Add Animator Component**
   - Select your character in the **Hierarchy**.
   - Click **Add Component → Animator**.
   - Create or assign an **Animator Controller**.

2. **Open Animator Controller**
   - Double-click the Animator Controller in **Project Window**.
   - Add states by dragging animation clips into the Animator.
   - Define **transitions** between states based on conditions like speed or triggers.

---

## 🌐 Using Mixamo Animations in Unity

**Mixamo** provides free rigged characters and pre-made animations. Follow these steps to integrate Mixamo animations into Unity.

### Step 1: Choose or Upload Character
1. Go to [Mixamo.com](https://www.mixamo.com/).
2. Select a character from the library or upload your own rigged character.

### Step 2: Pick Animations
1. Search for the desired animation (walk, run, jump, attack, etc.).
2. Click the animation to preview it in the Mixamo viewer.

### Step 3: Download Animation
1. Click **Download**.
2. Choose **FBX for Unity**.
3. Set **Pose → T-Pose**.
4. Choose **With Skin** (for full character) or **Without Skin** (if adding only animation).

### Step 4: Import into Unity
1. Drag the downloaded FBX into **Assets** in Unity.
2. Select the FBX file, go to **Rig** tab, and set:
   - **Animation Type → Humanoid**
   - Click **Apply**.
3. Unity automatically generates **Animation Clips** from the FBX.

### Step 5: Configure Animator Controller
1. Open your **Animator Controller**.
2. Drag the imported Animation Clips into the Animator window.
3. Create **transitions** between animations.
   - Example: Idle → Walk → Run
4. Add **parameters**:
   - Float: `Speed` for movement
   - Trigger: `Jump` for jump animation

### Step 6: Enable Root Motion (Optional)
- If the animation moves the character in world space (e.g., walking forward), check **Apply Root Motion** in the Animator.

---

## 🛠️ Controlling Animations via Script

```csharp
using UnityEngine;

public class CharacterController : MonoBehaviour
{
    public Animator animator;

    void Update()
    {
        float move = Input.GetAxis("Vertical");
        animator.SetFloat("Speed", move);

        if (Input.GetButtonDown("Jump"))
        {
            animator.SetTrigger("Jump");
        }
    }
}
```

---

## 📌 Getting Started: Animator Controller
https://learn.unity.com/course/introduction-to-3d-animation-systems/unit/the-animator

---

# Unity Editor AI Tools 🤖✨

AI is rapidly transforming the way we create games, and Unity Editor AI tools are here to **accelerate prototyping, automate repetitive tasks, and enhance creativity**.

---

## 📌 What Are Unity Editor AI Tools?
Unity Editor AI tools integrate artificial intelligence into the Unity Editor to help developers:
- 🖌 **Generate assets** (textures, sprites, 3D models).
- 🛠 **Automate code snippets** (C# scripting with AI assistance).
- 🎨 **Assist level design** (AI terrain sculpting, scene layout).
- ⚡ **Accelerate iteration** (dialogue generation, testing bots).
- 🧪 **Prototype gameplay ideas** faster.

Some AI tools are **Unity Official** (like Unity Muse), while others come from **community packages** or **third-party services**.

---

## 📥 Unity AI Tutorial

https://learn.unity.com/course/prototype-a-scene-with-unity-ai/tutorial/set-up-your-project-with-unity-ai#688a29feedbc2a084aceb988

This tutorial as a series of short tutorials, each focused on a specific Unity AI capability, in the following order:

* Unity AI Assistant: A built-in tool that helps you build, modify, and script your project using text-based commands. You’ll use it to set up your scene, generate lighting, and write scripts directly in the Editor.

* Animation Generator: Creates humanoid animations from a prompt. You’ll generate animations like idle or dance motions and apply them to your character.
* Texture Generator: Produces 2D textures to use as backgrounds or surface effects. You’ll apply these textures to create a custom backdrop for your scene.
* Material Generator: Builds physically-based materials for 3D surfaces. You’ll create and apply materials to give your ground a polished, tileable surface.
* Sprite Generator: Outputs 2D images ideal for UI icons or decals. You’ll generate a character avatar sprite and use it in your UI.
* Sound Generator: Generates ambient sounds and effects. You’ll add background music and randomized sound effects to bring your scene to life.

At the end of this tutorial, you’ll learn best practices for writing effective prompts and integrating the generated assets directly into your project. have a working game prototype and the confidence to use Unity AI to streamline your future development efforts.


---

## ✅ Best Practices

* Treat AI outputs as **starting points**, not finished products.
* Keep **version control** active (AI changes can be large).
* Use AI for **rapid iteration**, but refine manually for performance/quality.
* Test generated code for **performance + security**.

---

# Unity Vuforia SDK 🔍✨

Vuforia is a leading **Augmented Reality (AR) SDK** for Unity that allows developers to recognize images, objects, and environments, then overlay interactive 3D content. It’s widely used for AR apps in education, retail, training, and entertainment.

---

## 🎯 What is Vuforia?
Vuforia is an **AR engine** that integrates with Unity to provide:
- 📷 **Image Target Recognition** → Detect and augment 2D images.  
- 🛠 **Model Target Tracking** → Recognize 3D objects.  
- 🌍 **Ground Plane** → Place AR objects on real-world surfaces.  
- 🎭 **VUMarks** → Custom markers (like QR codes but stylized).  
- 🕹 **Virtual Buttons** → Trigger actions with physical marker interactions.  
- 🧩 **Multi-targets** → Track multiple objects at once.  

---

## 🛠 Requirements
- Unity **2021 LTS or newer**.  
- [Vuforia Engine SDK](https://developer.vuforia.com/downloads/sdk) installed in Unity.  
- A supported device (Android/iOS) with a working camera.  
- [Vuforia Developer Account](https://developer.vuforia.com/) (for license keys).  

---

## 📥 Installation

1. **Enable Vuforia in Unity**  
   - Go to: `Edit → Project Settings → Player → XR Settings`.  
   - Enable **Vuforia Augmented Reality Support**.  

2. **Get a License Key**  
   - Sign up at [Vuforia Developer Portal](https://developer.vuforia.com/).  
   - Create a new project → Copy your **App License Key**.  
   - Paste it into: `Vuforia Configuration → App License Key`.  

3. **Import Vuforia SDK**  
   - Via Unity **Package Manager** or `.unitypackage` download from the Vuforia portal.  

---

## 🚀 Quick Start Tutorial

### 1. Setup AR Camera
- Delete the default Unity **Main Camera**.  
- Add a **Vuforia AR Camera** (GameObject → Vuforia Engine → AR Camera).  
- In **AR Camera Inspector**, paste your License Key.  

### 2. Add an Image Target
1. Go to [Vuforia Target Manager](https://developer.vuforia.com/target-manager).  
2. Upload a reference image → Generate a **Database**.  
3. Download the `.unitypackage` and import into Unity.  
4. In Unity:  
   - Add **GameObject → Vuforia Engine → Image Target**.  
   - Assign your imported database + image.  

### 3. Place 3D Content
- Drag a 3D model (e.g., Cube, Character prefab) as a **child of the Image Target**.  
- When the target is detected via camera, the object appears on top of it.  

### 4. Build & Test
- Switch platform: **Android/iOS**.  
- Build & run on a device.  
- Point your camera at the image target → Watch your AR content appear.  

---

## 🧩 Example Script: Rotate Object on Target
```csharp
using UnityEngine;
using Vuforia;

public class RotateOnTarget : MonoBehaviour, ITrackableEventHandler
{
    private TrackableBehaviour trackable;

    void Start()
    {
        trackable = GetComponent<TrackableBehaviour>();
        if (trackable) trackable.RegisterTrackableEventHandler(this);
    }

    public void OnTrackableStateChanged(
        TrackableBehaviour.Status prev, TrackableBehaviour.Status newStatus)
    {
        if (newStatus == TrackableBehaviour.Status.DETECTED ||
            newStatus == TrackableBehaviour.Status.TRACKED)
        {
            // Target found → Start rotating
            StartCoroutine(Rotate());
        }
    }

    private System.Collections.IEnumerator Rotate()
    {
        while (true)
        {
            transform.Rotate(Vector3.up * 50 * Time.deltaTime);
            yield return null;
        }
    }
}
````

✅ This script rotates a 3D object whenever the target image is detected.

---

## ⚡ Advanced Features

* **Ground Plane** → Place objects on horizontal surfaces without markers.
* **Model Targets** → Recognize and augment real 3D products.
* **VUMarks** → Brandable AR markers (customized QR-like codes).
* **Virtual Buttons** → Add interactivity by defining button zones on targets.

---

## 💡 Best Practices

* Use **high-contrast, non-repetitive images** for targets.
* Test target ratings in the Vuforia Target Manager (⭐ stronger = better).
* Optimize 3D assets (low poly, compressed textures) for mobile performance.
* Handle lost tracking gracefully (fade or pause AR content).
* Always test on real devices — AR is hardware dependent.

---
