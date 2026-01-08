package.json: Node project config. Name: "brainrot-gaming-platform". Version: "1.0.0". Type: "module". Scripts: dev (vite), build (vite build), preview (vite preview), lint (eslint). Dependencies: react, react-dom, zustand, @react-three/fiber, @react-three/drei, three, axios, tailwindcss, postcss, autoprefixer. DevDependencies: @vitejs/plugin-react, vite, eslint, tailwindcss, postcss.

vite.config.js: Vite configuration. Plugin: @vitejs/plugin-react. Build target ES2020. Output dir: "dist". Optimizations: React plugin enabled. Base: "/" for Vercel deployment.

tsconfig.json: TypeScript config (optional). CompilerOptions: jsx: "react-jsx", esModuleInterop: true, moduleResolution: "bundler". Include: ["src/**/*"]. Exclude: ["node_modules", "dist"].

tailwind.config.js: Tailwind CSS config. Content: ["./index.html", "./src/**/*.{jsx,js}"]. Theme: Extend colors (brainrot-purple, gaming-neon, dark-bg). Variants: responsive, hover, focus, group-hover.

postcss.config.js: PostCSS config. Plugins: tailwindcss, autoprefixer.

index.html: Root HTML file. DOCTYPE, meta tags (charset UTF-8, viewport responsive). Title: "Brainrot Gaming Platform". Root div with id="root". Script: type="module" src="src/main.jsx".

README.md: Complete documentation. Project description. Features list. Tech stack. Deployment instructions (3 steps: npm install && npm run build, deploy to Vercel, visit URL). Local development: npm install && npm run dev. File structure explanation. Game modes description. Player progression system. Cosmetics and shop details. Browser compatibility (Chrome, Firefox, Safari, Edge).

.env.example: Environment variables template. VITE_API_URL (optional), VITE_STORAGE_VERSION="1.0", VITE_MAX_PLAYERS_PER_GAME="10", VITE_BRAINROT_SPAWN_RATE="5000", VITE_GARDEN_TICK_RATE="2000", VITE_ABILITY_COOLDOWN="3000", VITE_PET_EVOLUTION_THRESHOLD="100".

src/main.jsx: React entry point. Imports React, ReactDOM, App component. ReactDOM.createRoot(document.getElementById("root")).render(<App />). Initializes error boundary.

src/App.jsx: Main application component. Imports Router/navigation logic, stores initialization, theme provider. Conditional render based on userStore.isLoggedIn(). Routes: /login (AuthScreen), /dashboard (MainDashboard), /game/:mode (GameScreen), /profile (ProfileScreen), /shop (ShopScreen), /leaderboard (LeaderboardScreen). Error boundary wrapper. Layout with Header, Sidebar, MainContent, Footer.

src/components/Layout/Header.jsx: Navigation header component. Props: none. Display: User avatar, username, current level, XP bar, coin balance, gem balance. Buttons: Profile icon, Settings icon, Shop icon, Logout. Responsive design. Imports userStore. Uses Tailwind dark mode styling.

src/components/Layout/Sidebar.jsx: Left sidebar navigation. Props: none. Menu items: Dashboard, Steal a Brainrot, Grow a Garden, Ability Wars, Pet Simulator. Active route highlighting. Icons for each game mode. Leaderboard link. Settings link. Responsive collapse for mobile. Imports navigation hooks.

src/components/Layout/Footer.jsx: Footer component. Props: none. Display: Version info, last update time, online player count (simulated). Social links. Feedback button. Copyright notice.

src/components/Common/Button.jsx: Reusable button component. Props: children, onClick, variant (primary, secondary, danger, success), size (sm, md, lg), disabled, loading, icon. Tailwind classes for styling. Loader animation when loading prop true.

src/components/Common/Modal.jsx: Reusable modal component. Props: isOpen, onClose, title, children, footer, size (sm, md, lg, xl). Portal rendering. Backdrop with click-to-close. Header with close button. Body and footer sections. Animation on open/close.

src/components/Common/Card.jsx: Reusable card component. Props: children, className, header, footer, hoverable. Box shadow, border-radius. Responsive padding. Tailwind dark mode support.

src/components/Common/Loading.jsx: Loading spinner component. Props: size, message, fullscreen. Animated spinner using CSS. Text message display. Center alignment.

