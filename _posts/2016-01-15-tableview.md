---
layout: post
title: Exploring GMC Properties
---

The main output of [CPROPS](https://github.com/low-sky/cprops) and [cpropstoo](https://github.com/low-sky/cpropstoo) are tables of cloud parameters.  In astronomy, a common table file format is that of the FITS table where FITS refers to the Flexible Image Transport System.  The original FITS format was designed for images, but it has been extended in hundreds of different ways including for tables and catalogs.  We can explore the table from one of two approaches.  The first is in an exploratory mode, and I recommend using the programs (TOPCAT)[http://www.star.bris.ac.uk/~mbt/topcat/] or (glue)[http://www.glueviz.org/en/stable/].  The second mode is more making proper plots and doing good analysis using python.  If you are given a binary table (of GMC properties), here's how to start exploring.  

## TOPCAT

TOPCAT has [extensive documentation](http://www.star.bris.ac.uk/~mbt/topcat/sun253/index.html) but this will focus on a few methods that we use a lot.  To start TOPCAT on a server with it installed, you can just call

	topcat table_name.fits
	
where `table_name.fits` is the filename of the table you are exploring.  This will pop up main window which looks like this:

![Spectral Cubes](/images/LoadWindow.png)