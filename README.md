# GriefPrevention3D (Folia Edition)

A specialized, high-performance fork of GriefPrevention designed exclusively for **Folia** servers. This version features a fully thread-safe architecture, true 3D claim support, and eliminates global synchronization bottlenecks to ensure lag-free protection in a multi-threaded environment.

---

## ⚡ Key Features & Technical Changes

### 🚀 Folia Native & Thread-Safe
Unlike the original GriefPrevention which relies on global `synchronized` locks (which stall Folia's region threads), this version has been heavily refactored:
*   **Lock-Free Architecture:** Critical paths like claim lookups (`getClaimAt`) and event handling are now lock-free.
*   **Concurrent Collections:** Utilizes `ConcurrentHashMap` and `CopyOnWriteArrayList` to ensure data integrity across multiple threads without blocking region ticks.
*   **Atomic Operations:** Claim data modifications utilize atomic operations to prevent race conditions.

### 🧊 True 3D Claims
*   **Vertical Subdivisions:** Create stacked claims (e.g., apartments, multi-story bases) that respect Y-axis boundaries.
*   **3D Mode:** Toggle your shovel between 2D (infinite height) and 3D mode easily.

---

## 📥 Installation

1.  **Requirements:**
    *   Server Software: **Folia** (or a compatible fork). *Not compatible with standard Spigot/Paper.*
    *   Java: Java 21 or higher.
2.  **Setup:**
    *   Download the `GriefPrevention3D.jar`.
    *   Place it in your server's `plugins/` folder.
    *   Restart the server.

---

## 🎮 Command & Permission Reference

### 👤 Player Commands
Commands available to regular players for managing their claims.

| Command | Aliases | Description | Permission |
| :--- | :--- | :--- | :--- |
| `/claim` | | Create a claim using the golden shovel. | `griefprevention.createclaims` |
| `/abandonclaim` | `unclaim`, `declaim` | Delete the claim you are currently standing in. | `griefprevention.claims` |
| `/abandonallclaims` | | Delete **ALL** of your claims. | `griefprevention.abandonallclaims` |
| `/trust <player>` | `tr` | Grant full build access to a player. | `griefprevention.claims` |
| `/untrust <player>` | `ut` | Revoke access from a player. | `griefprevention.claims` |
| `/containertrust <player>` | `ct` | Grant access to chests, crops, animals, and buttons. | `griefprevention.claims` |
| `/accesstrust <player>` | `at` | Grant access to buttons, levers, and beds (no building). | `griefprevention.claims` |
| `/permissiontrust <player>` | `pt` | Grant permission to manage the trust list. | `griefprevention.claims` |
| `/trustlist` | | List all trusted players in the current claim. | `griefprevention.claims` |
| `/subdivideclaims` | `sc` | Switch shovel to **2D subdivision** mode (infinite height). | `griefprevention.claims` |
| `/3dsubdivideclaims` | `3dsubdivideclaim` | Switch shovel to **3D subdivision** mode (height restricted). | `griefprevention.claims` |
| `/basicclaims` | `bc` | Switch shovel back to basic claim creation mode. | `griefprevention.claims` |
| `/claimslist` | `listclaims` | View your claim block balance and claim locations. | `griefprevention.claims` |
| `/trapped` | | Eject yourself to nearby safe wilderness (has cooldown). | `griefprevention.trapped` |
| `/unlockdrops` | | Allow other players to pick up your death drops. | `griefprevention.unlockdrops` |
| `/givepet` | | Transfer a tamed pet to another player. | `griefprevention.givepet` |
| `/buyblocks` | | Buy claim blocks with server currency. | `griefprevention.buysellclaimblocks` |
| `/sellblocks` | | Sell claim blocks for server currency. | `griefprevention.buysellclaimblocks` |
| `/ignoreplayer <player>` | `ignore` | Ignore chat messages from a specific player. | `griefprevention.ignore` |
| `/unignoreplayer <player>` | `unignore` | Stop ignoring a player. | `griefprevention.ignore` |

### 🛡️ Administrative Commands
Commands for server staff to manage claims and moderation.

| Command | Aliases | Description | Permission |
| :--- | :--- | :--- | :--- |
| `/adminclaims` | `ac` | Switch shovel to Admin Claim mode (free, no owner, infinite). | `griefprevention.adminclaims` |
| `/adminclaimslist` | | List all administrative claims. | `griefprevention.adminclaims` |
| `/deleteclaim` | | Force delete the claim you are standing in. | `griefprevention.deleteclaims` |
| `/deleteallclaims <player>` | | Force delete **ALL** claims belonging to a player. | `griefprevention.deleteclaims` |
| `/deleteclaimsinworld` | | (Console) Delete all claims in a specific world. | `griefprevention.deleteclaimsinworld` |
| `/deletealladminclaims` | | (Console) Delete all admin claims. | `griefprevention.adminclaims` |
| `/ignoreclaims` | `ic` | Toggle "Ignore Claims" mode (bypass protections). | `griefprevention.ignoreclaims` |
| `/adjustbonusclaimblocks` | `acb` | Add/subtract bonus claim blocks for a player. | `griefprevention.adjustclaimblocks` |
| `/setaccruedclaimblocks` | `scb` | Set the precise accrued block count for a player. | `griefprevention.adjustclaimblocks` |
| `/restorenature` | `restore` | Switch shovel to Restoration Mode (revert terrain). | `griefprevention.adminclaims` |
| `/transferclaim <player>` | | Transfer the claim you are standing in to another player. | `griefprevention.transferclaim` |
| `/softmute <player>` | | Soft-mute a player (they can chat, but no one hears them). | `griefprevention.softmute` |
| `/separate <p1> <p2>` | | Force two players to ignore each other permanently. | `griefprevention.separate` |
| `/gpreload` | | Reload the plugin configuration and messages. | `griefprevention.reload` |

---

## 🛠️ How to Use 3D Claims

1.  **Create a Main Claim:**
    *   Use a Golden Shovel.
    *   Right-click two corners to create a standard 2D protection (protects from bedrock to sky).
2.  **Create a 3D Subdivision (Apartment/Floor):**
    *   Stand inside your main claim.
    *   Run `/3dsubdivideclaims` (or `/mode 3d`).
    *   Right-click the **bottom corner** (e.g., the floor of the 1st story).
    *   Right-click the **top corner** (e.g., the ceiling of the 1st story).
    *   You now have a subclaim that only exists between those Y-levels. You can trust players to this specific floor without giving them access to the roof or basement.

---

## ⚖️ Credits

*   **Ryan Hamshire**: The original creator of GriefPrevention.
*   **BigScary & GP Community**: For maintaining the legacy codebase.
*   **GriefPrevention3D Team**: For the Folia concurrency rewrite and 3D implementation.