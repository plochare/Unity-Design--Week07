# Unity Design - Week 07

## Agenda

1. [Tweening with DOTween](#DO-Tween)  
2. [Unity Animator & Mixamo](#Unity-Animator)
3. [Unity Editor AI Tools](#Unity-AI-Tools)

# 🎬 Unity DOTween

Tweening (short for *in-betweening*) lets you smoothly animate values over time, such as movement, rotation, scale, UI transitions, or color changes.

**[DOTween](http://dotween.demigiant.com/)** is a fast, efficient, full-featured tweening engine for Unity. It’s widely used in professional projects because of its flexibility and performance.

---

## 🚀 What is DOTween?

DOTween provides:

* ✨ **Powerful animations** for any value, not just transforms.
* 🔗 **Sequences** – chain multiple tweens in order.
* 🎛️ **Ease of use** – simple one-liners to animate properties.
* ⚡ **High performance** – optimized for mobile and consoles.
* 🛠️ **Extensibility** – works with custom variables, UI, shaders, and more.

---

## 📦 Installation

### Option 1: Unity Asset Store

1. Open **Unity Asset Store** inside the Unity Editor.
2. Search for **DOTween** and install the free version (or Pro for extra features).

### Option 2: Package from Website

1. Download DOTween from [dotween.demigiant.com](http://dotween.demigiant.com/).
2. Import the `.unitypackage` into your Unity project.
3. Run **DOTween Utility Panel** via `Tools > Demigiant > DOTween Utility Panel` to set up.

---

## 💡 Basic Usage

Here’s how to move a GameObject smoothly across the screen:

```csharp
using UnityEngine;
using DG.Tweening; // DOTween namespace

public class DoTweenExample : MonoBehaviour
{
    void Start()
    {
        // Move the object to position (5, 2, 0) over 2 seconds
        transform.DOMove(new Vector3(5f, 2f, 0f), 2f);
    }
}
```

---

## 🛠️ DOTween API Overview

### 1. Move Object

```csharp
transform.DOMove(Vector3 targetPosition, float duration);
```

Moves a GameObject to the target position.

---

### 2. Rotate Object

```csharp
transform.DORotate(new Vector3(0, 180, 0), 2f);
```

Rotates a GameObject smoothly.

---

### 3. Scale Object

```csharp
transform.DOScale(Vector3.one * 2f, 1f);
```

Doubles the size of the object in 1 second.

---

### 4. Color Tween

```csharp
spriteRenderer.DOColor(Color.red, 1.5f);
```

Tweens a sprite’s color over 1.5 seconds.

---

### 5. UI Tweening

```csharp
myText.DOFade(0f, 2f);  // fade out text
myImage.DOFillAmount(1f, 3f); // fill radial image
```

---

### 6. Sequences

Chain multiple animations together:

```csharp
Sequence mySequence = DOTween.Sequence();
mySequence.Append(transform.DOMoveX(3, 1f))
          .Append(transform.DOScale(Vector3.one * 2, 0.5f))
          .Append(transform.DORotate(new Vector3(0, 180, 0), 1f))
          .OnComplete(() => Debug.Log("Sequence Finished!"));
```

---

### 7. Looping

```csharp
transform.DOMoveY(3f, 1f).SetLoops(-1, LoopType.Yoyo);
```

Makes the object bounce up and down forever.

---

### 8. Callbacks

```csharp
transform.DOMoveX(5, 2f).OnComplete(() => Debug.Log("Done!"));
```

---

## 🎮 Tutorial: Bouncy UI Button

Let’s animate a UI button to “bounce” when clicked:

```csharp
using UnityEngine;
using UnityEngine.UI;
using DG.Tweening;

public class DoTweenButton : MonoBehaviour
{
    public Button myButton;

    void Start()
    {
        myButton.onClick.AddListener(() =>
        {
            myButton.transform.DOScale(Vector3.one * 1.2f, 0.2f)
                .SetEase(Ease.OutBack)
                .OnComplete(() =>
                {
                    myButton.transform.DOScale(Vector3.one, 0.2f).SetEase(Ease.InBack);
                });
        });
    }
}
```

✅ Result: The button pops when clicked with a smooth easing curve.

---

## 📸 Example Scenarios

* Smooth **camera transitions**
* UI elements sliding in/out
* Looping **background animations**
* Complex cutscene animations using **Sequences**
* Sprite flashing or color transitions

---

## 📚 Resources

* [DOTween Official Documentation](http://dotween.demigiant.com/documentation.php)
* [DOTween Pro](http://dotween.demigiant.com/pro.php) – extended features for UI and visual tools
  
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
