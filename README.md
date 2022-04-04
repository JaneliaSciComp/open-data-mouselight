# open-data-mouselight
MouseLight Gen1 Imagery hosted on AWS Open Data 

This repository contains static files for MouseLight's AWS Open Data. These folder are mirrored on S3 with each top-level folder corresponding to a public bucket:
* [janelia-mouselight-imagery](janelia-mouselight-imagery/README.md)

## Implementation notes

* The Markdown used in this repo contains footnotes, which are [not supported by Github](https://github.com/github/markup/issues/498), so they will not render correctly in the Github preview. The actual publication target for these README's is [Quilt](https://open.quiltdata.com/b/janelia-mouselight-imagery) which does support footnotes. 

## Bucket structure

* Root
    * images
        * `<date>`
    * registration
        * `<date>`
    * segmentation
        * `<date>`
    * tracings
        * Finished_Neurons
            * `<date>`
        * tracing_complete
            * `<date>`

## Bucket Structure

Files are organized by type and date:

* Root
    * `<release name>`
        * _JSON metadata file_ - metadata about the release including the associated publication(s)
        * `<fly line publishing name>`
            * _JSON metadata file_ - metadata about the images, including curated anatomical annotations
            * _LSM files (LSM)_ - microscope imagery in Zeiss LSM format
            * _unaligned image stack files (H5J)_ - 3d imagery, distortion corrected, merged, and stitched
            * _aligned image stack files (H5J)_ - 3d imagery registered to a canonical template
            * _MIP files (PNG)_ - maximum intensity projections for rapid viewing
            * _movie files (MP4)_ - small movies for rapid viewing of Z slices

FlyLight file names contain metadata as follows:
```
[Publis
