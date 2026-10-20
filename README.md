# Wojos Tools
Create custom and override existing tools with super abilities

## Goal
Add additional features to tools to mimic how the mcmmo plugin improves basic gathering in minecraft

## Features
- **New Tool:** *Mining Hammer*
  - Primary
    - Light: 3x1x1 (Vertical)
    - Heavy: 3x3x1 
  - Secondary
    - Light: 1x3x1 (Herizontal)
    - Break: 1x1x1 (Bad Pickaxe)
  - Special
    - Charge Level is persistent
    - 3x3x3

## Ideas
- Charge level drains after some time
- Pickaxe
  - Super (Options)
    - Charge Level is persistent
    - Short term Fortune Effect
    - Mining speed increase
    - Vain mining ability
- Siccle
  - Super (Options)
    - Bonus Essence
    - Bonus Items

## Animation Guide
The item that triggers the animation creates an interaction chain. A simple chain is as follows
- `My_Tool.json:: Interactions: { Primary: { My_Tool_Selector.json }` The tool goes to a selector json it pick what the user is hitting
- `My_Tool_Selector.json: { Effect: { PlayerAnimationId: SwingLeft, <Some selector info> }}` Tell the selector what animation to play and some details about how to select what your animation interacts with.
- `SwingLeft` Is an key for a key value Animation stored in the `Server/Item/Animations/My_Tool.json` file.

## Development Planns
- Hammer
			- Primary
				- Light
					- 1x3x1: Horizontal(Break 3 Blocks total)
					- (Med Knockback & Minimal dmg vs Hit Monsters)
				- Heavy
					- 3x3x1 (Break 9 Blocks)
					- (Heavy Knockback & Minimal dmg vs Hit Monsters)
					- Overhead Smash
			- Secondary
				- Light
					- 3x1x1: Vertical (Break 3 Blocks total)
				- Heavy
					- Break Single Block (Doesn't drop item? Slow? Tier Down Item?)
					- (Heavy Knockback & Minimal Damage vs Single Monster)
			- Special
				- 3x3x3 (Break 27 Blocks)
				- Charging
					- Bonus charge when hitting same block type
					- Charge decays over time when not breaking blocks
					- Full charge can decay out
					- Bonus charge when block gets broken
			- Components
				- HammerCharge (Can get added and removed from player)
					- CurrentChargeValue			0			// Current charge value
					- MaxTotalChargeValue			150			// Max total carge value
					- SpecialReadyChargeThreshold	100			// Charge Required for Special to be ready
					- ChargeDeayDelaySeconds		10 Seconds	// Time Delay before charge starts to decau
					- ChargeDelayCountdown			10 Seconds	// Delay tracking counter 
					- ChargeDecayIntervalSeconds	1 Second	// How often does decay get triggered
					- ChargeDecayValue				5			// How much carge decayed per tick
					- ChargePerHit					1			// How much charge gained when hitting a block
					- ChargePerBlockBreak			5			// How much charge gained when breaking a block
					- BlockTypeBroken				BlockId		// What was the block type that was broken
					- NumTimesBlockTypeBroken		0			// How many times have we broken the same block type
					- BonusPerNumBlockBroken		1			// Charge Value * NumTimesBlockTypeBroken as stacking bonus when breaking a block
				- BreakBlockEvent (Filter entity w/ HammerCharge Component)
				- HammerChargeSystem (Decays Hammer Change by X Ammount every Y Server Tic's, Remove component at 0)
			- Misc:
				- Short Range
				- Target Block Ghos