src/components/Common/XPBar.jsx: Experience bar component. Props: currentXP, maxXP, level. Visual bar filling. Percentage display. Progress text. Color change at thresholds.

src/components/Common/CurrencyDisplay.jsx: Currency display component. Props: coins, gems, showAnimation. Icons for coins and gems. Number animation when currency changes. Imports userStore.

src/components/GameModeSwitcher.jsx: Game mode selection screen. Props: none. Display: 4 game mode cards (Steal a Brainrot, Grow a Garden, Ability Wars, Pet Simulator). Each card: icon, description, player count, best time/score. Click to launch game. Returns router navigation. Imports gameStore.

src/components/Profile.jsx: User profile screen. Props: userId (optional, defaults to current). Display: Avatar, username, level, total XP, join date, total playtime, statistics per game mode, achievement badges, equipped cosmetics. Edit profile button (name, avatar). Export stats button. Imports userStore.

src/components/Shop.jsx: Shop component. Props: none. Tabs: Cosmetics (skins, emotes, effects), Boosts (XP boost, double coins, pet food), Pet Items (eggs, breeding materials). Item cards: name, description, price (coins/gems), preview. Buy button with confirmation. Currency display. Imports playerStore, userStore.

src/components/Leaderboard.jsx: Leaderboard component. Props: gameMode (optional, all games or specific). Display: Ranked list of top 50 players. Columns: rank, username, level, score/winrate, XP. Search bar to find player. Tab switching between game modes. Sorting options (XP, wins, score). Local storage data. Imports leaderboardStore.

src/components/Settings.jsx: Settings screen. Props: none. Options: Audio toggle (master, sfx, music volume sliders), Video quality (low, medium, high), Controls customization (for Ability Wars, Steal a Brainrot), Delete account confirmation, Clear cache, Export/Import save data. Save/Reset buttons. Imports userStore.

src/components/AuthScreen.jsx: Login/Register screen. Props: none. Display: Logo, login form (email/username, password) and register form (username, email, password, confirm password, terms checkbox). Toggle between login/register. Social login buttons (Google, GitHub - simulated). Store user data in localStorage and IndexedDB. Imports userStore.

src/games/StealABrainrot/StealABrainrot.jsx: Main Steal a Brainrot game component. Props: none. Display: 3D arena using Three.js/Babylon.js. Player count: 4-8 players. Objective: Steal brainrot from opponents, return to base. Controls: WASD movement, mouse look, space jump, Q interact, R reload. UI: HUD with health, ammo, brainrot count, team score. Timer. Minimap. Kill feed. Match end screen with rewards. Imports game store, battle service. Babylon.js engine setup.

src/games/StealABrainrot/StealABrainrotGame.jsx: Game logic for Steal a Brainrot. Manages: Player spawning, movement, collision detection, brainrot pickup/drop, team scoring, match timer, win condition (first to X brainrots or time limit). Random AI player behavior. Calculates XP and coin rewards. Handles damage/death mechanics. Uses babylon.js physics. Exports tick() function for game loop.

src/games/StealABrainrot/Arena.jsx: 3D arena component. Props: gameInstance. Creates 3D mesh arena using Babylon.js. Spawns bases (red, blue), brainrot locations, obstacles, walls. Lighting setup (ambient + directional). Shadow mapping. Material/texture application. Camera setup. Responsive canvas sizing.

src/games/StealABrainrot/Player.jsx: 3D player character model. Props: position, rotation, team, health, name. Creates Babylon mesh (capsule or imported model). Applies team color shader. Name tag above player. Health indicator. Animations: idle, running, jumping, falling, shooting. Handles model destruction on death.

src/games/StealABrainrot/store.js: Zustand store for Steal a Brainrot game state. State: players (array with position, health, team, brainrot count), teams (red, blue with scores), matchTime, playerStats (kills, deaths, captures), localPlayerID, matchStatus (playing, ended). Actions: updatePlayerPosition, addKill, captureFlag, endMatch, resetGame. Persists top scores to IndexedDB.

