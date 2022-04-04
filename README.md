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
        * `<date>`
            * default.0.tif - a TIFF format file containing ...
            * default.1.tif - a TIFF format file containing ...
            * ktx
                * `<number, 1-8>`
                    * `<number, 1-8>` (this structure of prefixes will continue for up to 6 levels)
                    * block_8_xy_`<number, 1-8>`.ktx - KTX format file ...
                * block_8_xy_.ktx - KTX format file ...
            * tilebase.cache.yml - a YML format file containing ...
            * transform.txt - a text file containing ...
    * registration
        * `<date>`
            * `<date>`.horta.yml - YML format file ...
            * `<date>`.nrrd - NRRD format file ...
            * `<date>`.yml - YML format file ...
            * HortaObj
                * `<cell type>`.obj (there will be many of these .obj files in the prefix; one per cell type)
            * Transform.`<date>`.h5 - - H5J format file???
            * Transformed_`<date>`.nrrd - NRRD format file ...
    * segmentation
        * `<date>`
    * tracings
        * Finished_Neurons
            * `<date>`
        * tracing_complete
            * `<date>`
