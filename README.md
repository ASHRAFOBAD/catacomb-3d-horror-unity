# Catacomb: 3D First-Person Survival Horror (Unity Engine)

A first-person 3D survival horror maze game developed in Unity Engine (C#). Set in an underground subterranean labyrinth, players must navigate through dark corridors, manage limited inventory resources (lantern light, ammunition), evade/neutralize an aggressive patrol AI, and find the escape key to unlock the exit door. 

The project features two distinct, hand-crafted maze layouts representing scalable difficulty tiers with differing sight-lines, patrol route densities, and chase mechanics.

---

### 🎮 Play & Download
* **Playable Windows Build (.zip):** [Download from Google Drive](https://drive.google.com/drive/folders/YOUR_FOLDER_ID_HERE?usp=sharing)


---

### System Architecture & State Execution

The gameplay loop integrates multiple decoupled subsystems spanning kinematic movement, artificial intelligence, raycast hitscan combat, and trigger-based interaction:

```text
                               +-----------------------------+
                               |     Game / Level Loop       |
                               +--------------+--------------+
                                              |
        +-------------------------------------+-------------------------------------+
        |                                     |                                     |
        v                                     v                                     v
+---------------+                     +---------------+                     +---------------+
| Player System |                     |   Enemy AI    |                     |  Environment  |
| - Movement    |                     | - NavMesh     |                     | - Trigger IO  |
| - Weapon Sway |                     | - Patrolling  |                     | - Item Chests |
| - FOV Zoom    |                     | - Line-of-Sight|                     | - Exit Door   |
| - Health/Death|                     | - Death Drop  |                     | - Post-FX     |
+-------+-------+                     +-------+-------+                     +-------+-------+
        |                                     |                                     |
        | [Hitscan Raycast / Damage Event]    |                                     |
        +------------------------------------>+                                     |
        |                                     | [Collision / Kill Radius]           |
        |                                     +------------------------------------>| (Triggers Fade-to-Black)
        |                                                                           |
        | [Reach Tool Trigger Collision]                                            |
        +---------------------------------------------------------------------------> (Updates Crosshair & Unlocks)
