# Wild West TD: finding and editing things

## Start here

Open `Assets/Wild West TD/Scenes/Wild West TD.unity`.
The game lives below **Wild West TD**. The original sample scene is separate.

## Edit the interface without writing layout code

Expand **07 Interface** in the Hierarchy. Home, Exploration, Battle and BartenderShop are real Canvas objects.
Select a Text to change its font, size, alignment or colour. Select a panel's Image to change its colour and transparency.
Use the Rect Tool and RectTransform anchors to move or resize controls. Enable a normally hidden panel temporarily to preview it in Edit Mode, then disable it again before saving.

The reusable Canvas is `Assets/Wild West TD/UI/Prefabs/SaloonInterface.prefab`.
Button **On Click** entries are saved in the Inspector. The controller updates live values and visibility; it does not create or position the menus.
Gold, wave numbers, changing button captions, shop ownership and lesson text still need small scripts. `SaloonInterface` connects those values to saved objects. Keep its binding keys unchanged; object names can be changed safely.
`BankIncomeLabel.prefab` controls the appearance of the floating bank payout.

## Place tower models before pressing Play

Open `Assets/Wild West TD/Prefabs/Towers`. Drag any of the eight prefabs into the Scene or Hierarchy.
They are ordinary visible 3D models in Edit Mode; no Play button or construction script is required.
Move, rotate and scale them with Unity's normal tools. The mesh is on the prefab root alongside its own tower script.
These decorative copies do not shoot, spend money or start a match. The game creates and binds its own copies to battle records.
The Gatling has one extra child mesh for the rotating barrels. Its script references that child in the Inspector.
Meshes are in `Meshes/Towers`, and their saved colours are in `Materials/Towers`.

## Read the scripts in this order

All game C# files are below `Assets/Scripts/Wild West TD`:

1. **Gameplay/Towers**: small named scripts for each tower and the shared `TowerView` model component. Each tower's starting cost, damage, firing rate, range and special settings are clearly named at the top of its own file. The shared battle reads these settings.
2. **Core/SaloonEconomy**: permanent Gold Coins, victory rewards and tower unlocks.
3. **Core/SaloonProgress**: tutorial, difficulties, entrance key and Wipe Progress.
4. **Core/FrontierRules**: collects the tower settings and handles upgrades, waves, enemies and combat. Its step is separated into spawning, firing, movement/rewards and wave completion.
5. **Gameplay/FrontierGame**: coordinates the match, camera, input and visible models.
6. **UI**: connects the saved Canvas to actions, lessons and feedback.
7. **World**: walking, table/map previews, the entrance, battle scenery and Otis' shop.
8. **Audio**: named WAV playback, music/effects preferences and sound synthesis fallback.

`partial class FrontierGame` means several files contribute to the same component. HUD, tutorial and effects have their own files so they are easier to find.
`FrontierModels` keeps the original source shapes for rebuilding designs and animated enemies. Live towers are instantiated from saved mesh prefabs, not built from primitives.

## Otis and the two currencies

Otis stands behind the counter under **03 Bar and Furniture**. Look at his upper body from near the counter and press E. Escape closes the shop.
The first four towers are owned at the start. Bank, Gatling, Shotgun and Bounty Hunter each cost **50 Gold Coins** to unlock permanently.
Each Easy win earns **50**, Medium **75**, Hard **100**. Training, defeats and leaving early award none.
Gold Coins survive between matches. Match cash starts fresh and pays for building/upgrading towers. Buying an unlock does not place a tower for free.
Wipe Progress resets coins and purchased towers along with tutorial, difficulty and entrance progress; the first four towers remain owned.

## Character and audio assets

Fitted hair, facial hair and joined hand meshes are in `Meshes/Characters`.
Otis' prefab is in `Prefabs/Characters`, with his new materials in `Materials/Characters`.
Original character assets remain in `Characters` to preserve existing references.
Music is in `Audio/Music`; individual effects are in `Audio/SFX`. Replace clips through the SaloonAudio Inspector references.

## Limits

The game still requires scripts for rules, interaction and changing values. The Canvas removes the need to code layout, not the need for gameplay logic.
Characters use stylized low-poly meshes and are not fully rigged humanoid models. Tower prefabs preserve their established designs; this is not a new animation system.