src/games/GrowAGarden/GrowAGarden.jsx: Main Grow a Garden game component. Props: none. Display: 3D garden view using Babylon.js. 9-grid farm plot layout. UI: Seed selection menu, plant details, harvest button, inventory (seeds, fertilizer), shop for seeds/tools, watering can cursor. HUD: Money, time until growth, overall garden value. Tutorial on first load. Imports game store, progression service.

src/games/GrowAGarden/GardenSimulator.jsx: Farming simulation logic. Manages: Crop growth stages (planted, sprouting, growing, mature, harvestable), growth tick calculation (15-60 seconds per stage), fertilizer effect (doubles speed, costs coins), watering mechanics (visual effect, growth boost). Crop types: corn (15s growth, 100 coins), tomato (20s, 120 coins), carrot (25s, 150 coins), legendary flower (60s, 1000 coins + special effect). Market prices fluctuation. Harvest reward logic. Random events (pest, rain). Exports tick() function.

src/games/GrowAGarden/GardenWorld.jsx: 3D garden visualization. Props: gardenState. Creates Babylon scene with 9 plots (3x3 grid). Each plot: interactive mesh, particle effects on harvest, animations on plant/grow/wilt. Sky and lighting. Ground texture. Water effects. Responsive camera zoom. Plot interaction detection.

src/games/GrowAGarden/Crop.jsx: 3D crop model component. Props: cropType, growthStage, position. Creates Babylon mesh representing crop at growth stage (seed, sprout, plant, flower). Applies appropriate textures/colors. Animation blend between stages. Particle effects (growth sparkles, water splash on water). Lod system for performance.

src/games/GrowAGarden/store.js: Zustand store for garden simulator state. State: plots (array with crop type, growth progress, planted time, fertilizer applied), inventory (seeds count, coins, fertilizer), harvestedThisSession, totalHarvests, garden level, special events. Actions: plantCrop, waterCrop, harvestCrop, useFertilizer, buySeeds, tick (progress crops), sellCrop. Persists to IndexedDB with auto-save every 10 seconds.

src/games/AbilityWars/AbilityWars.jsx: Main Ability Wars 3v3 arena battle component. Props: none. Display: Isometric 3D battle arena using Babylon.js. 6 playable champions (3v3 teams). UI: Champion health bars, mana/energy bar, ability buttons (Q, W, E, R cooldowns), minimap, combat log, team score. Match timer. Victory condition: destroy enemy nexus or eliminate all enemies. Real-time battle system (not turn-based). Imports game store, battle service. Tutorial/champion select screen before match.

src/games/AbilityWars/Arena3v3.jsx: 3D isometric arena for battles. Props: gameInstance. Creates Babylon scene with arenas (blue side, red side), lanes (3 lanes), minions, towers (future). Terrain with elevation changes. Fog of war simulation. Lighting for competitive feel. Camera setup (locked isometric view with zoom). Particle systems for ability effects.

src/games/AbilityWars/Champion.jsx: 3D champion character model. Props: championType, team, level, abilities. Creates Babylon mesh (hero model). Team color tint. Animations: idle, walking, casting, death. Ability indicators above character. Health/mana bars. Level indicator. Particle effects on ability cast. Name tag. Shadow. Handles animation blending.

src/games/AbilityWars/Ability.jsx: Ability component managing ability execution. Props: abilityConfig, caster, targets. Visual effect creation (projectile, AoE, beam, buff particle). Handles: cooldown tracking, mana cost, range validation, target validation. Particle effect spawning at cast and impact. Animation triggers. Damage calculation via battle service. Sound effect triggers (no actual audio, just trigger markers). Destroys after duration.

src/games/AbilityWars/BattleSystem.jsx: Real-time battle system logic. Manages: Player input handling (ability clicks), cooldown tracking, mana regeneration (5 per second), health regeneration (2 per second in base), collision detection, friendly fire prevention, XP gain from kills. Calculated damage formula: baseAbilityDamage * (1 + level * 0.1) * damageModifiers. Win condition: nexus health = 0. Exports tick(deltaTime) for game loop. Sends XP/rewards to progression service on match end.

src/games/AbilityWars/store.js: Zustand store for Ability Wars state. State: champions (array with hp, mana, position, level, abilities data), teams (red, blue with nexus hp, score), gameTime, playerChampionID, abilityStates (cooldowns, mana costs), matchStatus. Actions: castAbility, takeDamage, gainXP, restoreMana, endMatch, selectChampion, resetGame. Persists champion win rates and statistics to IndexedDB.

