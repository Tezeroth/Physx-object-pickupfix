# PhysX Object Pickup & Inspection Demo

This project is a web-based 3D interactive environment built with [A-Frame](https://aframe.io/) and the [PhysX](https://github.com/c-frame/physx) physics engine. It demonstrates realistic object pickup, movement, and inspection in a virtual scene, with support for both desktop and mobile controls.

## Features

- **3D Scene with Physics:**
  - Realistic gravity and collision using PhysX.
  - Multiple pickupable objects (box, sphere, cylinder, and a GLTF model).
  - Immersive skybox and textured ground.
- **Object Pickup & Inspection:**
  - Click (desktop) or tap (mobile) to pick up objects.
  - Hold and move objects in front of the camera for inspection.
  - Only one object can be held at a time.
- **Physics Handling:**
  - Physics are temporarily disabled when an object is picked up, then re-enabled when dropped.
  - Touching objects have their physics temporarily removed and restored to prevent collision glitches.
- **Camera Controls:**
  - First-person camera at realistic height (1.6 meters).
  - Pointer lock (desktop) and gyroscope (mobile) support.
- **Mobile Support:**
  - Touch controls and permission handling for device orientation.
- **Loading Overlay:**
  - Loading screen while the physics engine initializes for a smooth experience.

## How Physics and Camera Issues Were Fixed

### 1. Objects Falling Through the Floor
- **Problem:** Objects would sometimes fall through the floor or behave unpredictably when picked up or dropped.
- **Solution:**
  - The ground is a thin, wide `<a-box>` with a static PhysX body (`physx-body="type: static; mass: 0;"`), ensuring reliable collision.
  - When picking up an object, its physics are removed, and after a brief delay, it is set to kinematic mode and attached to the camera. When dropped, physics are re-enabled as a dynamic body, and the object's position/rotation are restored to prevent glitches.
  - Nearby objects have their physics temporarily removed and restored after a short delay to prevent collision bugs during pickup/drop.

### 2. Camera Height and Hovering Objects
- **Problem:** The player camera height was off, or objects appeared to hover above the ground.
- **Solution:**
  - The camera is placed at `position="0 1.6 0"`, a standard eye height for VR/first-person scenes.
  - Held objects are positioned about 2 units in front of the camera and aligned with its rotation, ensuring they appear at a natural height and distance.
  - When dropped, objects have their position and rotation explicitly set, and physics are reapplied so they settle naturally onto the floor.

## How to Use

1. Open the site in a modern browser (desktop or mobile).
2. Wait for the physics engine to load (you'll see a loading overlay).
3. Use your mouse (desktop) or touch (mobile) to look around and move.
4. Click/tap on an object to pick it up. Click/tap again to drop it.
5. Use the controls to inspect objects or move around the scene.

## Technologies Used
- [A-Frame](https://aframe.io/) for 3D scene and VR/AR support
- [PhysX](https://github.com/c-frame/physx) for real-time physics
- JavaScript for custom logic and controls

## License
MIT License. See LICENSE file for details.
