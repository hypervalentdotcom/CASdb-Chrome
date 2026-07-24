# CAS DB

CAS DB is a Chrome Manifest V3 extension for drawing one molecule in a
ChemDoodle sketcher and finding checksum-valid CAS numbers listed among the
synonyms of its matching PubChem compound.

## Installation

1. Open `chrome://extensions`.
2. Enable **Developer mode**.
3. Click **Load unpacked**.
4. Select the `molecule-cas-extension` folder.
5. Pin **CAS DB** to the Chrome toolbar.

The extension has no build step and does not load remote scripts.

## Usage

1. Open the extension.
2. Draw one molecule in ChemDoodle.
3. Click **Find CAS**.
4. Copy the result, open its PubChem CID, check SpectraBase, search supplier
   catalogues, or expand **Physicochemical properties**.

The drawn structure and the latest successful result are stored locally. They
remain visible after the popup closes and are restored the next time it opens.
Editing the structure clears the previous result. Using ChemDoodle's clear
button removes both the structure and its saved result.

The search submits the drawn MOLFile to the PubChem PUG REST exact-identity
operation. CAS-formatted synonyms are then checked with the CAS checksum
algorithm. The extension also displays molecular weight, density, melting and
boiling points, the usual physical state at 20 °C, and molecular formula.
Experimental values come from PubChem PUG View annotations and may be missing
for some compounds.

After finding a CAS number, CAS DB checks whether SpectraBase has a reference
for it and links to the corresponding search.

The **Suppliers** menu opens CAS searches at Sigma-Aldrich (Merck), TCI,
Fluorochem, abcr, EnamineStore, and CymitQuimica. EnamineStore provides a
searchable building-block catalogue.

## Important limitation

PubChem notes that synonym lists may contain unverified identifiers. CAS DB is
a research aid, not an official CAS Registry confirmation. A PubChem record may
also list several CAS numbers; the extension shows the first checksum-valid
number in PubChem order.

## Permissions

- `https://pubchem.ncbi.nlm.nih.gov/*`: structure identity, property, and
  synonym requests through PUG REST and PUG View.
- `https://spectrabase.com/*`: spectral-reference check by CAS number.
- `storage`: local persistence of the structure and latest successful result.
- `clipboardWrite`: copy the CAS number when the user clicks the copy button.

CAS DB does not collect user data. The molecular drawing is sent only to
PubChem when the user starts a search. Supplier and spectral sites are opened
only when the user follows their links, except for the automatic SpectraBase
availability check after a successful CAS search.

## Tests

With Node.js 18 or later:

```sh
npm test
```

## Licence

ChemDoodle Web Components is distributed under GPLv3. This extension and its
distribution must therefore comply with GPLv3; the full text is included in
`LICENSE`. Contact iChemLabs for a proprietary ChemDoodle licence if needed.

Documentation and services:

- <https://web.chemdoodle.com/tutorial/2d-structure-canvases/sketcher-canvas>
- <https://web.chemdoodle.com/installation/license>
- <https://pubchem.ncbi.nlm.nih.gov/docs/pug-rest>
- <https://spectrabase.com/>
- <https://enaminestore.com/>
