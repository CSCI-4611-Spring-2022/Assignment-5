# Assignment 5: Artistic Rendering

**Due: Thursday, April 14, 11:59pm CDT**

GLSL shaders make it possible for us to create some amazing lighting effects in real- time computer graphics. These range from photorealistic lighting to artistically inspired non-photorealistic rendering, as featured in games like *The Legend of Zelda: The Wind Waker* and *Team Fortress 2*. In this assignment, you will implement GLSL shaders that can produce both realistic per-pixel lighting, "toon shading," and a variety of other effects. You will also implement another shader that adds silhouette edges to complete a cartoon effect.

In this assignment, you will learn:

- How to calculate realistic and artistic per-pixel lighting in real-time.
- How to modify geometry on the fly to create viewpoint-dependent effects such as silhouette edges.
- How to implement and use your own shader programs!

You can try out the [instructor's implementation](https://csci-4611-spring-2022.github.io/Builds/Assignment-5) in the Builds repository on the course GitHub.

## Submission Information

You should fill out this information before submitting your assignment. Make sure to document the name and source of any third party assets that you added, such as models, images, sounds, or any other content used that was not solely written by you. 

Name:

Third Party Assets:

Wizard Bonus Functionality:

## Prerequisites

To work with this code, you will first need to install [Node.js](https://nodejs.org/en/) and [Visual Studio Code](https://code.visualstudio.com/). 

## Getting Started

The starter code implements the general structure that we reviewed in lecture.  After cloning your repository, you will need to set up the initial project by pulling the dependencies from the node package manager with:

```
npm install
```

This will create a `node_modules` folder in your directory and download all the dependencies needed to run the project.  Note that this folder is `.gitignore` file and should not be committed to your repository.  After that, you can compile and run a server with:

```
npm run start
```

The build system should launch your program in a web browser automatically.  If not, you can run it by pointing your browser at `http://localhost:8080`.

## Requirements

We provide code for loading several 3D model files, rotating them on the screen using the mouse, and toggling between Gouraud shading, Phong shading, "toon" shading, and wireframe shading. For this assignment, you **only** need to modify the GLSL code in the .vert and .frag shader programs.  However, you are welcome to add to the TypeScript code if you want to add additional wizard functionality.

There are three shader mini-programs that you need to complete:

1. Complete the `phong.frag` fragment shader to correctly calculate per-pixel shading using the standard Phong (or Blinn-Phong) lighting model. 
2. Complete the `toon.frag` fragment shader to correctly calculate the per-pixel toon shading, using the *diffuseRamp.png* and *specularRamp.png* textures to control the lighting.
3. Complete the `outline.vert` vertex shader to draw a black outline for the silhouette edges of the mesh, when rendering in "toon" mode.

## Graphics Framework

to be added.

## Per-Pixel Phong Shading

In class, we will work on some shader programs that calculate ambient, diffuse, and specular lighting using per-vertex (Gouraud) shading. Your job is to extend the concepts and programs we develop in class to implement per-pixel Phong shading with the same lighting model. You should be able to build this by extending the shaders that we discuss and develop in class.

Implement a shader program that performs all the calculations to accurately calculate the Phong lighting model for each pixel.  The lighting terms must vary per-pixel based on the normal and the light position, as well as the various material properties (such as the specular exponent). You should implement this shader following the lighting model equations discussed in class. 

For the specular component, you may use either the reflection vector or halfway vector method presented in lecture.  The traditional Phong model uses the reflection vector, and the halfway vector is a modification known as the Blinn-Phong model. The instructor's implementation uses the reflection vector, but either solution is acceptable.

## Flexible Toon Shading Using Texture Images

Once you have Phong shading working, including ambient, diffuse, and specular lighting, then you should copy and paste this code into `toon.frag`.  You can then adapt the shader to implement cartoon-style shading. Rather than setting the final color based on the intensity of light you calculate for the Phong model, you will instead use this intensity value as a lookup into a texture, and use that to compute the final color. A texture used in this way is typically called a "ramp." Using this strategy, you will be able to get a wide range of different lighting effects just by switching the texture you use for input.

Suppose that we use the dot product in the diffuse term, **n** &middot; **l**, to look up the texture.  Because this value represents the cosine of the angle between the two vectors, it will range from -1 to 1. We need to map this value to a texture coordinate, which will range from 0 to 1. 

If we then, use `standardDiffuse.png` (see below), which is zero in the left half corresponding to negative n &middot; l, and increases linearly from 0 to 1 for positive n &middot; l, then we’ll get back the standard diffuse lighting term.

## Rubric

To be added.

## Wizard Bonus Challenge

All of the assignments in the course will include great opportunities for students to go beyond the requirements of the assignment and do cool extra work. On each assignment, you can earn **one bonus point** for implementing a meaningful new feature to your program. This should involve some original new programming, and should not just be something that can be quickly implemented by copying and slightly modifying existing code.  

There are great opportunities for extra work in this assignment. For example:

## Submission

When you commit and push your assignment to GitHub, an automated script will build and deploy the production code to the `gh-pages` branch of your repository.  However, your submission is not complete until you do the following:

1. Open your repository on GitHub and go to Settings->Pages.
2. Change the source to the `gh-pages` branch, then save.

You will need to wait a few minutes for the website to deploy.  After that, make sure to test everything by pointing your web browser at the link generated for your build:

```
https://csci-4611-spring-2022.github.io/your-repo-name-here
```

If your program runs correctly, then you are finished!  The published build will indicate to the TAs that your assignment is ready for grading.  If you change your mind and want to make further changes to your code, then just delete the `gh-pages` branch and set the GitHub pages source back to `None`, and it will unpublish the website.

Note that the published JavaScript bundle code generated by the TypeScript compiler has been minified so that it is not human-readable. So, you can feel free to send this link to other students, friends, and family to show off your work!

## Acknowledgments

This assignment was based on content from CSCI 4611 Fall 2021 by [Daniel Keefe](https://www.danielkeefe.net/).

## License

Material for [CSCI 4611 Spring 2022](https://canvas.umn.edu/courses/290928/assignments/syllabus) by [Evan Suma Rosenberg](https://illusioneering.umn.edu/) is licensed under a [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-nc-sa/4.0/).