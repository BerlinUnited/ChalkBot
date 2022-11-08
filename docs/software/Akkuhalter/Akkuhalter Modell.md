The Akkuhalter 3D Model was created with Inventor and is therefore open for extensions and refactoring.

To understand how the model has been built from ground and what the components are I will first give a brief overview of the building process of the model and then write a short description for every component.

<br>
<b>Building Process</b>

Measurement:

![Trying to get the size right]("Screenshot 2022-11-08 190116.png")


There are many ways to achieve this and I tried several, f.e. the option above.

Because it was not precise enough I used a screenshot of a stl model with Vertex-View in Blender:

![Reference Image](Screenshot 2022-07-11 121428.png)

I loaded it into Inventor as a Reference-Image for the vertical sketch. I recommend using it. It should now match the real dimensions.

After a lot of try and error i found a solution for constructing the triangle sketch. 

![Triangle Base Construction](Bild1.png)

The size is determined by the diameter of the circle. The math is: `1/2 * length of sides / cos(30)` but it is coded in a transitive variable so you use the variable for the length of the sides.

Then I rounded the corners, also with a parameter ("Dreiecksabrundung"). And made an outer shape with polygons.
And finally it was all a matter of a lot of sketching and extruding.

I think it doesnt make sense to replicate each step, so for more details take a look at the components description instead.

<br>
<br>
<b>Components</b>

<br>
<i>Vertikale Skizze</i>

This is the main sketch for all vertical extrusions.
Affecting Variables:

    Dreiecksabrundung,
    Dreieckskantenlänge,
    Kreisradius (transitiv),
    Wanddicke,
    Lochdurchmesser


![Vorlage von oben](Screenshot 2022-11-08 192517.png)

<br>
<i>Hauptkörper oben</i>

Body of triangle with outer shape extruded up.
Affecting Variables:

    Dreiecksabrundung,
    Dreieckskantenlänge,
    Kreisradius (transitiv),
    Waagrechter Aufsatzdicke

<br>
<i>Hauptkörper unten</i>

Body of outer shape extruded down with defined thickness.
Affecting Variables:

    Dreieckshöhe,
    Wanddicke
    
<br>
<i>Bodenkörper</i>

The body wich is translated down to the bottom.
Affecting Variables:

    Wanddicke
    
<br>
<i>Boden</i>

The translation of "Bodenkörper" to the bottom.
Affecting Variables:

    Dreieckshöhe
    
<br>
<i>Akkuführungslasche vertikale Skizze</i>

A sketch on top of "Hauptkörper oben" for extruding the gap where the battery is sliding through.
Affecting Variables:

    Waagrechter Aufsatzdicke,
    BefestigungsDicke (not working)
    
<br>
<i>
    
<br>
<i>Akkuführungslasche boolean x</i>

The boolean extrusion for the gap. It affects the corresponding part of the other bodies.
Affecting Variables:

    Waagrechter Aufsatzdicke,
    BefestigungsDicke (not working),
    Klipphöhe
    
<br>
<i>Kontaktlöcher</i>

Creates the small holes in the bottom as boolean extrusion.

<br>
<i>Halterungsebene</i>

The body with the screw-holes for fixing the model.
Affecting Variables:
    
    BefestigungsDicke,
    AußenkörperKreisRadius (not working)
    
<br>
<i>Schraubenlöcherabrundung</i>

The phase around the "Kontaktlöcher".
Affecting Variables:

    Phasendicke
