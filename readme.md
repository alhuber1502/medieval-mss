## Medieval Manuscripts in Oxford Libraries

This repository contains the TEI data that represents the Bodleian Library's catalogue of manuscripts written from the Middle Ages, [Medieval Manuscripts in Oxford Libraries](https://medieval.bodleian.ox.ac.uk).

It also contains several scripts and tools for processing this data into a Solr instance for use with our
Blacklight search service.

### Indexing the Catalogue

**NB: This information is probably only useful if you're working in the Bodleian!**

This project ships with a version of the Saxon XML processor. The only dependency needed to run this
is a working Java installation. Inside the `processing` folder you will find two shell scripts and several
xQuery and XSLT files.

The `generate-html.sh` script will generate an HTML representation of the TEI data, for displaying
the record in the front-end catalogue.

The `generate-solr-document.sh` script will create a Solr XML document, which can then be passed along
to a running Solr instance. The arguments for this command are:

```bash
$> ./generate-solr-document.sh [xQuery File] [Solr XML Output filename] [Solr record type] [Solr server]
```

To index the manuscripts, you should first create a `html` folder inside of the processing folder, then run:
 
```bash
$> ./generate-html.sh
$> ./generate-solr-document.sh manuscripts.xquery mss_solr_index.xml manuscript [Some Solr Server]
```

For the Solr record type you should use `manuscript` for manuscripts, `person` for people, `place` for places,
and `work` for works.

### Indexing in Windows 7

The indexing scripts require `curl`, `tidy` alias HTML tidy and `xmllint`. These tools will need to be installed on your local machine, if you do not already have them. `curl` is included with posh-git (see below).

The scripts require a terminal running BASH. If you have GitHub Desktop installed on your machine, this should include Git Shell alias posh-git, which is a package for Windows PowerShell that will allow you to execute BASH shell scripts. 



### Modifying the HTML output

The HTML representations of each record is generated by the `convert2HTML.xsl` script. Modifying this
and running the `generate-html.sh` script will generate new HTML, which will then be picked up by the
Solr indexing process and incorporated into the Solr index for record display.