src/games/PetSimulator/PetSimulator.jsx: Main Pet Simulator game component. Props: none. Display: 3D pet world using Babylon.js. Show current selected pet in 3D view. UI: Pet list (all owned pets), pet stats (name, level, happiness, hunger, energy), actions (feed, play, pet, sleep, breed, battle). Pet collection counter. Breeding panel (shows countdown if breeding). Battle selector. Shop for pet eggs and items. Imports game store, breeding service, progression service. Tabs: My Pets, Breeding, Battles, Eggs, Shop.

src/games/PetSimulator/PetWorld.jsx: 3D pet world visualization. Props: selectedPet. Creates Babylon scene with pet environment (grassy area, water, trees, toys). Spawns selected pet model. Interactive toys that player can click. Day/night cycle (affects pet behavior). Weather effects. Camera follows pet with user zoom control. Background ambient animation.

src/games/PetSimulator/Pet.jsx: 3D pet model component. Props: petData, environment, isInteracting. Creates Babylon animated pet model. Pet type variation (cat, dog, dragon, alien, etc.). Size based on level. Color/pattern from genetics. Animations: idle (multiple variations), walking, running, eating, sleeping, playing, evolving (transformation). Particle effects on stat changes. Name tag. Heart particles when happy. Responds to interaction (follows mouse, plays animation).

src/games/PetSimulator/PetBreeding.jsx: Pet breeding UI and logic component. Props: none. Display: Breeding panel showing 2 pets to breed (dropdown selection). Breeding requirements display (level 10+, cost 500 coins). Button: Initiate breeding. Shows countdown timer (2-5 minutes real time). Result: Egg spawned in inventory. Egg hatching UI: Can check growth %. Egg names, predicted stats. Notification on hatch. Imports breeding service, pet store.

src/games/PetSimulator/PetBattle.jsx: Pet vs Pet battle component. Props: playerPet, opponentPet, onEnd. Display: Isometric view of 2 pets facing each other. Health bars for both. Turn-based battle system: Player chooses attack (1-3 attack types per pet), opponent selects random attack. Turn timer. Damage calculation with type advantage. Victory screen with rewards (coins, exp). Imports battle service. Can battle AI or other players' pets (simulated).

src/games/PetSimulator/store.js: Zustand store for Pet Simulator state. State: pets (array with type, level, exp, genetics, stats: happiness, hunger, energy, mood, breedCount), currentPetID, eggs (array with progress, genetics, hatchTime), petBoxCapacity (starts 5, upgradeable), breedingPairs (tracking active breeding), petStats (total level, battles won, eggs hatched). Actions: addPet, selectPet, updatePetStats, startBreeding, hatchEgg, releasePet, feedPet, playWithPet, petPet, sleepPet, evolveIfReady. Persists all to IndexedDB. Auto-saves every 30 seconds. Implements pet decay (hunger/energy increase, happiness decreases if not interacted with).

src/stores/userStore.js: Zustand user store. State: userID, username, email, level (1-100), totalXP, coins (earned in games), gems (premium currency), joinDate, lastLoginDate, totalPlaytime, preferredGameMode, equipdCosmetics (skin, emote, effect), accountStatus (active/banned), notificationSettings. Actions: createUser, loginUser, logoutUser, updateProfile, addCoins, addGems, spendCoins, spendGems, levelUp, gainXP, setCosmetic. Persists to localStorage (user profile) and IndexedDB (secure data). Validates user login from stored credentials.

src/stores/gameStore.js: Global game state store. State: currentGameMode (null or game mode string), isInGame (boolean), globalPlayerStats (kills, deaths, matches played across all modes), currentMatch (matchID, status, players count, duration), soundSettings (masterVolume, sfxVolume, musicVolume), videoSettings (quality, fpsTarget, shadowQuality). Actions: switchGameMode, startMatch, endMatch, updateGlobalStats, setSoundSettings, setVideoSettings. Simple global management without persistence (matches stored per-game).

