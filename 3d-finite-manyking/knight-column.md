# Appendix: Older more complex setup involving a knight tower rather than a bishop tower

## Strong virtual rook
A normal virtual rook cannot move and is only able to attack kings.
A *strong* virtual rook is a white rook that's able to make an actual *move*, to capture another piece. This will be used to defend columns we want to prevent the black knight from moving to. 
Once the white rook moves away from its defended spot to capture something, a black rook below will capture the white rook. 
It then however must return to its starting position, otherwise white will be able to force a checkmate. 

[TODO: image]

If white ever moves their rook for "no reason", then black can simply capture it for free and move back, and white is now at a strict disadvantage.
So white will only move the rook when it can actually capture something. 

The original blog post described this setup and claimed its enough to constrain black's knights to 2 columns.
However, I could not find a way to make this work. 
There are two issues - The first is that it's difficult to make this setup tilable, which is necassary to consttain several adjacent columns a knight might move to. 
The second is that if black recaptures white's rook (including after black intentionally sacrifices their knight to it) but doesn't move back, it still takes 3 turns for white to win (and in fact the original blog claimed to not need any bishops in the setup, for which the only forcing wins i could find take even longer) - and this allows an oppotunity for the rook to instead move around freely and chase down some king for a faster win. So you'd need to be very careful about sheilding everything in the position with pawn walls to ensure it's resilient to a few arbitrary rook moves.

Thus, I came up with an alternate setup for a knight column, inspired by a comment by `@Stage Cardinal` in the infinite chess discord.
The strong virtual rooks it uses have n tilability constraint and are set up in such a way that when white needs to capture a knight, a faster win than the one in the strong rook setup itself is being threatened, obligating the black rook to block it instead of returning to stop the slower win anyway.

## Knight column
This is a tricky part of the setup that needs to be carefully checked to ensure there are no adversarial moves that one side can use to gain an advantage they shouldn't. 

This image shows a cross section of the idea, not necessarily to scale:
![Knight column](./knight-tower.png)

In this image, all rooks are virtual, except for the white rooks above black rooks at the bottom, which are strong virtual rooks. 
Every king in a green region is confined to only that region using a series of virtual rooks elsewhere.

The basic idea is that during a part of the counter setup, a white king will need to move from m5 to o8 in order to make progress, for which it needs to go through n6 and n7. (anywhere else is covered by virtual rooks). To allow this, white's bishop must move from h11 to j9 (this bishop is constrained to its diagonal such that those are the only useful squares for it to be; by a pinning bishop not shown. This bishop can actually be a rook in three dimensions, but a bishop is easier to visualise in 2D). 
This forces black's king to block their rook that's constraining the n column, but will also remove its defense of c6, giving black an oppotunity to move a king there, opening a discovered attack on white's king and forcing it to c14.

The c column normally provides a pin from a white virtual rook of black's knight against a pair of black kings. The kings can move arbitrarily high upwards, and aren't threatened by white's arbitrary height rook columns as they can move faster than white can raise the ceiling of those columns, but they are constrained to the column by a ring of 8 white virtual rooks (2 of which are shown in this cross section at b17 and d17).

When white's king is forced to the c column, black has an oppotunity to move their knight. White then moves their king again to re-open the discovered check, forcing the knight to move back to its home column. (the fact that there are 2 kings rather then 1 at the top ensures black can't just move one out of the way above the knight's new position instead). 

If the knight had only moved out by 1 column, all is fine - it can return to either the same position it left, or up or down 4 spaces, which is fine.
However, if the knight had moved two columns over, it would be able to return only 2 columns higher or lower than where it started, breaking the modulo 4 constraint. Thus, we have strong virtual rooks covering the 4 bad columns (2 shown in this cross section) it could move to this way.
(if it moved 2 columns over but one column horizontally, i.e. toward/away from the viewer in this cross section, that's fine as it's only capable of returning to its original position)

When black moves their knight to a bad column this way, the resulting rook captures allow white to threaten a win using the column the knight normally defends - without a knight to defend it, the rook must move t this column instead, preventing it from moving to its home position and allowing the win enabled from the strong virtual rook setup. 
Care must be taken to ensure white's bishop can move back to cover c6 and prevent *black* from having a potential win if they were allowed to move arounf their kings to discover another check on white's king.

One final detail is that the knight shouldn't be allowed to go too low, lest it start getting in the way of the rest of the setup. To accomplish this, there's a black rook in lowest row of the tower, such that if the knight goes too low as to block it, it enables white to cause a checkmate.

So, overall, we have a system in which, whenever white wants to move a king through m5 to o8, it allows black an opportunity to move their knight upwards or downwards by 4 spaces, which is what we need for the helix constraint.

Full check of the intended protocol and possible adversarial moves by black indicating they don't grant an advantage:

