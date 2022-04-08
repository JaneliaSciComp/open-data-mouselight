# open-data-mouselight
MouseLight Gen1 Imagery hosted on AWS Open Data 

This repository contains static files for MouseLight's AWS Open Data. These folder are mirrored on S3 with each top-level folder corresponding to a public bucket:
* [janelia-mouselight-imagery](janelia-mouselight-imagery/README.md)

## Implementation notes

* The Markdown used in this repo contains footnotes, which are [not supported by Github](https://github.com/github/markup/issues/498), so they will not render correctly in the Github preview. The actual publication target for these README's is [Quilt](https://open.quiltdata.com/b/janelia-mouselight-imagery) which does support footnotes. 

## Bucket structure

Files are organized by type and date:

* Root
    * images
        * `<date>` - each date represents an individual brain
            * default.0.tif - a TIFF format file containing single channel of entire image in low resolution used for 2-D viewer
            * default.1.tif - a TIFF format file containing single channel of entire image in low resolution used for 2-D viewer
            * ktx - texture files for Horta 3D viewer
                * `<number, 1-8>`
                    * `<number, 1-8>` (this structure of prefixes will continue for up to 7 levels)
                    * block_8_xy_`<number, 1-8>`.ktx - KTX format file containing actual image
                * block_8_xy_.ktx - KTX format file ...
            * tilebase.cache.yml - a YML format file containing spatial index for tiles
            * transform.txt - a text file containing origin, scaling, and number or levels in octree
    * registration
        * `<date>`
            * `<date>`.horta.yml - YML format file ...
            * `<date>`.nrrd - NRRD format file ...
            * `<date>`.yml - YML format file ...
            * HortaObj
                * `<brain region>`_`<brain area ID>`.obj - multiple OBJ files (one per brain region) containing mesh
            * Transform.`<date>`.h5 - - H5J format file
            * Transformed_`<date>`.nrrd - NRRD format file ...
    * segmentation
        * `<date>` - SWC format neuron fragments generated during machine learning - structures vary
    * tracings
        * Finished_Neurons
            * `<date>`
                * G-`<number>`
                * `<date>`_G-`<number>`_AZ.swc - SWC format file
                * `<date>`_G-`<number>`_CA.swc - SWC format file
                * `<date>`_G-`<number>`_dendrites.swc - SWC format file
                * consensus
                    * `<date>`_G-`<number>`_base.swc - SWC format file
                    * `<date>`_G-`<number>`_consensus.swc - SWC format file
                    * AZ_uni.swc - SWC format file
                    * Backup
                        * `<date>`_G-`<number>`_consensus.swc - SWC format file
                    * CA_uni.swc - SWC format file
        * tracing_complete
            * `<date>`
                * G-`<number>`
                    * base.swc - SWC format file
                    * consensus.swc - SWC format file of axon
                    * dendrite.swc - SWC format file of dendrite
                    * soma.txt - text format file containing soma location
                    * somaLoc.png - PNG format file
                    * somaOnt.png - PNG format file
                    * Thumbs.db
                    * uni1.swc - SWC format file
                    * uni2.swc - SWC format file