src/stores/playerStore.js: Player inventory and cosmetics store. State: inventory (equipped items, count, slot management), cosmetics (skins owned, emotes owned, effects owned, equipped items per game), boosters (active boosts with expiry), achievements (unlocked with date), badges. Actions: buyCosmetic, equipCosmetic, activatBooster, unlockAchievement, inventoryAdd, inventoryRemove. Persists to IndexedDB. Updates on purchase from shop.

src/stores/leaderboardStore.js: Leaderboard data store. State: leaderboards (separate arrays per game mode: allPlayers ranked by XP/score, weekly top 100, allTimeTop 100), playerRanks (user's rank in each mode), localStats (player's stats for rank calculation). Actions: updateLeaderboard, calculateRanks, getPlayerRank, getTopPlayers, searchPlayer, resetWeeklyLeaderboard (runs on schedule via IndexedDB timestamp check). Calculates rankings from userStore data and gameStore stats. Simulates data for other players.

src/services/storageService.js: Unified storage management service. Functions: initDB() - opens IndexedDB connection with version 1, stores (users, pets, matches, cosmetics, leaderboard data, saved games). setItem(store, key, value) - persists to IndexedDB. getItem(store, key) - retrieves from IndexedDB. getAllItems(store) - retrieves all items from store. deleteItem(store, key). clearStore(store). exportData() - exports all stores as JSON. importData(json) - imports JSON into stores. migrationHandler for schema updates. Error handling and fallback to localStorage if IndexedDB unavailable.

src/services/multiplayerService.js: Multiplayer simulation service (offline). Functions: getLocalPlayers() - returns simulated list of players from localStorage ("matchPlayers" store). broadcastPlayerUpdate(playerData) - stores player state in localStorage under current match key. receivePlayerUpdates() - returns updates from other "players" in localStorage. simulateAIPlayer(gameMode) - returns randomized AI player actions/positions. matchmaking() - finds available local players or creates AI opponents. Uses localStorage events listener (storage event on other tabs if needed) or simple polling. exportMatchData() - saves match to IndexedDB for replay. No actual WebSocket (client-side only).

src/services/gameProgressService.js: Player progression and XP system service. Functions: gainXP(amount, gameMode) - adds to global XP and game-specific XP. calculateXPReward(match stats) - returns XP based on kills, score, time, position (winner gets bonus). checkLevelUp(currentXP) - returns new level if XP > threshold. getXPThreshold(level) - exponential formula: 100 * (level ^ 1.5). gainCoins(amount) - adds coins to player. spendCoins(amount) - deducts coins with validation. getAchievement(condition) - unlocks achievement if condition met. Tracks achievements (first win, level 10, 100 kills, breed 10 pets, etc.). Updates userStore and leaderboardStore on progression. Emits events for UI updates.

src/services/petBreedingService.js: Pet genetics and breeding logic. Functions: createPet(parentA, parentB) - creates offspring with blended genetics (color, pattern, size tendency, stat potential). getEggHatchTime() - returns milliseconds until hatch (exponential random: 120-300 seconds). inheritTraits(parents) - Mendelian genetics simulation (dominant/recessive traits). calculateStats(genetics, level) - stat calculation based on genes and level. canBreed(pet1, pet2) - validates both 10+ level, not parent-child, not same individual. evolveIfReady(pet) - evolves pet at level 25, 50, 75 (changes model/type). calculateEvolutionStats(currentPet) - stat boost on evolution. Stores pet genetics in IndexedDB for persistence.

src/services/battleService.js: Battle calculation and mechanics engine. Functions: calculateDamage(attacker, ability, defender) - formula: baseAbilityDamage * (1 + attackerLevel * 0.1) * damageMultiplier * randomCrit(0.85-1.15). applyEffect(target, effect) - applies status effects (burn, freeze, slow with duration). checkTypeAdvantage(petTypeA, petTypeB) - returns multiplier (1.5 for advantage, 0.5 for disadvantage, 1.0 for neutral). calculateBattleWinner(team1, team2) - determines match winner. calculateXPGain(winner, loser, matchDuration) - XP reward formula: baseXP * winMultiplier * (duration modifier). recordBattle(winner, loser, duration, stats) - saves match data to IndexedDB. Exports battle replay generation function.

