# ❓ Frequently Asked Questions (FAQ) — Penumbra & Glamourer Preview Manager

This FAQ covers common questions, performance guidelines, and technical details for both **Penumbra Preview Manager (PPM)** and **Glamourer Preview Manager (GPM)**.

---

## 1. Core Questions

### Why are these separate plugins? Why doesn't Penumbra/Glamourer support previews natively?
The developers of Penumbra and Glamourer have a strict design philosophy focused on keeping the core tools high-performance, lightweight, and database-centric. Adding image rendering engines, clipboard monitors, screenshot crop overlays, and custom UI components is considered out-of-scope for the core modding database. 

They officially recommend using community-made companion plugins for these features. You can read the official discussion and reasoning in the **Penumbra Discord**:
https://discord.gg/PvxW4mXaWp](https://discord.com/channels/884363610640498698/1061229753794826241

---

## 2. Performance & Resource Management

> [!WARNING]
> **Important Performance & Memory Disclaimer**
> 
> PPM and GPM provide the *framework* for loading and rendering custom images. They do not automatically compress or optimize the files you choose to import. 
> 
> * **User Responsibility:** The responsibility for managing system resources and texture sizes lies entirely with you (the user) or the mod creator who packages the preview files.
> * **VRAM / RAM Danger:** Loading hundreds of uncompressed 4K PNG images can quickly deplete your Video RAM (VRAM) or system memory, leading to frame drops, micro-stutters, or game crashes (DirectX 11 errors).

### What are the best practices for preview images?
To keep your game running smoothly, follow these image guidelines:
1. **Resolution:** We recommend a maximum resolution of **1280x720 (720p)** for preview images. Since the previews are displayed as thumbnails in small ImGui panels, 720p is more than enough for crisp visuals.
2. **Format:** Use **PNG** or **JPG/JPEG**. If you are a mod creator packaging previews, pre-compress your images.
3. **Aspect Ratio:**
   * **PPM (Penumbra):** Best scaled at **16:9** (landscape).
   * **GPM (Glamourer):** Best scaled at **9:16** (portrait/vertical), though GPM supports multiple ratios.

---

## 3. Data Portability & Mod Sharing

### If I share my Penumbra mod with a friend, will they see my option previews?
**Yes, absolutely!** 
PPM was designed with portability in mind. Individual option previews are stored in a `ppm/` directory and tracked in a `ppm.json` file directly inside the respective mod's folder. As long as you zip or share the entire mod folder, anyone else with the Penumbra Preview Manager plugin installed will instantly see your custom previews.

### Can I share my Glamourer design previews the same way?
**No, not directly.**
Glamourer designs are saved in Glamourer's centralized configuration database rather than individual folders on your disk. Therefore, GPM stores all preview allocations in a central `allocation.json` file inside the Dalamud plugin configuration directory. If you want to move your Glamourer previews to a new PC, you will need to copy the GPM configuration folder:
`%appdata%\XIVLauncher\pluginConfigs\GlamourerPreviewManager\`

---

## 4. Troubleshooting & FAQ

### Why does a preview image show as a black or empty box?
If an image fails to load, check the following:
* **Invalid File Format:** Ensure the image is a valid, uncorrupted `.png`, `.jpg`, `.jpeg`, `.webp`, `.bmp`, or `.gif`.
* **Broken URL:** If you imported the image via a URL, the link may have expired or the hosting site might block hotlinking (e.g., Cloudflare protection). Try downloading the image and pasting it from your clipboard instead.
* **NSFW/Restricted Mods:** If you are importing from XIVModArchive (XMA), remember that the plugin cannot automatically download images from mods flagged as NSFW or Restricted unless you manually copy-paste the image from your browser.

### Do these plugins run in the background and impact game performance?
**No.** 
PPM and GPM are only active when you open the **Penumbra Mod Settings** window or the **Glamourer Design Panel**. When these panels are closed, the plugins consume virtually 0% CPU/GPU and do not render anything. 
When the panels are open, the texture loading is asynchronous, meaning it won't freeze your game while loading images.

---

## 5. Support & Feedback
If you run into bugs or have feature requests, please join the official support server:
📢 **[Join the Support Discord](https://discord.gg/PvxW4mXaWp)**
