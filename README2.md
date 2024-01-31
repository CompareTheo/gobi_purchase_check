# GobiChecker

GobiChecker is a program that takes a brief export of Gobi requests and searches Alma for duplicate holdings in the institution zone (IZ).

The scripts in this project are the original work of [Jermey Hobbs](https://github.com/MrJeremyHobbs). More details about the updates to the code found in this repository and statements about coding credit can be found in the acknowledgements section below. 

## Description
GobiChecker is a program that takes a brief data export from Gobi and searches Alma for duplicate holdings in the institution zone (IZ). This program uses the Search/Retrieve via URL (SRU) protocol to query Alma using the alma.isbn (ISBN query), alma.title (Title query), and alma.all_for_ui (Keyword query) indexes. 

## Getting Started

### Dependencies

* Alma requires the setup of an SRU integration profile. More information about setting up an SRU integration profile can be found in the [Ex Libris Developer Blogs](https://developers.exlibrisgroup.com/blog/how-to-configure-sru-and-structure-sru-retrieval-queries/)
* Scripts require the creation of a "config.ini" file consisting of version numbering, download directory, Alma institution code, Alma institution zone path, and log directory. For a more complete example of the appropriate structure and format, see [Jeremy Hobbs' GobiChecker Repository](https://github.com/MrJeremyHobbs/GobiChecker).

## License

This project is licensed under the MIT License - see the LICENSE.md file for details

## Acknowledgments

The inception and a substantial portion of the codebase for this project originated from the creative mind and diligent efforts of [Jeremy Hobbs](https://github.com/MrJeremyHobbs). The fundamental ideas and structures were crafted by Jeremy, forming the foundation upon which this forked repository is built.

The current state of the code represents a 10% net increase in modifications from Jeremy's original work. All alterations and enhancements made are documented in the section below.

I wish to publicly express my gratitude to Jeremy for his invaluable contributions to this project. His openness in sharing his original code under such permissive licensing are the foundation of the improvements and customizations introduced in this fork. He has my deepest thanks and professional admiration.

## Change Log

**gobi/__init__.py**

* Two additional parsing sections have been added:
    1. The first simply defines a variable for "selector," a GOBISMART custom field label that we require from selector/liaisons and output into the PO-Line. 
    2. The second defines a variable for "intentional duplicate" which is an additional GOBISMART custom field label that is notated by the Ordering Assistant to clarify to Gobi our desire to duplicate a previously purchased title.

**alma/sru.py**

    * A new import was module was imported which references a "elookup.py" file. This file is a list of Alma Electronic Collection IDs which correspond to collections of non-owned, temporary, or subscribed electronic portfolios.
    * 