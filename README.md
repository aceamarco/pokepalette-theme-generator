# pokepalette-theme-generator

There’s this cool website called https://pokepalettes.com that can generate the (sorted by pixel density) hex-coded color palette of any Pokemon before Gen 5 (before Pokemon games used 3D sprites).

Let’s users enter their favorite Pokemon name / number (like on the pokepalette website) and then have it grab the the sorted hex palette data from the pokepalette website and generate a VSCode theme based on that pokemon's color palette.

VSCode themes can be created by generating a JSON file that configures the hex color of components on their UI.

So my idea was that the site could give a user the JSON fields they need copy and paste into their settings.json file, or let them download it period.

Things I’ve considered so far:

    How will I actually gather the Pokemon color Palette information?
        I did some digging into the source code for the pokepalette website. The website hosts 2-D images of every pokemon you can search for. When you search for a pokemon, it makes a request for that image, loops through every pixel in the sprite, and then populates a dictionary with the the amount of times a hex color appears in a pixel. Finally it sorts that dictionary into an array (in ascending order) and adds that information to the UI.
        Everything I explained above can be seen in the source code here: main.js file that initializes data model pokeModel.js file that calculates and sorts the pixel density map of a pokemon sprite, in the second link the _getspritedata function is where everything I described happens
        If you’d like to follow the original lifecycle on your own, the searchOnEnterFunction is where it starts
    How will my website generate themes for VSCode?
        Like I mentioned before every color on the VSCode UI can be edited through the workbench.colorCustomizations field in the settings.json file. This is what all themes downloaded on VSCode edit.
        Given the array of hex values from pokepalette, I could assign those colors to UI components by generating the JSON fields need to change colors on VSCode
    How will I make sure that the color theme is usable/readable?
        Using the hex color palette, I could find the color that is closest to the complementary color of #1 ranked color in the palette. That way things are still readable and contrast each other while remaining withing the color palette of the Pokemon. Please see the images below for an idea of how I would find the "nearest complimentary color" given the hex color codes.

