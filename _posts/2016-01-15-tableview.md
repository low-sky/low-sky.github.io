---
layout: post
title: Exploring GMC Properties
---

The main output of [CPROPS](https://github.com/low-sky/cprops) and [cpropstoo](https://github.com/low-sky/cpropstoo) are tables of cloud parameters.  In astronomy, a common table file format is that of the FITS table where FITS refers to the Flexible Image Transport System.  The original FITS format was designed for images, but it has been extended in hundreds of different ways including for tables and catalogs.  We can explore the table from one of two approaches.  The first is in an exploratory mode, and I recommend using the programs [TOPCAT](http://www.star.bris.ac.uk/~mbt/topcat/) or [glue](http://www.glueviz.org/en/stable/).  The second mode is more making proper plots and doing good analysis using python.  If you are given a binary table (of GMC properties), here's how to start exploring.  

## TOPCAT

TOPCAT has [extensive documentation](http://www.star.bris.ac.uk/~mbt/topcat/sun253/index.html) but this will focus on a few methods that we use a lot.  To start TOPCAT on a server with it installed, you can just call

	topcat table_name.fits
	
where `table_name.fits` is the filename of the table you are exploring.  This will pop up main window which looks like this:

![Spectral Cubes](/images/LoadWindow.png)

You can mouse over the different buttons in the top row to get some help text about their functions.  The main thing you'll want to do is to make bivariate plots, which is the button with white square.  This brings up a plot window for the table you have selected.  You can then select from the bottom-right panel all the different keys (i.e., columns) in the table to plot them against each other.  Let's start by making a classic GMC properties plot: the luminous mass vs the virial mass of the cloud.  These are all calculated using the methods described in the [CPROPS paper](http://adsabs.harvard.edu/abs/2006PASP..118..590R).  The tag name for the luminous mass is just `MASS_EXTRAP` and the virial mass is called `VIRMASS_EXTRAP_DECONV`, both of which have units in solar masses.  Go ahead and make this plot by changing the axes accordingly.  The graph should look something like this:

![Massplots](/image/MlumMvir.png)

This isn't very illuminating since all the points are clustered down in the bottom of the plot.  Go ahead and click the axes tab in the bottom left and click `X log` and `Y log` to make this into a log-log plot:

![Massplots](/image/logMlumMvir.png)



