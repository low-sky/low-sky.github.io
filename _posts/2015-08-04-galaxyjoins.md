---
layout: post
title: Galaxy Database Joins
---

Eric asked for a list of galaxies with position angles and inclinations.  While I have a nice list for internal use, Adam and Karin have put together an extensive set of information [here](https://github.com/akleroy/galbase/).  This does beg the question of how to do a good table join and get out the information from a huge set of tables.  After much munging around with `astropy.table`, I managed to extract things using [this](https://gist.github.com/low-sky/01000ab550ebf88ab3a8).