src/services/achievementService.js: Achievement system management. Functions: unlockAchievement(achievementID) - marks achievement as unlocked with timestamp. getAchievements() - returns all achievement definitions (name, description, reward coins/gems, condition logic). checkConditions(playerStats) - evaluates if conditions met for any achievements. getReward(achievementID) - returns coin and gem rewards. displayNotification(achievement) - triggers UI notification. Data: Predefined achievements (First Blood, Garden Master - harvest 100 crops, Pet Collector - catch 50 pets, etc.). Stores in IndexedDB with unlock date.

src/utils/constants.js: Game constants. Exports: XP_THRESHOLDS (level scaling), GAME_MODES (array with metadata), ABILITY_CONFIG (per-champion abilities with cooldowns, mana cost, damage), PET_TYPES (attributes, base stats, evolution paths), COSMETIC_PRICES (coins/gems), STAT_MULTIPLIERS (critical chance base, dodge base), ACHIEVEMENT_DEFINITIONS (name, description, reward, condition function), CROP_TYPES (growth time, sell price, rarity), STORAGE_KEYS (constant strings for localStorage), MAP_DIMENSIONS (arena sizes), RESPAWN_TIME (seconds).

src/utils/helpers.js: General utility functions. Functions: formatTime(ms) - returns MM:SS format. formatNumber(n) - returns 1K, 1M notation. clampValue(val, min, max) - clamps number. calculateDistance(p1, p2) - 3D distance. randomRange(min, max) - random integer. shuffleArray(arr) - Fisher-Yates shuffle. debounce(func, wait) - debounce wrapper. throttle(func, limit) - throttle wrapper. generateID() - unique ID generation. lerp(a, b, t) - linear interpolation. easeInOutQuad(t) - easing function. getRandomElement(arr) - random selection.

src/utils/mathHelpers.js: Game math utility functions. Functions: calculateDistance2D(p1, p2) - returns euclidean distance. rotateVector(vector, angle) - 2D vector rotation. normalizeVector(vector) - unit vector. dotProduct(v1, v2) - dot product. isPointInCircle(point, center, radius) - collision detection. isPointInRect(point, rect) - AABB collision. getCollisionResponse(vel, normal) - velocity reflection. predictPosition(currentPos, velocity, time) - extrapolation. calculateAngleBetween(p1, p2) - returns angle in radians. getRandomPointInCircle(center, radius) - random spawn point.

src/utils/animations.js: Animation utilities for UI and game. Functions: springValue(current, target, stiffness) - spring physics animation. createKeyframeAnimation(frames, duration) - keyframe animation data. easeOutElastic(t) - easing function. easeInBounce(t) - easing function. colorLerp(colorA, colorB, t) - color interpolation. createParticleEmitter(config) - particle system configuration. animationLoop() - RAF-based loop handler. Exports preset animations (popIn, fadeIn, slideIn, bounce, wobble, pulse).

src/utils/babylonHelpers.js: Babylon.js 3D utilities. Functions: createScene(canvas, lights) - initializes Babylon scene with lighting. createGround(size, texture) - ground plane with texture. createSkybox(colorHex) - simple colored skybox. createParticleSystem(emitterConfig) - particle system factory. loadModel(url, position) - model loading (from CDN). createHealthBar(scene, position, max, current) - 3D health indicator. applyMaterialToMesh(mesh, colorHex, roughness) - material application. enablePhysics(scene, gravity) - physics engine setup. getMousePickPosition(scene, pointerInfo) - raycasting. createAnimation(targetMesh, property, keyframes) - animation creation. freeCameraSetup(scene, position, target) - camera initialization.

public/index.html: Already covered in root index.html (same file).

public/favicon.ico: Favicon file reference (external CDN URL or inline data URL).

public/manifest.json: PWA manifest. Name: "Brainrot Gaming Platform". Short_name: "BrainrotGames". Description: "Multiplayer web gaming platform with 4 game modes". Start_url: "/". Display: "standalone". Background_color: "#1a1a1a". Theme_color: "#8b5cf6". Icons array with 192x192 and 512x512 sizes (from CDN).

public/robots.txt: SEO robots configuration. User-agent: *. Allow: /. Disallow: /api/ (if applicable). Sitemap reference.

.gitignore: Standard Git ignore. Patterns: node_modules/, dist/, .env, .env.local, .DS_Store, *.log, .vscode/, .idea/, coverage/, build/.
