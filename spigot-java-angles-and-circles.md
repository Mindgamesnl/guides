# Locations around a player, with math!
Quick demo, let's get the location in front of a player (you can change the angle yourself)

What you want to do in this case is calculate the location in front of the player, this can be don by calculating a circle.
You can do this with the  player's YAW and XZ locations

When calculating a circle, you don't calculate it all at once, you calculate a specific angle (one at a time), in stead of calculating the full 360° you can of course also only calculate it with the player's angle (where the YAW part comes in to play)

(the math part)

We'll first need a clone of the player location, simply do this by
```java
Location loc = player.getLocation().clone();
```

this is important since we will add/subtract from this later, and we don't want to ruin the real location
then we will calculate the radians

```java
double angle = Math.toRadians(loc.getYaw());
```

When we have done that, we can start calculating the X and Z (sine and cosine), we dont calculate Y since we are calculating a point in a horizontal circle around the player

After we have calculated that, we need to multiply it by the radius (so 1 is one block, 1.5 is one and a half block etc), for this example, two blocks should be it (i think) since when swimming the location is at the player's feet.
```java
double xTarget = Math.cos(angle) * 2;
double zTarget = Math.sin(angle) * 2;
```

Now we have the angle and target, we can add it to the player's location since it is still relative, lucky for us, Bukkit provides a function for this.
We can do this by using it on the CLONED location. But remember, we ONLY calculated the x and z axis, so we dont do anything with the Y coordinates.
```java
loc.add(xTarget, 0, zTarget);
```

Now we have loc, which should be the location two blocks in front of a player, as seen in the picture below
From that, you can teleport or do get block or whatever

I hope this helped some what <3

![](https://i.gyazo.com/210a165546b3b21f9d0bef628385b13f.png)
