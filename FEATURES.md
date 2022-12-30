# Features

This document is a complete listing of all the features available in the game.

## Title Screen

* The starry background features bright squares that blink periodically. The stars also move depending on your device's orientation.

## Help and Credits Scene

* Uses a slider to allow navigating between pages of information.

## Options

* Allows the player to toggle device vibration on/off. Click [here](#device-vibrations) to see when vibrations occur.

## Gameplay

### Missiles

#### Player Missiles

* Launched by missiles launchers and will fly towards the location clicked or tapped by the user on the screen.

* These missiles explode upon reaching their destination.

#### Enemy Missiles

* Spawns at the top of the playing field, off-screen and travels downwards at a random angle.

* Explodes upon collision with the ground, a missile launcher, a city or another explosion.

* There are standard missiles and cluster missiles. Only cluster missiles have the special behaviour to branch off into multiple standard missiles during their descent.

  * The time before the cluster missile branches off depends on the current wave.

  * The cluster missile will flash before branching off.

* The speed at which enemy missiles travel at depends on the current wave.

### City

* Serve as objects the player must defend.

* The game ends when all cities have been destroyed.

### Missile Launchers

* Serve as a weapon that players must use to defend their cities.

* Tap on a missile launcher to make it active. This will deactivate other missile launchers, if they are already active.

  * A visual indication will appear to show that the launcher is active.

* Tap anywhere on the screen to launch a missile from that active missile launcher to that position.

* Status text will appear when the launcher has ammo less than or equal to a specified percentage of its capacity, or when it is destroyed.

  * The text "LOW" appears when current ammo is less than or equal to 40%.

  * The text "OUT" appears when there are no more missiles or when it is destroyed.

* Missile launchers are unusable when destroyed or when it's out of missiles.

* When all missile launchers have become unusable, the game will fast-forward itself.

### Device Vibrations

* The device vibrates whenever a missile launcher or city gets destroyed.

### Explosions

* Explosions are created whenever a player's missile reaches its destination, or when an enemy missile hits the ground, a city, a missile launcher or comes into another explosion.

* Explosions caused by enemy missiles will destroy cities, missile launchers and other enemy missiles that come into contact.

* However, explosions caused by the player's missiles will only destroy enemy missiles.

* Also, explosions that come from player-destroyed enemy missiles will only destroy enemy missiles.

### Points

* Points are displayed when an enemy missile is destroyed by the player and will go away after a few seconds.

* The value shown is the amount of points added to the player's total score ever since the missile got destroyed.

* The standard enemy missile awards 5 points when destroyed, while the cluster missile awards 10 points.

* The displayed point value will increase in font size and will start to alternate between yellow and red more as you get more points from the explosion due to combo. The visual effects get more intense up to a max.

### Combo

* A combo happens when player-caused explosions destroy more than one missile.

* When this happens, additional points are awarded to the player based on the number of missiles destroyed.

  * The amount of additional points are calculated using $n * \text{base}$ where $n$ is the number of missiles destroyed, including the one we just destroyed, and $\text{base}$ is the number of points the missiles originally awards.

  * For example, the player fired a missile which damaged a standard enemy missile. The player gets 5 points. After which, the resulting explosion destroyed another standard enemy missile. The player will get 10 additional points, as we multiply 5 by 2, where 2 is the number of missiles the player has destroyed. The total number of points the player gets from that single instance of firing the missile is 15.

  * The additional score will be added to the displayed point value from the explosion, to reflect the amount of points the single chain of explosions have given.

  * Every player missile explosion is considered a standalone combo. Meaning the combo from one player missile explosion will not carry over to another player missile explosion. So each chain will have its own combo.

  * In the event there are many missile explosions in an area and an enemy missile gets caught in multiples of them, the combo from the enemy missile gets awarded to the chain that has the highest combo.

  * Combos end once all explosions caused by the chain dies off.

### Progression

* As the player progresses to the next wave, things are going to get more difficult.

* The following properties changes when the player progresses:

  * Missile speed is increased.

  * Spawning frequency is generally increased. That is because the interval between spawning
  gets lesser.

    * Internally, spawning frequency uses a range. A random value is picked within the range and used as the interval for the next spawn. As progression happens, the upper and lower limits of the range are moved closer to 0, which results in lower intervals.

  * More missiles will spawn, up to a maximum value.

  * The chance that an enemy cluster missile will spawn instead of a standard enemy missile increases, up to a max value.

## Audio

* Missile launchers use `AudioSource.PlayOneShot` to play its firing sounds, which stops one sound from clipping another, because the other one hasn't finished playing.
