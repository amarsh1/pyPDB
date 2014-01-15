pyPDB
=====

**pyPDB** is a python class that represents a structural PDB file (not related to the python PDB debugger). It enables swift utility functions that can be used to prepare PDB files for further analysis and retrieve information from it.

Developed by Gareth Price (gareth.price@warwick.ac.uk). Please feel free to email or to use the issues pane at Github.

Instructions for installation
------

Download the latest release or the bleeding edge version and extract the files. `pyPDB.py` contains all necessary code.

Examples
------

```python
from pyPDB import *

# load pdb
p = pyPDB('pdbs/gly.pdb')

# select one atom
p.selectAtom(4)

# select multiple atoms individually (this continues after the previous one)
p.selectAtom(5).selectAtom(6)

# or select multiple atoms all in one go
p.selectAtoms([4, 5, 6])

# the 'p' pyPDB instance now has a selectedAtoms attribute that is iterable:
for atom in p.selectedAtoms:
    print '{}{}'.format(atom.name, atom.id)

# calculate a distance map
print p.distanceMap()

# and also plot it
p.plotDistanceMap(save=False, close=True)

# calculate the distance between two atoms
print p.distanceBetweenAtoms(8, 9)

# calculate atoms within a given distance of another atom
print p.atomsWithinDistanceOfAtom(10, 3)

# you can iterate over something like the above such as:
atomsWithinDistance = p.atomsWithinDistanceOfAtom(10, 3)
i = 0
for x in atomsWithinDistance[0]:
    print 'Atom {}{} is within {} of {}{}: {}'.format(x.name, x.id, 3,
        p.molecule.atoms[10].name, 10, atomsWithinDistance[1][i])
    i += 1

# or even make an amber mask:
print p.toAmberMask('atoms')

# output a description of 'p' as json
print p.toJSON()

# reduce a pdb:
p.reduce()

# ...which can be iterated over:
for atom in p.reduce():
    print '{}{}'.format(atom.name, atom.id)

# the selection (or all atoms if no selection) can be written to a pdb file
p.writePDB()

# the selection can be removed using
p.removeSelection()

# translate the coordinates (or selection)
p.translateCoordinates([1,1,1])
for atom in p.molecule.atoms:
    a = p.molecule.atoms[atom]
    print "[{0:g}, {1:g}, {2:g}]".format(a.x, a.y, a.z)
```

License
---------

All necessary information can be found in LICENSE (GPL v3). In brief this means:

You may copy, distribute and modify the software as long as you track changes/dates of in source files and keep modifications under GPL. You can distribute your application using a GPL library commercially, but you must also provide the source code.

(obtained from http://www.tldrlegal.com/license/gnu-general-public-license-v3-(gpl-3))
